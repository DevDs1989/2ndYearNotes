
**Class**: [[Elements of AI]]

**Title:** Predicates

**Date:** 09-09-2025

**Time:** 08:48

**Tags:** 

**Related:**
# Topic


--- 
# Keywords

- Predicate
- Subject
- Propositional function
- Truth value
- Domain

--- 
# Notes

## Predicates

A **predicate** is a statement or function that contains variables and becomes a proposition (a statement that is either true or false) when specific values are assigned to those variables.

### Structure of a Predicate Statement

Consider a statement $x > \phi$:
- The **subject part** is the variable itself (here, $x$).
- The **predicate part** is the condition or property being asserted about the variable (here, "$>$ $\phi$").
- When we assign a value to $x$, the predicate becomes a specific proposition, which can be evaluated as true or false.

#### Example

- Predicate: $P(x): x > 3$
    - $P(2): 2 > 3$ (False)
    - $P(5): 5 > 3$ (True)

### Predicate as a Propositional Function

- A predicate can be seen as a **propositional function**: it takes a variable as input and outputs a proposition.
- Notation: $P(x)$, where $P$ is the predicate and $x$ is the subject variable.

### Domain of Discourse

- The **domain of discourse** specifies the set of values that the variable can take.
- Example: If $x$ is an integer, then we only consider integer values for $x$.

### Multiple Variables

- Predicates can have more than one variable.
    - Example: $Q(x, y): x + y = 10$
        - $Q(5, 5): 5 + 5 = 10$ (True)
        - $Q(3, 6): 3 + 6 = 10$ (False)

### Conversion to Propositions

- When all variables in a predicate are replaced with specific values from the domain, it becomes a **proposition** (statement with a definite truth value).
- Example: $P(x): x$ is a prime number
    - $P(2)$ is True
    - $P(4)$ is False

### Use in Logic

- Predicates are used along with quantifiers (universal $\forall$, existential $\exists$) to make general statements about sets of objects.

---

# Work

- [ ] Review more examples of predicates with different domains.
- [ ] Practice writing predicates for various properties.
- [ ] Explore how predicates form the basis for quantified statements.

---