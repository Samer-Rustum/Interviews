# RTOS

A **Real-Time Operating System (RTOS)** provides functionality, data types, and structure that can be used to better scale and maintain firmware. It can accept and process a large number of events (usually external to the computer system).

It includes **multi-tasking** where "chunks of execution" are separated into tasks that can run "concurrently".

RTOS ensure timing deadlines are met.

### Benefits of RTOS

RTOSs are used when large amounts of events need to occur and timing is critical. This can be seen on wireless stacks like bluetooth or wifi where the device needs to respond quickly to the network.

They are also usually more suited for larger firmware teams as each member can work on their task knowing that each task can run concurrently.
# Tasks

A set of program instructions loaded into memory.

In the case of multi-threaded processors, a task can be assigned to each thread, allowing for true concurrent execution. For single-threaded processors, the processor time must divided up amongst all the tasks. Tasks with higher priority can execute first or have more processor time allocated.

Interrupts work normally as long as they have a higher priority than the rest of the tasks.

# Scheduler

![Scheduler image](https://user-images.githubusercontent.com/43387528/231057559-c6af929a-c09d-4e26-935c-ed02bbe001a4.png)

### Task States
![Task States](https://user-images.githubusercontent.com/43387528/231058868-966f3067-69df-4eaf-8eda-1b50091f4d9f.png)

A task can exist in one of the following states:
1. Running: When a task is actually executing. On a single-core processor, there can only be one running task.
2. Ready: Able to execute (!(Blocked || Suspended)) but are not current executing because of a task with a higher or equal priority.
3. Blocked: Waiting for a temporal or external event (eg. delay of 50ms). Cannot enter running state. Have a time-out period, after wich the task will be timeout, and be unblocked, even if the event the task was waiting for has not occured.
4. Suspended: Similar to blocked but does not have a timeout period. Tasks enter or exit the Suspended state when explicitly commanded to do so.

### Context Switching

When switching from one task to the next, the scheduler has the job of remembering exactly where the task left off and all of its working variables. The data saved is the **context**.

# Memory

### FreeRTOS example

When a new task is created, it is assigned a portion of the memory from the heap. That portion is divided into a a TCB (Task Control Block) and a stack unique to the task.

The TCB is a struct that keeps track of vital information of the task like priority level.

# Thread Safety

If we want to save a 64-bit value to memory with a word length of 32 bits. This requires 2 write operations and 2 cycles. After the first write operation, another task interrupts and reads that 64 bit value from memory. We essentially cannot guarantee that a variable will be written or read without being interrupted by another task.

There are a few ways to solve this issue.
### 1. Queue

A FIFO Queue that allows passing variables between Tasks.
![image](https://user-images.githubusercontent.com/43387528/231063658-984cf6cc-3f81-4eb1-a4f6-dc75d0143fbc.png)
![image](https://user-images.githubusercontent.com/43387528/231063677-47cb7c43-a138-4166-ac59-6343d641df7c.png)

### 2. Mutex

A mutex is a mutual exclusion lock. It allows only one thread to access the data at a specificed location in memory. Are useful for dealing with race conditions.

### 3. Semaphore

A semaphore is similar to a mutex, but it allows multiple tasks the access the same piece of data. The semaphore only allows for a certain number of tasks to access the critical data concurrently.

This is not the usual use of a semaphore, however. Semaphores are used as to signal to other tasks that some shared resource is ready to be read. One task increases the semaphore and another decreases it.
