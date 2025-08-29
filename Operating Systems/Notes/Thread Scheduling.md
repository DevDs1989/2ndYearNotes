**Class**: [[Operating Systems]]

**Title:** Thread Scheduling

**Date:** 26-08-2025

**Time:** 09:12

**Tags:**

**Related:**
# Topic

Thread Scheduling methods


---
# Keywords



--- 
# Notes

## Thread Scheduling

- Based on thread scope
	- Process Contention Scope
	- System Contention Scope
- pthread scheduling

## Thread Scope Based Scheduling
### Process Contention Scope(PCS)

- User level thread scheduling

### System Contention Scope(SCS)

- Kernel Level thread scheduling

## POSIX

- **POSIX:** Portable Operating System Interface
- Made by IEEE
-  Unifies  process execution for UNIX based operating systems
- pthread_create()
- pthread_join()

### PTHREAD scheduling 

- **PTHREAD_SCOPE_PROCESS():** -> used for PCS
- **PTHREAD_SCOPE_SYSTEM()** -> used for SCS
- `Pthrread_attr_SetScope(phtread_att_t,*attr, int scope)`
- `Pthrread_attr_SetScope(phtread_att_t,*attr, int scope)`

## Threading Issues

### Race Condition

- Occurs when two or more threads access shared data and try to change it at the same time.
- Happens due to lack of synchronization mechanisms (like mutexes, semaphores).
- Two threads compete instead of synchronizing, leading to unpredictable results or corrupted data.
- Solution: Use proper synchronization (locks, atomic variables) to prevent concurrent access.

### System Calls

- System calls by threads can lead to the process being blocked, especially if one thread is waiting for I/O or other resources.
- If a thread is blocked in a system call, other threads may also be blocked depending on implementation and how resources are shared.
- Solutions:
  - Use non-blocking system calls where possible.
  - Design threads to handle blocking gracefully, possibly by spawning additional threads or using asynchronous patterns.

### Thread Cancellation

When a thread is stopped before it finishes executing.

#### Asynchronous
- The thread is killed immediately by another thread.
- Is **not preferred** because resources may not be released properly, leading to inconsistent program state or memory leaks.

#### Deferred

- The thread periodically checks for a cancellation request and cancels itself at a safe point.
- **Preferred way** of thread cancellation, as it allows the thread to clean up resources and exit gracefully.
- Typically implemented using cancellation points (e.g., during sleep, wait, I/O operations).

### System Handling

- The system assigns equal priority to threads by default at the start.
- Can cause **misassignment of priority**, where critical threads may not get necessary CPU time, and less important threads may preempt more important ones.
- Solution:
  - Use thread priorities to manage scheduling (if supported by OS).
  - Implement custom scheduling algorithms if needed for time-critical applications.
  - Monitor and adjust priorities dynamically based on thread workload or importance.

### Thread Pool

#### What is a Thread Pool?

- A thread pool is a collection of pre-instantiated, idle threads which stand ready to execute tasks.
- Instead of creating and destroying threads for each task, threads are reused, improving performance and resource management.

### Thread Specific Data

- Happens when a thread specific data is modified depending on the variable scope of the threads and global level

# Additional Concepts

#### Deadlock

- Occurs when two or more threads are each waiting for resources held by the other, resulting in all threads being blocked indefinitely.
- Solution: Avoid circular waits, use lock ordering, and employ timeout strategies.

#### Starvation

- Happens when a thread never gets CPU time or resources because others are constantly favoured.
- Solution: Use fair scheduling algorithms and ensure all threads get a chance to execute.

#### Thread Safety

- Code is thread-safe if it functions correctly during simultaneous execution by multiple threads.
- Achieved via immutability, synchronisation mechanisms, and careful design.

#### Context Switching

- The process of storing and restoring thread state when switching between threads.
- Excessive context switching can reduce performance.
---
# Work

- [ ] 

---
