## Binary Trees

+ Acyclic and connected.
+ Rooted, directed and ordered.

Binary Tree T defined as
: T = $\emptyset$
	or T = {root, $T_{L}$, $T_{R}$}

**Tree Height**

Empty tree has height of -1, so `height` = max( height($T_{L}$), height($T_{R}$) ) + 1

**Tree Properties**

1. Full
: All nodes have either `0` or `m` children.

2. Perfect
: Every leaf node is at the same level.

3. Complete
: Perfect tree for every level except the leaves, where all leaves are pushed leftward.

Not every full tree is complete.
Not every complete tree is full.

## Binary Search Trees (BSTs)

We use BSTs because can't run binary search on Linked List

+ Height bound by n such that \\(lg(n) \leq h \leq n\\)
+ Full, Complete and/or perfect
+ `n` nodes in a Binary Tree means $n+1$ NULL pointers
+ BST has avg height of $O(lg(n))$

**Tree Analysis**

+ Best Case BST: Complete Tree
+ Worst Case BST: Linked List Tree
	- If inserting sorted list of elements, start at middle to avoid this outcome.
+ All height-based BST operations have lower bound of $\\Omega$(log(n)) time, and upper bound of $O(n)$ time
+ Min number of nodes in tree of height $h$: $log(n)$
+ Max number of nodes in tree of height $h$: $n$

**Traversals**

1. Pre/Post/In Order Traversals

	Always Left then Right. Only change where current node goes.

	+ Pre-Order: Self, L, R -- Stack (DFS)
	+ In-Order: L, Self, R
		- *Ordered list*
	+ Post-Order: L, R, Self

2. Level-Order Traversal -- Queue (BFS)

	+ Enqueue root
	+ While queue isn't empty
		- Dequeue and if element isn't NULL, print it and enqueue its children.

**Traversals vs. Searches**

A traversal visits each node exactly once.
A search visits each node until find node being searched for.

An invalid in-order traversal is one that doesn't strictly ascend.

BFS
: Visits all nodes on same level before going deeper.

DFS
: Visits leaf nodes as quickly as possible.

**Two Child Removal**

1. Find In Order Predecessor (rightmost element of left subtree)
2. Swap IOP with node
3. Delete removal node

**Run Time Analysis**

|     Operation     |  BST Avg. Case     |   BST Worst Case    |  Sorted Array  | Sorted List |
|       ----       |     ----              |    ----      |   ----         |    ----      |
|   find()         |  O(log(n))          |      O(n)     | O(log(n)) *Binary Search    |     O(n)      |
|   insert()       |  O(log(n))           | O(n)   | O(n)    |     Given: O(1), Random: O(n)      |
|   delete()       |  O(log(n))            | O(n)  | O(n)    |     Given: O(1), Random: O(n)    |
|   traverse()     |  O(n)            | O(n)  | O(n)    |     O(n)    |