
**Class**:  [[Elements of AI]]

**Title:** Quantification

**Date:** 11-09-2025

**Time:** 09:12

**Tags:** #AI 

**Related:**
# Topic

---

# Keywords

- Quantification
    - Universal
    - Existential

--- 
# Notes

## Quantification

Quantification is a logical process used to create propositions from propositional functions (predicates). It allows us to generalize statements over a domain of discourse.

There are two main types of quantification:

### Universal Quantification

- States that a predicate is true for every element in the domain.
- Notation: $\forall x \, P(x)$
- Read as: "For all $x$, $P(x)$" or "For every $x$, $P(x)$".  
- If there is even a single $x$ for which $P(x)$ is false, the entire statement is false. This $x$ is called a **counterexample**.
- Example:  
  "Every student passed the exam" can be written as  
  $\forall x \, (\text{Student}(x) \implies \text{Passed}(x))$

### Existential Quantification

- States that there is at least one element in the domain for which the predicate is true.
- Notation: $\exists x \, P(x)$
- Read as: "There exists an $x$ such that $P(x)$" or "For some $x$, $P(x)$".
- If $P(x)$ is false for all $x$, then the statement is false.
- Example:  
  "Some student passed the exam" can be written as  
  $\exists x \, (\text{Student}(x) \land \text{Passed}(x))$

#### Quick Reference Table

| Statement            | True when...                               | False when...                                |
|----------------------|--------------------------------------------|----------------------------------------------|
| $\forall x \, P(x)$  | $P(x)$ is true for all $x$                 | There is at least one $x$ where $P(x)$ false |
| $\exists x \, P(x)$  | There is at least one $x$ where $P(x)$ true| $P(x)$ is false for all $x$                  |

---

### De Morgan's Laws for Quantifiers

| Negation                  | Equivalent Statement        | Why true                                      | Why false                                   |
|---------------------------|----------------------------|-----------------------------------------------|---------------------------------------------|
| $\neg \exists x \, P(x)$  | $\forall x \, \neg P(x)$   | $P(x)$ is false for every $x$                 | There is at least one $x$ where $P(x)$ true |
| $\neg \forall x \, P(x)$  | $\exists x \, \neg P(x)$   | There is at least one $x$ where $P(x)$ false  | $P(x)$ is true for every $x$                |

---

### Examples

#### Example 1: All P's are Q's
$$
\forall x \, (P(x) \implies Q(x))
$$

#### Example 2: Some Men are Clever
$$
\exists x \, (\text{Man}(x) \land \text{Clever}(x))
$$

---

# Work


---