## B-Trees

+ Use for large data sets. Minimizes number of disk seeks. Chunks data for better caching.
+ B-trees can be expensive if frequently modified
+ Self-balancing and sorted

**B-Tree of order m**

+ All internal nodes have one more child than key
+ All leaves are on the same level, and hold no more than $m-1$ keys
+ When a node has `m` key, you split it into two nodes, and push the median value to the node above.
+ Binary Search to Insert
+ All non root internal nodes have `[ceil(m/2), m]` children.
+ Root can be a leaf or have between 2 and m children.
+ All keys are sorted within a node

**B-Tree Upper and Lower Bounds**

1. Max Num Keys in Tree : $m^{h+1} - 1$
2. Min Num Keys in Tree : `2 ceil[m/2]^h - 1` -> $2^{kh + 1} - 1$

**Time Complexity**

|     B-Tree Operation/Property     |  Run Time     |
|       ----       |     ----     |
|   Search Through Single Node         |  $O(log (m))$  |
|   height       |  $O(log_m(n))$ |
|   find()       |  `height * Search`  |
|   insert()     |  Same runtime as `find()` |

## k-D Trees

+ CAN NOT USE FOR DICTIONARY because can't insert or remove elements.
+ "Think about how a K-D tree is created. We have to know information about all of the nodes that will eventually be in our tree so we can find the median and medians of the subarrays. Now that we have created our tree, we try to add in a new node. This could potentially change which node is our median, meaning we'd have to reconstruct the entire tree which is not efficient. Same with removals"

**Constructor**

+ Quickselect allowed us to find the k-th smallest element
+ Partition actually does the swapping

**Run Time**

+ Worst Case Find Nearest Neighbor : $O(n)$
+ Average Case Find Nearest Neighbor : $O(log n)$