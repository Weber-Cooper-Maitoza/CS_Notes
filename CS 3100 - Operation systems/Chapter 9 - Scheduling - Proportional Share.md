## proportional-share scheduler:
(also known as "fair-share scheduler")

==instead of optimizing for turnaround or response time, a scheduler might instead try to guarantee that each job obtain a certain percentage of CPU time.==

## lottery scheduling:
==tickets==, which are used to represent the share of a resource that a process
==The percent of tickets== that a process has represents its share of the system resource in question.

EX: Imagine two processes, A and B, and further that A has 75 tickets while B has only 25. Thus, what we would like is for A to receive 75% of the CPU and B the remaining 25%.

Advantages over traditional decision making algorithms:
1. random often avoids strange corner-case behaviors that a more traditional algorithm may have trouble handling.
2. random also is lightweight, requiring little state to track alternatives.
3. random can be quite fast.

## Ticket Mechanisms:
==ticket currency==, allows a user with a set of tickets to allocate tickets among their own jobs in whatever currency they would like (Global Currency is global tickets).

EX: A and B have each been given 100 tickets. User A is running two jobs, A1 and A2, and gives them each 500 tickets (out of 1000 total) in User A’s own currency. User B is running only 1 job and gives it 10 tickets (out of 10 total). The system will convert A1’s and A2’s allocation from 500 each in A’s currency to 50 each in the global currency; similarly, B1’s 10 tickets will be converted to 100 tickets. The lottery will then be held over the global ticket currency (200 total) to determine which job runs.

==ticket transfer==, a process can temporarily hand off its tickets to another process.

==ticket inflation==, a process can temporarily raise or lower the number of tickets it owns.

## Implementation:
```c
// Counter: used to track if we have found the winner yet
int counter = 0;

// Winner: use some call to a random generatior to get a value 
//.        between 1 and the # of total tickets.
int winner = getrandom(0, totaltickets);

// current: use this to walk through the list of jobs
node_t *current = head;

// loop until the sum of ticket values is > the winner
while (current) {

    counter = counter + current->tickets;
    if (counter > winner)

        break; // found the winner
    current = current->next;

}
// ’current’ is the winner: schedule it...
```

![[Pasted image 20240205102640.png]]

## Why not deterministic:
==stride scheduling==, a deterministic fair-share scheduler.
