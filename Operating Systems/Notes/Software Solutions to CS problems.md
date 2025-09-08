**Class**: [[Operating Systems]]

**Title:** Software Solutions to CS problems

**Date:** 03-09-2025

**Time:** 09:07

**Tags:**

**Related:**
# Topic



---
# Keywords

- Dekker's Algorithm

--- 
# Notes

## Dekker's Algo
### First Version
- Shared thread: Signal turn -> priority
- Checks if turn value belongs to the current process and if not true it holds itself and runs the process that has its turn 

**Process 0**
```python
while turn != 0:
	do nothing #P1 is happening
CRITICAL SECTION #P0 is happening
turn = 1
```

**Process 1**
```python
while turn != 1:
	do nothing # P0 is happening
CRITICAL SECTION #P1 is happening
turn = 0
```

### Second Version
- Uses Boolean flags for each process
- flag updates while  entry
- **Can violate mutual exclusion**

```python
flag[0] = true or false
flag[1] = true or false

#Process 0
while flag[1]:
	do nothing
flag[0] = true
CRITICAL SECTION
flag[0] = flase

#Process 1
while flag[0]:
	do nothing
flag[1] = true
CRITICAL SECTION
flag[0] = true

```

### Third Version
- Generates flag before entry and exit
- sets its own flag to true before starting
- still check for other processes before entering critical section
- If 2 processes enter critical section at the same time, **deadlock** happens.

```python
flag[0] = true
while flag[1]:
	do nothing
CRITICAL SECTION
flag[0] = false 
```

### Fourth version
- Uses delay after entry to stop deadlock 
- Can cause **starvation** again due to higher priority mismanagement

```python
#Process 0
flag[0] = true
while flag[1]:
	flag[0] = false
	delay
flag[0] = true
CRITICAL SECTION
flag[0] = flase
```

### Fifth Version
- Final version of Dekker's Algorithm
- Uses both turn and flags
- `turn -> priority`
- `flag -> intent`
- Solves bounded condition, mutual exclusion, progress
```c++
boolean flag[2];
int turn;
void PO(){
	while(true){
	flag[0] = true
	if(turn == 1){
		flag[0] = false
		}
	while(turn == 1){
		do nothing
		}
	flag[0] = true
	CRITICAL SECTION
	}
turn = 1
}
void P1(){
	while(true){
	flag[1] = true
	if(turn == 0){
		flag[1] = false
		}
	while(turn == 0){
		do nothing
		}
	flag[1] = true
	CRITICAL SECTION
	}
	turn = 0
}
	
int main(){
	flag[0] = false;
	flag[1] = false;
	turn  = 1;
	parbegin(P0, P1);

}
```

---
# Work

- [ ] 

---
