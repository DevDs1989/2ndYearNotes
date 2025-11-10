---
Class:
Title: "Chinese  Remainder Theorem"
date: "03-11-2025"
Time: "09:31"
type:
  - class-notes
tags:
Related:
---
# Topic



---
# Keywords



--- 
# Notes

# Chinese Remainder Theorem — Notes for Algorithms Class

## Overview / Intuition
The Chinese Remainder Theorem (CRT) gives conditions under which a system of simultaneous congruences has a solution, and shows that when the moduli are pairwise coprime the solution is unique modulo the product of the moduli. CRT is widely used in algorithms and number-theoretic computations (e.g., big-integer arithmetic, RSA optimizations, modular FFTs, distributed/parallel computations).

---

## Statement (pairwise coprime moduli)
Let n 1, n 2, ..., nk be positive integers that are pairwise coprime (gcd (ni, nj) = 1 for i ≠ j). For any integers a 1, a 2, ..., ak, the system

X ≡ a 1 (mod n 1)  
X ≡ a 2 (mod n 2)  
...  
X ≡ ak (mod nk)

has a solution, and any two solutions are congruent modulo N = n 1 * n 2 * ... * nk. Thus there is a unique solution x modulo N.

---

## Existence and uniqueness (sketch)
- Existence: Constructive proof: build x as a linear combination of the ai with coefficients that are 1 mod ni and 0 mod nj for j ≠ i.
- Uniqueness: If x and y both satisfy all congruences, then x ≡ y (mod ni) for every i, so x−y is divisible by every ni. Since moduli are pairwise coprime, x−y is divisible by N; hence x ≡ y (mod N).

---

## Constructive algorithm (standard CRT)
Let N = ∏i ni. For each i:
- Ni = N / ni
- Find yi = (Ni)^{-1} mod ni (the modular inverse of Ni modulo ni) using extended Euclidean algorithm
- Then contribution ci = ai * yi * Ni
- Final solution: x = (∑i ci) mod N

Proof that yi exists: gcd (Ni, ni) = 1 because ni is coprime with all other moduli, so Ni and ni are coprime.

### Pseudocode
```text
CRT(a[1..k], n[1..k]):
  N = 1
  for i = 1..k:
    N = N * n[i]

  x = 0
  for i = 1..k:
    Ni = N / n[i]
    yi = modInverse(Ni, n[i])       // via extended gcd
    x = (x + a[i] * yi * Ni) % N

  return x  // unique modulo N
```

### Modular inverse (extended gcd)
To compute `modInverse(b, m)`:
- Use extended Euclidean algorithm to get u, v with u*b + v*m = gcd (b, m) = 1
- Then `u mod m` is the modular inverse.

---

## Complexity
- Extended Euclidean algorithm on numbers of size up to O (log N) takes O (log^2 N) bit operations (using schoolbook multiplication); with fast integer arithmetic replace with M (n).
- Doing this k times yields roughly O (k * log^2 N) bit complexity using naive multiplication.
- Practical performance depends strongly on representation of big integers and on k.

---

## Example
Solve:
X ≡ 2 (mod 3)  
X ≡ 3 (mod 5)  
X ≡ 2 (mod 7)

N = 3*5*7 = 105  
N 1 = 105/3 = 35, inverse of 35 mod 3 is 2 because 35≡2 (mod 3) and 2*2≡1 (mod 3)  
N 2 = 105/5 = 21, inverse of 21 mod 5 is 1 because 21≡1 (mod 5)  
N 3 = 105/7 = 15, inverse of 15 mod 7 is 1 because 15≡1 (mod 7)

X = 2 * 35 * 2 + 3 * 21 * 1 + 2 * 15 * 1  
  = 140 + 63 + 30 = 233  
X mod 105 = 233 mod 105 = 23

Check: 23 ≡ 2 (mod 3), ≡ 3 (mod 5), ≡ 2 (mod 7). So x = 23 (unique mod 105).

---

## Non-coprime moduli (general case)
If moduli are not pairwise coprime, consider system:
X ≡ a (mod m)  
X ≡ b (mod n)

A necessary and sufficient condition for a solution is:
A ≡ b (mod gcd (m, n))

If satisfied, you can merge the two congruences into one with modulus l = lcm (m, n) by solving a single congruence. The merging step uses extended gcd to express a solution; repeat pairwise to reduce k congruences to one. If a condition fails for any pair during merging, the system is inconsistent.

Simple merge algorithm for two congruences:
- Let g = gcd (m, n). If a % g != b % g then no solution.
- Otherwise find solution x 0 mod l = lcm (m, n):
  - Solve (m/g) * t ≡ (b-a)/g (mod n/g) for t (use inverse).
  - X = a + m * t (reduce mod l).

---

## Garner's algorithm (avoids big intermediate products)
Garner's algorithm computes the unique solution modulo N without directly forming very large products N or Ni. It computes coefficients ci such that:

X = c 1 + c 2*n 1 + c 3*(n 1*n 2) + ...,

Where each ci is computed iteratively using modular inverses. This is numerically convenient when you want the result in mixed-radix representation or to avoid huge integers.

High-level steps:
- Compute r[i][j] = inverse of n[i] mod n[j] for i < j
- Use iterative back-substitution to compute coefficients

Garner is especially useful when moduli fit in machine words but product N does not.

---

## Applications
- Reconstructing a large integer from its residues (big-integer arithmetic).
- RSA CRT optimization: compute mod p and mod q and combine (faster exponentiation).
- Fast polynomial arithmetic over integers via modular evaluation and CRT recombination.
- Parallel/distributed computing where different processes compute residues modulo different primes.
- FFT-based integer multiplication techniques with modular reduction.

---

## Practical tips
- Always reduce ai modulo ni first.
- When using CRT in code, be careful with overflow: use big-integer arithmetic or Garner's algorithm to keep intermediates small.
- Precompute modular inverses for many queries when moduli are fixed.

---

## Exercises
1. Solve using CRT: x ≡ 1 (mod 4), x ≡ 2 (mod 5), x ≡ 3 (mod 9).
2. Merge the congruences x ≡ 2 (mod 6) and x ≡ 5 (mod 8). Are they compatible? If yes, find the solution modulo lcm (6,8).
3. Implement CRT and Garner in your favorite language; compare runtime and memory when moduli are 32-bit primes and k = 50.
4. Show formally that if gcd (ni, nj) = 1 for all i ≠ j then gcd (Ni, ni) = 1.

---

## References / Further Reading
- Ireland & Rosen — A Classical Introduction to Modern Number Theory (CRT proof and examples).
- Vajda — Fibonacci & Lucas Numbers (applications).
- Algorithm textbooks (CLRS) — Section on number-theoretic algorithms (extended gcd, modular inverse).
- Online: Wikipedia article "Chinese remainder theorem".

---

End of notes.

---
# Work

- [ ] 

---
