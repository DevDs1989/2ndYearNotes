
**Class**: [[DBMS]]

**Title:** RC and RA

**Date:** 08-09-2025

**Time:** 11:40

**Tags:** 

**Related:**
# Topic


# Keywords

- Relational Calculus (RC)
- Relational Algebra (RA)
- Set Operations
- Union
- Intersection
- Difference
- Selection ($\sigma$)
- Projection ($\pi$)
- Tuple Relational Calculus (TRC)
- Domain Relational Calculus (DRC)
- Cartesian Product
- Rename ($\rho$)

--- 
# Notes

## Introduction

Relational Algebra (RA) and Relational Calculus (RC) are two formal languages for manipulating and querying data stored in relational databases.

- **Relational Algebra**: A procedural query language that specifies a sequence of operations to retrieve required data.
- **Relational Calculus**: A non-procedural query language that uses mathematical predicate calculus to describe what data to retrieve.

---

## Relational Algebra: Basic Operations

1. **Selection ($\sigma$):**
   - Selects rows (tuples) that satisfy a given predicate.
   - Example: $\sigma_{\text{age} > 17}(\text{Student})$

2. **Projection ($\pi$):**
   - Selects columns (attributes).
   - Example: $\pi_{\text{Name}}(\text{Student})$

3. **Renaming ($\rho$):**
   - Renames the output relation or its attributes.
   - Example: $\rho_{\text{S}}(\text{Student})$ renames Student to S.

4. **Cartesian Product ($\times$):**
   - Combines tuples from two relations in all possible ways.
   - Example: $\text{R} \times \text{S}$

5. **Set Operations:**
   - **Union ($\cup$)**
   - **Intersection ($\cap$)**
   - **Difference ($-$)**

---

## More on Set Operations

### Union ($\cup$)
- Combines all tuples from two relations, removing duplicates.
- Both relations must be union compatible (same number and type of attributes).

### Intersection ($\cap$)
- Returns tuples present in both relations.
- Also requires union compatibility.

### Difference ($-$)
- Returns tuples present in the first relation but not in the second.
- Also requires union compatibility.

### Cartesian Product ($\times$)
- Returns all possible combinations of tuples from two relations.
- Used as a step in join operations.

---

### Join Operations

1. **Theta Join ($\bowtie_\theta$):**
   - Combines tuples from two relations based on a condition $\theta$.
   - Example: $\text{R} \bowtie_{R.A = S.B} \text{S}$

2. **Natural Join ($\bowtie$):**
   - Joins on all attributes with the same name in both relations.

3. **Equi Join:**
   - A theta join using only equality ($=$) as the condition.

4. **Outer Joins:**
   - Includes tuples from one or both relations that do not have matching tuples in the other relation (LEFT, RIGHT, FULL OUTER JOIN).

---

## Relational Calculus

### Types

- **Tuple Relational Calculus (TRC):**
  - Focuses on describing the tuples to be selected.
  - Format: $\{ t \mid P(t) \}$, where $t$ is a tuple variable and $P(t)$ is a predicate.

- **Domain Relational Calculus (DRC):**
  - Focuses on attributes (domains) of the tuples.
  - Format: $\{ \langle x_1, x_2, ..., x_n \rangle \mid P(x_1, x_2, ..., x_n) \}$

### Safety of Expressions
- Only "safe" expressions (those that produce a finite number of results) are allowed in RC.

---

## Example Queries

### Relational Algebra Example

Retrieve names of students older than 17 with SapID = 2:
$$
\pi_{\text{Name}}(\sigma_{\text{age} > 17 \ \&\ \text{SapID} = 2}(\text{Student}))
$$

### Tuple Relational Calculus Example

$\{ t.\text{Name} \mid t \in \text{Student} \land t.\text{age} > 17 \land t.\text{SapID} = 2 \}$

### Domain Relational Calculus Example

$\{ N \mid \exists A, S ( (N, A, S) \in \text{Student} \land A > 17 \land S = 2 ) \}$

---

## Example Problem Solution

**Given:**  
- 30 like tea ($|T|$)
- 25 like coffee ($|C|$)
- 10 like both ($|T \cap C|$)
- Total students = 50

**Formulas:**
- $|T \cup C| = |T| + |C| - |T \cap C| = 30 + 25 - 10 = 45$
- Only tea: $|T| - |T \cap C| = 20$
- Neither tea nor coffee: $50 - |T \cup C| = 5$

---

## Additional Notes

- **Difference between RC and RA:**
    - RA: Specifies how to obtain the result (procedural).
    - RC: Specifies what you want (non-procedural).

- **Practical Use:**  
    - SQL is based on both RA and RC concepts.

- **Set operations in SQL may not always remove duplicates unless the keyword ALL is omitted.**

---

# Work

- [ ] Practice more set operation and join problems.
- [ ] Write queries in RA, TRC, DRC, and SQL for the same requirement.
- [ ] Understand safety in relational calculus.
- [ ] Explore outer joins and their use cases.

---