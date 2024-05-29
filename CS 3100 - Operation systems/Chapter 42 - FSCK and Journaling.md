==FSCK== - the approach taken by older file systems to address the crash-consistency problem. (file system checker)

==journaling== - a technique which adds a little bit of overhead to each write but recovers more quickly from crashes or power losses.


![[Pasted image 20240409093036.png]]
the file system must perform three separate writes to the disk, one each for the inode (I[v2]), bitmap (B[v2]), and data block (Db). Note that these writes usually don’t happen immediately when the user issues a write() system call; rather, the dirty in- ode, bitmap, and new data will sit in main memory (in the page cache or buffer cache) for some time first; then, when the file system finally decides to write them to disk (after say 5 seconds or 30 seconds), the file system will issue the requisite write requests to the disk.
a ==crash== may occur and thus interfere with these updates to the disk. In particular, if a crash happens after one or two of these writes have taken place, but not all three, the file system could be left in a funny state.

## Solution #1: The File System Checker
The approach was to let inconsistencies happen and then fix them later (when rebooting).

It is run ==before== the file system is mounted and made available (fsck assumes that no other file-system activity is on-going while it runs); once finished, the on-disk file system should be consistent and thus can be made accessible to users.

- ==Superblock==: fsck first checks if the superblock looks reasonable, mostly doing sanity checks such as making sure the file system size is greater than the number of blocks allocated. Usually the goal of these sanity checks is to find a suspect (corrupt) superblock; in this case, the system (or administrator) may decide to use an alternate copy of the superblock.

- ==Free blocks==: Next, fsck scans the inodes, indirect blocks, double indirect blocks, etc., to build an understanding of which blocks are currently allocated within the file system. It uses this knowledge to produce a correct version of the allocation bitmaps; thus, if there is any inconsistency between bitmaps and inodes, it is resolved by trusting the information within the inodes. The same type of check is performed for all the inodes, making sure that all inodes that look like they are in use are marked as such in the inode bitmaps.

- ==Inode state==: Each inode is checked for corruption or other problems. For example, fsck makes sure that each allocated inode has a valid type field (e.g., regular file, directory, symbolic link, etc.). If there are problems with the inode fields that are not easily fixed, the inode is considered suspect and cleared by fsck; the inode bitmap is correspondingly updated.

- I==node links==: fsck also verifies the link count of each allocated in- ode. As you may recall, the link count indicates the number of different directories that contain a reference (i.e., a link) to this particular file. To verify the link count, fsck scans through the entire directory tree, starting at the root directory, and builds its own link counts for every file and directory in the file system. If there is a mismatch between the newly-calculated count and that found within an inode, corrective action must be taken, usually by fixing the count within the inode. If an allocated inode is discovered but no directory refers to it, it is moved to the lost+found directory.

- ==Duplicates==: fsck also checks for duplicate pointers, i.e., cases where two different inodes refer to the same block. If one inode is obviously bad, it may be cleared. Alternately, the pointed-to block could be copied, thus giving each inode its own copy as desired.

- ==Bad blocks==: A check for bad block pointers is also performed while scanning through the list of all pointers. A pointer is considered “bad” if it obviously points to something outside its valid range, e.g., it has an address that refers to a block greater than the partition size. In this case, fsck can’t do anything too intelligent; it just removes (clears) the pointer from the inode or indirect block.

- ==Directory checks==: fsck does not understand the contents of user files; however, directories hold specifically formatted information created by the file system itself. Thus, fsck performs additional integrity checks on the contents of each directory, making sure that “.” and “..” are the first entries, that each inode referred to in a directory entry is allocated, and ensuring that no directory is linked to more than once in the entire hierarchy.

fsck (and similar approaches) have a bigger and perhaps more fundamental problem: ==they are too slow.==

## Solution #2: Journaling (or Write-Ahead Logging)
When updating the disk, before overwriting the structures in place, first ==write down a little note (somewhere else on the disk, in a well-known location) describing what you are about to do.== Writing this note is the “write ahead” part, and we write it to a structure that we organize as a “==log==”; hence, write-ahead logging.

you can go back and look at the note you made and try again; thus, you will know exactly what to fix (and how to fix it) after a crash

### Writing to the journal:
![[Pasted image 20240409101907.png]]
1. The transaction begin (TxB) tells us about this update, including information about the pend- ing update to the file system (e.g., the final addresses of the blocks I[v2], B[v2], and Db), as well as some kind of transaction identifier (TID).
2. The middle three blocks just contain the exact contents of the blocks themselves; this is known as physical logging as we are putting the exact physical contents of the update in the journal (an alternate idea, logical logging, puts a more compact logical representation of the update in the journal, e.g., “this update wishes to append data block Db to file X”, which is a little more complex but can save space in the log and perhaps improve performance).
3. The final block (TxE) is a marker of the end of this transaction, and will also contain the TID.
Once this transaction is safely on disk, we are ready to overwrite the old structures in the file system; this process is called ==checkpointing==. Thus, to ==checkpoint== the file system (i.e., bring it up to date with the pend- ing update in the journal), ==we issue the writes I[v2], B[v2], and Db to their disk locations as seen above==; if these writes complete successfully, we have successfully ==checkpointed== the file system and are basically done.

Steps of journaling:
1. ==Journal write==: Write the transaction, including a transaction-begin block, all pending data and metadata updates, and a transaction- end block, to the log; wait for these writes to complete.
2. ==Checkpoint==: Write the pending metadata and data updates to their final locations in the file system.

An important aspect of this process is the atomicity guarantee provided by the disk. It turns out that the disk guarantees that any 512-byte write will either happen or not (and never be half-written); thus, to make sure the write of TxE is atomic, one should make it a single 512-byte block. Thus, our current protocol to update the file system, with each of its three phases labeled:
1. ==journal write==: Write the contents of the transaction (including TxB, metadata, and data) to the log; wait for these writes to complete.
2. ==Journal commit==: Write the transaction commit block (containing TxE) to the log; wait for write to complete; transaction is said to be committed.
3. ==Checkpoint==: Write the contents of the update (metadata and data) to their final on-disk locations.