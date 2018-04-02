**Arrays**

Given index, $O(1)$ access. Cache optimized
1. Sorted Array -- Efficient find (Binary Search), inefficient insert/remove.
1. Unsorted Array -- Inefficient find ($O(n)$), efficient insert/remove

**List ADT**

There are two implementation strategies for a List.

1. Linked List-based Implementation
	+ insertAtFront in $O(1)$ time if head pointer exists, and same for back if tail pointer exists.
2. Array-based Implementation
	+ insertAtFront in $O(n)$ because all the elements need to be shifted back.
	+ Allocate extra space on the front and back of the array for front/back inserts and keep pointer to next "front" and "back" space. "Circular" array.
	+ Array Resize by doubling array capacity and copying data over. $O(n)$ every $n$ times for amortized $O(1)$ per insert.

	|     Methods     |  Linked List     |   Array    |
	|      ----       |     ----         |    ----      |
	| push/pop Front()     |  `O(1)`   |     `O(1)` *due to extra space left     |
	| insert/remove NotFront()   |  `O(1)` *IF have pointer to prev | `O(n)` *need to copy data |
	| insert/remove Arbitrary()   | `O(n)` | `O(n)` *need to copy data |

**Stack ADT**

Last In, First Out

|     Methods     |  Linked List     |   Array    |
|      ----       |     ----         |    ----      |
| push()     |  `O(1)`   |     `O(1)`     |
| pop()   |  `O(1)`  | `O(1)`  |

**Queue ADT**

First In, First Out

|     Methods     |  Linked List     |   Array    |
|      ----       |     ----         |    ----      |
| enqueue()     |  `O(1)`   |     Amortized `O(1)`     |
| dequeue()   |  `O(1)`  | `O(1)`  |

**Important Takeaways**

O(1) `push() / enqueue()` and `pop() / dequeue()` operations with both Array and Linked List implementation for Stacks and Queues.
