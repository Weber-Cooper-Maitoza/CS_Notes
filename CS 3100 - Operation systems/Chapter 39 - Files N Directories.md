file  
-  Array of bytes  
-  Created, read, and written  
-  Identifier  
	- file Name (human redable) 
	-  Inode number (low-level name) OS level identifier  
Directory  
- Collection of files and sub-directories  
-  Identifier  
	-  Name  
	-  Inode number (low-level name)  
-  A directory always has two special entries: the . entry, which refers to itself, and the .. entry, which refers to its parent

A ==directory tree== or directory hierarchy organizes all files and directories into a large tree, starting at the ==root (/).==

## File System Interface:

### `open()` 
-  Creates a new file or opens an existing one 
- Returns a file descriptor that uniquely identifies a file 
- file descriptor: a pointer to an object of type file; once you have such an object, you can call other “methods” to access the file, like read() and write()

### `read()`  
### `write()`  
### `lseek()`  
### `close()`

### `fsync()`
### What does a file system need?  
- A way to keep track of allocated and free storage  
- A way to keep track of the directory structure  
- A way to store metadata about directories and files  
- A way to manage storage so all the storage belonging to a single file is accessible

### File Discriptor:
0 = Read
1 = Write
2 = log file

0, 1, 2  are RESERVED files.

![[Pasted image 20240328100920.png]]

## METADATA:

Getting Information About Files Beyond file access, we expect the file system to keep a fair amount of information about each file it is storing. We generally call such data about files metadata. To see the metadata for a certain file, we can use the ==stat()== or ==fstat()== system calls. These calls take a pathname (or file descriptor) to a file and fill in a stat structure as seen in Figure 39.5. 