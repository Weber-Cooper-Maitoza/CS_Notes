## Locks: The Basic Idea:
provides ==mutual exclusion== between threads
Desirable features of locks:
- Mutual Exclusion (MUTEX) - prevent multiple threads from entering critical section.
- Fairness - When open, do all threads have fair shot to use critical section.
- Performance - can speed up or slow down performance.

```c
pthread_mutex_t lock;
int count = 0;

void* doThis() {
	pthread_mutex_lock(&lock);
	count++;
	pthread_mutex_unlock(&lock);
}

int main() {
	pthread_t t1, t2;
	pthread_create
}
```

## Controlling Interrupts:
Assume we are running on such a single-processor system. By ==turning off interrupts== (using some kind of special hardware instruction) before entering a ==critical section==, we ensure that the code inside the critical section will ==not be interrupted==, and thus will execute as if it were ==atomic==.
When finished, we re-enable interrupts.

Problems:
- thread to perform a privileged operation (turning interrupts on and off), and thus trust that this facility is not abused.
- does not work on multiprocessors
- turning off interrupts for extended periods of time can lead to interrupts becoming lost

## Test And Set (Atomic Exchange):
The simplest bit of hardware to support for locking is known as a ==test-and-set instruction==, also known as ==atomic exchange==.

a simple lock without Atomic Exchange. THIS DOESNT WORK!!
```c
typedef struct __lock_t { int flag; } lock_t;

void init (lock t *mutex) {
	// 0 -> lock is available, 1 -> held 
	mutex-›flag = 0;
}

void lock(lock_t *mutex) {
	while (mutex->flag == 1)  // TEST the flag
		; // spin-wait (do nothing)
	mutex-›flag = 1; // now SET it!
}

void unlock (lock_t *mutex) {
	mutex-›flag = 0;
}
```
failed to provide the most basic requirement: providing mutual exclusion.

The thread waits to acquire a lock that is already held: it endlessly checks the value of flag, a technique known as ==spin-waiting==.

## Building A working Spin Lock:

Test And Set:
```c
int TestAndSet(int *old_ptr, int new) {
	int old = *old_ptr; // fetch old value at old_ptr
	*old_ptr = new;     // store ’new’ into old_ptr
	return old;         // return the old value
}
```
It returns the old value pointed to by the ptr, and simultaneously updates said value to new. The key, of course, is that this sequence of operations is performed ==atomically==.

Spin Lock:
```c
typedef struct __lock_t {
	int flag;
} lock_t;

void init(lock_t *lock) {
    // 0 indicates that lock is available, 1 that it is held
    lock->flag = 0;
}
void lock(lock_t *lock) {
    while (TestAndSet(&lock->flag, 1) == 1)
        ; // spin-wait (do nothing)
}
void unlock(lock_t *lock) {
    lock->flag = 0;
}
```
requires a ==preemptive scheduler==

## Compare-And-Swap:
```c
int CompareAndSwap(int *ptr, int expected, int new) {
    int actual = *ptr;
    if (actual == expected)

        *ptr = new;
    return actual;
}
```
The basic idea is for compare-and-swap to test whether the value at the address specified by ptr is equal to expected; if so, update the memory location pointed to by ptr with the new value. If not, do nothing.