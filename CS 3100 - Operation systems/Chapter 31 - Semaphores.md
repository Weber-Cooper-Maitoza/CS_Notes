A semaphore is an object with an integer value that we can manipulate with two routines; in the POSIX standard, these routines are ==`sem_wait()`== and ==`sem_post()`==.

MUST INITIALIZE TO SOME VALUE (EX. 1 in third argument)
```c
#include <semaphore.h>
sem_t s;
sem_init(&s, 0, 1);
```
`sem_init(`<1>, <2>, <3>`)`
1. address of sem_t object.
2. usually always 0. this indicates that the semaphore is shared between threads in the same process.
3. What value the Semaphore is initialize to EX. 1

### `sem_wait()`:
wait() just waits for the semaphore to become more than 0  
- wait decrements the semaphore On which the critical section is executed.

### `sem_post()`:
post() on the other hand increments the value of semaphore and returns

## Binary Semaphores (Locks):
![[Pasted image 20240317152104.png]]

## Semaphores As Condition Variables:
![[Pasted image 20240317152149.png]]


![[Pasted image 20240317152227.png]]
