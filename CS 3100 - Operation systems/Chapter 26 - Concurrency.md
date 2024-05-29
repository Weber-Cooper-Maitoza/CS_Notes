## The point of threads:
also known as a ==light weight process==
==THREE FILES ARE GIVEN TO EVERY PROCESS, standard Input (0), standard output(1), error file. ==

![[Pasted image 20240227093707.png]]

Each thread gets a stack in the program's virtual address space.
any stack-allocated variables, parameters, return values, and other things that we put on the stack will be placed in what is sometimes called ==thread-local storage==, i.e., the stack of ==the relevant thread.==

STORED IN THE ==THREAD CONTROL BLOCK (TCB)==!!!
==EACH THREAD KEEPS TRACK OF STACK AND REGISTERS IN TCB==
## Creating threads in C:
```c
#include <pthread.h>

void *function(void *args) { // has to be pointer fucntion with void *args
	printf("%s\n", (char *) arg);
	return NULL;
}

int main() {
	pthread_t t1, t2;

	int rc1;
	int rc2;

	rc1 = pthread_create(&t1, NULL, function, "A");
	rc2 = pthread_create(&t2, NULL, function, "B");

	// You have to join threads after creation
	pthread_join(t1, NULL);
	pthread_join(t2, NULL);

	return 0;
}
```
WHEN ==COMPILING== USE `gcc -pthread -o threadProg program04.c`

==Three Threads==; the program, the first pthread, the second pthread.
every process has at least one thread.

`void*` for function: is used for flexibility so you can return anything.
`void*` for parameter: is also used for flexibility. 


## Race conditions, critical section, and mutual exclusion:
==Race Conditions== - the results depend on the timing execution of the code. (indeterministic)
==Critical Section== - When multiple threads running can result in a race condition. A critical section is a piece of code that accesses a shared variable and must not be concurrently executed by more than one thread.
==Mutual Exclusion== - This property guarantees that if one thread is executing within the critical section, the others will be prevented from doing so.

## Atomicity:
==Atomically== - when an instruction executed, it would perform the update as desired and could not be interrupted mid-instruction.

Atomically means to run ==in a unit== so the idea is that you could have a set of instructions that ==could not be stopped or interrupted==. 

