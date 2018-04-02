+ Used for *membership lookups* or for *seeing if two elems are part of same set*. (Graphs, mazes, path generation...)
+ Unordered, but structured.
+ Each element can be in one and only one set.

**UpTrees**

Disjoint Sets are commonly implemented with UpTrees. If an array is given and there are **negative numbers** in the array, it's probably an UpTree.

| Functions |  Description | Run Time |
| ----      |     ----     |  ----    |
| makeSet() |  Inserts n elements into the set   |    O(n)      |
| union()   |  Combines two sets  |   O(log *n)   **OR**  O(1)  *--see below--*  |
| find()    |  Finds the representative element of the set    |    O(log* n)  -> Iterated log (kinda O(1))    |

The ideal UpTree is a single root node with every other node being a direct child.

An array of UpTrees is like an equivalence class. (?)

No way to efficiently find all elements in one set, however, can efficiently check if two elements are in the same set.

**Set Unions**

Always union with roots of the trees. If union is called on a non-root node, call `find(node)` to get the root of the tree, then union with that.

1. Union by Height
	+ Store `(-1 * height) - 1` in root nodes
	+ Attach the smaller tree to the taller tree by pointing the small root to the large root
	+ Only update larger root value if trees are the same height. Literally just subtract one.

2. Union by Size
	+ Store `(-1 * num_nodes_in_tree)` in root nodes
	+ Attach the smaller tree to the taller tree by pointing the small root to the large root
	+ Save the small root value and add it to the value of the large root

**Union Run Time**

Changes based on whether or not we're given a representative element of the set.

+ If not given representative element, need to call `find(elem)` before you can union, so $O(log* n)$
+ If given representative element, can union in $O(1)$ time.

**Path Compression**

+ Always done in a `find()` call, and makes the next `find(elem)` call more efficient
+ Shortens the distance of every node on the path between `find(elem)` and the root node