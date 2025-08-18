**Class**: [[Design and Analysis of Algorithms (DAA)]]

**Title:** Asymptotic Notation

**Date:** 14-08-2025

**Time:** 08:26

**Tags:** #DAA

**Related:**
# Topic



---
# Keywords

- Asymptotic Notation
- Function


--- 
# Notes

##  Asymptotic Notation

Formal way of notation to speak about functions and classify them for an algorithm

### Asymptotic Analysis

#### Two kinds of features of class notation 

1. Functions should belong to the same class
	1. Constant multipliers should be ignored
2. Gives more importance to behaviour as N -> ∞

### Theta Notation

- f, g: non negative function of non negative arguments
- θ(g): {f | f is a non negative function such that there exists constants C<sub>1</sub>, C<sub>2</sub> , n  }
	- where C<sub>1</sub> g(n) <= f(n) <= C<sub>2</sub> g(n) for n <= n<sub>0</sub> 

θ(g) is the intersection of 0(g) and Ω(g)
#### Property

- f ∈ θ(g<sub>1</sub>), h ∈ θ(g<sub>2</sub>)
	- f + h ∈ θ(g<sub>1</sub> + g<sub>2</sub>)
	- g<sub>1</sub> + g<sub>2</sub> = g
	- f + h ∈ θ(g)

### Big O Notation

- O(g) { f | is a non negative function and there exists C<sub>2</sub>, n<sub>0</sub> }
	- where f(n) <= C<sub>2</sub>g(n) for n >= n<sub>0</sub>
	- 


### Omega(Ω) Notation


- Ω(g) { f | is a non negative function and there exists C<sub>1</sub>, n<sub>0</sub> }
	- where C<sub>1</sub>g(n) <= f(n) for n >= n<sub>0</sub>

---
# Work

- [ ] 

---
