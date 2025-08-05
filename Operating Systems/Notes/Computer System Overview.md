**Class**: Operating Systems

**Title:** Computer System Overview

**Date:** 05-08-2025

**Time:** 09:10


# Topic



---
# Keywords

- **Processor**
- **IO Module**
- **Main Memory**
- **System Bus**

--- 
# Notes


```mermaid
graph TD
    A[CPU] --> B[Bus]
    B --> C[Memory]

    subgraph LR_Group[ALU & Registers]
        direction LR
        D[ALU] --> E[Registers]
    end

    A --> D
    A --> E

```

### Instruction Cycle
```mermaid
flowchart LR;
A[Start] -->|Fetch Cycle| B[Next]
B -->|Execution Cycle| C[Execute Instruction]
C --> D[Halt]
```

### Instruction Execution
1. Processor - Memory
2. Processor - I/O
3. Data Processing
4. Control

---
# Work

- [ ] 

---
