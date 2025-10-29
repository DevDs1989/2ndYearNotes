---
Class: "[[Design and Analysis of Algorithms (DAA)]]"
Title: Floyd Wagshall Algo
date: 27-10-2025
Time: 09:10
type:
  - class-notes
tags:
Related:
---
# 🧭 Dijkstra’s Algorithm vs Floyd–Warshall Algorithm

## Overview

Both algorithms are used to find the **shortest paths** in a weighted graph, but they differ in purpose, approach, and efficiency.

---

## 🔹 Dijkstra’s Algorithm

**Purpose:**  
Finds the **shortest path from a single source** to all other vertices.

**Type:**  
Single-source shortest path algorithm.

**Key Features:**
- Works on **weighted graphs** with **non-negative edge weights**.  
- Follows a **greedy approach**.  
- Builds shortest paths incrementally.

**Time Complexity:**
- `O(V^2)` with adjacency matrix.  
- `O(E + V log V)` using a priority queue (with adjacency list).

**Best Used For:**
- **Sparse graphs** (few edges).  
- When only **one source node’s paths** are needed.

---

## 🔹 Floyd–Warshall Algorithm

**Purpose:**  
Finds the **shortest paths between all pairs of vertices**.

**Type:**  
All-pairs shortest path algorithm.

**Key Features:**
- Works on **weighted graphs**, even with **negative edge weights** (but **no negative cycles**).  
- Based on **dynamic programming**.  
- Iteratively updates distances through all possible intermediate vertices.

**Time Complexity:**
- `O(V^3)`

**Best Used For:**
- **Dense graphs** (many edges).  
- When **shortest paths between every pair** of nodes are required.

---

## 🔸 Comparison Table

| Feature | **Dijkstra’s Algorithm** | **Floyd–Warshall Algorithm** |
|----------|--------------------------|-------------------------------|
| **Purpose** | Shortest paths from a *single source* | Shortest paths between *all pairs* |
| **Graph Type** | Weighted (non-negative edges only) | Weighted (can handle negative edges, not cycles) |
| **Approach** | Greedy | Dynamic Programming |
| **Handles Negative Weights** | ❌ No | ✅ Yes (no negative cycles) |
| **Time Complexity** | `O(V^2)` or `O(E + V log V)` | `O(V^3)` |
| **Best For** | Sparse graphs, one source | Dense graphs, all pairs |
| **Type** | Single-source | All-pairs |

---

## 🧠 Summary

- **Use Dijkstra’s Algorithm** when you need shortest paths **from one source node** and all weights are non-negative.  
- **Use Floyd–Warshall Algorithm** when you need **all-pairs shortest paths**, especially when the graph may include **negative weights**.
 