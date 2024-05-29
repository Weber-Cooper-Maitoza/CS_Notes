we would like here instead is some way to put the parent to ==sleep== until the condition we are waiting for (e.g., t==he child is done executing==) comes true.
![[Pasted image 20240317133620.png]]

In multi-threaded programs, it is often useful for a thread to wait for some condition to become true before proceeding. The simple approach, of just spinning until the condition becomes true, is grossly inefficient and wastes CPU cycles, and in some cases, can be incorrect. Thus, how should a thread wait for a condition?

## Definition and Routines:
To wait for a condition to become true, a thread can make use of what is known as a condition variable.

A condition variable is an explicit queue that threads can put themselves on when some state of execution (i.e., some condition) is not as desired (by waiting on the condition)

```c
pthread_cond_t c;
pthread_cond_wait(pthread_cond_t *c, pthread_mutex_t *m);
pthread_cond_signal(pthread_cond_t *c);
```
- The wait() call is executed when a thread wishes to put itself to sleep; 
- the signal() call is executed when a thread has changed something in the program and thus wants to wake a sleeping thread waiting on this condition.

![[Pasted image 20240317135149.png]]

## The Producer/Consumer (Bounded Buffer) Problem:
Producers - generate data items and place them in a buffer
consumers - grab said items from the buffer and consume them in some way.

![[Pasted image 20240319093823.png]]

THINK GROCER ISLE OF PRODUCTS ON A SHELF
## Dining Philosophy:
`Five [philosophers](https://en.wikipedia.org/wiki/Philosopher "Philosopher") dine together at the same table. Each philosopher has his own plate at the table. There is a fork between each plate. The dish served is a kind of [spaghetti](https://en.wikipedia.org/wiki/Spaghetti "Spaghetti") which has to be eaten with two forks. Each philosopher can only alternately think and eat. Moreover, a philosopher can only eat his spaghetti when he has both a left and right fork. Thus two forks will only be available when his two nearest neighbors are thinking, not eating. After an individual philosopher finishes eating, he will put down both forks.`
