# Deadlock & Deadlock Prevention

## What is Deadlock?

A **deadlock** is a situation in operating systems and concurrent programming where two or more processes (or threads) are unable to proceed with their execution because each is waiting for another to release a resource. As a result, none of the processes can finish, and the system becomes stuck in an infinite waiting state.

### Real-life Analogy

Imagine two cars at a narrow bridge from opposite sides, both refusing to back up so the other can pass. Both are stuck, neither moves—this is a deadlock!

---

## Deadlock Characteristics

Deadlock can only occur if the following **four Coffman conditions** are met simultaneously:

1. **Mutual Exclusion**  
   - At least one resource must be held in a non-sharable mode (only one process at a time can use the resource).
   - Example: A printer cannot be shared between two print jobs at the same time.

2. **Hold and Wait**  
   - A process is holding at least one resource and is waiting to acquire additional resources held by other processes.
   - Example: Process P 1 holds Resource R 1 and requests R 2, which is held by process P 2.

3. **No Preemption**  
   - Resources cannot be forcibly taken away from a process; they can only be released voluntarily.
   - Example: If process P 1 holds R 1, we cannot forcibly take R 1 from P 1 to give to P 2.

4. **Circular Wait**  
   - There exists a set of processes {P 1, P 2, ..., Pn} such that P 1 is waiting for a resource held by P 2, P 2 is waiting for a resource held by P 3, ..., Pn is waiting for a resource held by P 1, forming a circular chain.

---

## Deadlock Example

Consider two processes and two resources:

- **Process P 1** holds **Resource R 1**, waits for **Resource R 2**.
- **Process P 2** holds **Resource R 2**, waits for **Resource R 1**.

Both processes are waiting for each other to release a resource. Neither can proceed, causing a deadlock.

#### Resource Allocation Graph

- Nodes: Processes (circles) and Resources (squares)
- Edges: Request (process → resource) and assignment (resource → process)
- A cycle in this graph indicates a possible deadlock.

---

## Handling Deadlocks

There are **four main strategies** for dealing with deadlocks:

1. **Deadlock Prevention**: Prevent deadlocks by ensuring that at least one of the Coffman conditions cannot occur.
2. **Deadlock Avoidance**: Dynamically examine resource-allocation state to ensure a system will never enter a deadlocked state (e.g., Banker's Algorithm).
3. **Deadlock Detection and Recovery**: Allow deadlocks to occur, detect them, and recover (e.g., by terminating or restarting processes).
4. **Ignore Deadlock**: In some systems (like UNIX), deadlocks are ignored as their occurrence is rare.

---

## Deadlock Prevention

**Deadlock prevention** involves designing the system so that at least one of the necessary conditions for deadlock never occurs.

### Techniques

#### 1. **Mutual Exclusion**
- Make resources sharable whenever possible.
- Not practical for all resources (e.g., printers, files).

#### 2. **Hold and Wait**
- Require processes to request all needed resources at once, before execution begins.
- If resources are not available, the process waits and releases any held resources.
- Drawback: Can cause poor resource utilization and starvation.

#### 3. **No Preemption**
- If a process requests a resource and is denied, it must release all currently held resources.
- The process can try again later.
- Used for resources where preemption is possible (e.g., CPU).

#### 4. **Circular Wait**
- Impose a linear ordering of resource types.
- Processes must request resources in increasing order of enumeration.
- Prevents circular chains, thus circular wait cannot occur.

---

## Deadlock Avoidance

- Requires knowledge of future process requests.
- **Banker's Algorithm**: The system checks each resource allocation request to see if granting it will leave the system in a safe state.

---

## Deadlock Detection & Recovery

If deadlocks are not prevented or avoided, the system can:

### Detection
- Periodically check for cycles in the resource allocation graph.
- For single resource instances, simple cycle detection suffices.
- For multiple instances, use algorithms similar to Banker's Algorithm.
- Resource Preemption: 
	- Select Victim: Find the process that is causing deadlock
	- Roll Back: Restart the process
	- Starvation: Make sure there is no starvationd

### Recovery
- **Terminate processes**: Kill one or more processes in the deadlock cycle.
- **Resource preemption**: Take resources away from some processes and give to others.
- **Rollback**: Restore processes to a safe state before deadlock.

---

## Starvation vs Deadlock

- **Starvation**: A process never gets the resources it needs because other processes are always prioritized.
- **Deadlock**: All involved processes are permanently blocked.

---

## Summary Table

| Strategy          | Description                                                    | Pros                       | Cons                              |
|-------------------|---------------------------------------------------------------|----------------------------|-----------------------------------|
| Prevention        | Eliminate one Coffman condition                               | Simple concept             | May reduce system efficiency      |
| Avoidance         | Careful resource allocation (Banker's Algorithm)               | Can be very safe           | Requires knowledge of future      |
| Detection/Recovery| Allow deadlock, then detect and recover                       | Flexible                   | May require process termination   |
| Ignore            | Do nothing                                                    | Simple                     | Risk of system hang               |

---

## Tags

#os #deadlock #concurrency #process #notes
