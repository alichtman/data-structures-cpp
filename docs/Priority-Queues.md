| Implementation	| insert() Run Time	| removeMin() Run Time |
|	--- 			|	--- 			|	--- 				|
|	Unsorted Array	|	Amortized O(1) -> insert at end, resize when full	|	O(n)		|
|	Unsorted List	|	O(1)			|					|	O(n)
|	Sorted Array	|	O(log(n)) + O(n) -> Binary Search + Shift elements	|	O(1) -> Pop from front/back	|
|	Sorted List		|	O(n) *must traverse, no binary search				|	O(1) -> Pop from front/back				|


**Min-Heaps**

+ Min Heaps are not BSTs, but they are Binary Trees. Descendants are all larger than root.
+ Complete tree.
+ No ordering between subtrees.

**Calculating Indices (1-Indexed)**

+ Left Child: `2 * curr_index`
+ Right Child: `2 * curr_index + 1`
+ Parent: `floor[curr_index/2]`

**Implementation Details**

+ Insert
	- Push the new value to the back of the vector `vector.push_back(val);`
	- Call HeapifyUp() on the last element of the vector `HeapifyUp(vector.size() - 1)`

+ Remove
	- Save root node in temp var
	- Swap root and last element `std::swap(vector[getRoot()], vector[vector.size() - 1]);`
	- Pop the last element `vector.pop_back()`
	- Call `HeapifyDown()` on the root `HeapifyDown(getRoot())`

+ HeapifyUp()

+ HeapifyDown()

+ BuildHeap()

**Run Time**

|     Methods     |  Description     |   Running Time    |
|      ----       |     ----         |    ----      |
| heapifyUp()     |  Called on last element after insertion at end of list   |     O(log n)      |
| heapifyDown()   |  Called on root index after remove() call b/c root swapped with last element in remove() | O(log n) |
| buildHeap()   |  Called on array to build heap | O(n) |


+ Build Heap from Unsorted Array
	- Walk through array from end to front and call HeapifyDown() on each element.

+ A heap can be represented as a `perfect` or a `complete` tree.
	- Perfect: Every level is fully filled. All leaves are on the same level.
	- Complete: Every non-leaf level is fully filled, and all leaf nodes are pushed to the left.
	- A heap is always complete, but it is not always perfect.