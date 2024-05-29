
Synchronization primitives  
-  Locks  
-  Mutex (Mutual exclusion)  
-  Semaphores  
-  Condition variables

## Locks:
==Locks== provide mutual exclusion to a critical section.

```c
pthread_mutex_t lock;  
pthread_mutex_lock(&lock);  
x = x + 1; /*or whatever your critical section is*/ pthread_mutex_unlock(&lock);
```

the mutex should be initialized properly.
```c
pthread_mutex_t lock = PTHREAD_MUTEX_INITIALIZER;
```

How to dynamically initialize it would be as follows:
```c
int rc = pthread_mutex_init(&lock, NULL); 
assert(rc == 0); // always check success!

pthread mutex destroy() // Should aways be used toghether
```

Should also check if lock fails:
```c
// Use this to keep your code clean but check for failures // Only use if exiting program is OK upon failure  
void Pthread_mutex_lock(pthread_mutex_t *mutex) {
	int rc = pthread_mutex_lock(mutex);
	assert(rc == 0);
}
```

Some other locks:
```c
int pthread_mutex_trylock(pthread_mutex_t *mutex); 
int pthread_mutex_timedlock(pthread_mutex_t *mutex, struct timespec *abs_timeout);
```

## Conditional Variables:
==Condition variables== are useful when some kind of signaling must take place between threads, if one thread is waiting for another to do something before it can continue.
```c
int pthread_cond_wait(pthread_cond_t *cond, pthread_mutex_t *mutex); 
int pthread_cond_signal(pthread_cond_t *cond);
```