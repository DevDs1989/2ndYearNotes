---
Class: "[[Design and Analysis of Algorithms (DAA)]]"
Title: Greedy Algorithms
date: 15-09-2025
Time: 09:29
type:
  - class-notes
tags:
  - DAA
  - GreedyAlgorithm
Related:
---
# Topic



---
# Keywords



--- 
# Notes

## Huffman encoding
### Algorithm
- Input: A set of characters and their frequencies
- Output: A binary tree representing the optimal prefix-free encoding of the characters
- Steps:
	1. Create a priority queue (min-heap) and insert all characters with their frequencies.
	2. While there is more than one node in the queue:
		 - Extract the two nodes with the smallest frequencies.
		 - Create a new internal node with these two nodes as children and frequency equal to the sum of their frequencies.
		 - Insert the new node back into the priority queue.
	3. The remaining node is the root of the Huffman tree.
	4. Assign binary codes to each character by traversing the tree (left edge = 0, right edge = 1).


### Question

> [!QUESTION] Question 1
> Write the number of bits required of huffman encoding of the given message and find the avg bits required to represent a character
> `aa bbb a bbb ccc ddd eee ccc eee dd eee`


---
# Work

- [ ] 

---
