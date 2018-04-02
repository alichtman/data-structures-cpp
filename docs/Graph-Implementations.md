Simple Graph
: Graph with no self loops or multi-edges.

Incident Edges
: Edges coming off a node. `Degree(v)` is the number of Incident Edges.

Number of Vertices: `n`
Number of Edges: `m`

Min num edges in Unconnected Graph = `0`
Min num edges in Minimally Connnected Graph = $n - 1$

Max num edges in Simple Graph = $\frac{n \cdot (n-1)}{2}$
Max num edges in Not Simple Graph = $\infty$ because self edges are allowed.

Relationship between degree of graph and edges: $degree = 2m$

**Graph Implementations**

1. Edge List

	An array of pairs of vertices (Edges). If edges have weights, add either a third element to the array or more information to the object.

	The total space for an edge list is Θ(E).

	To find if the graph contains a particular edge, we have to search through the entire edge list, so $O(|E|)$.

	Example : `[[0,1], [0,6], [0,8], [1,4], [1,6], [1,9], [2,4], [2,6], [3,4], [3,5]]`

	| Operation | Run Time |
	| ---	|	---	|
	|	insertVertex(K key)	|	$O(1)$	|
	|	removeVertex(K key)	|	$O(m)$	|
	|	areAdjacent(Vertex v1, Vertex v2)	|	$O(m)$	|
	|	incidentEdges(Vertex v)	|	$O(m)$	|

2. **Adjacency Matrix**

	v = Number of vertices $(|V|)$.

	The matrix is `v x v`. Number of edges is irrelevant.

	An adjacency matrix can determine whether two vertices are adjacent in $O(1)$ time by looking at the corresponding entry.

	`matrix[i][j]` is 1 if the edge `(i,j)` exists in the graph, otherwise it's 0.

	The diagonal should be all 0s if the graph is simple (no self edges).

	For an undirected graph, adjacency matrix is symmetric.
	For a directed graph, adjacency matrix is not necessarily symmetric.

	It takes $Θ(V2)$ space, even if the graph is sparse.

	Example:

		 [0, 1, 0, 0, 0, 0]
		 [1, 0, 0, 0, 1, 0]
		 [0, 0, 0, 0, 1, 0]
		 [0, 0, 0, 0, 1, 1]
		 [0, 1, 1, 1, 0, 1]
		 [0, 0, 0, 1, 1, 0]

	| Operation | Run Time  |
	| ---	|	---	|
	|	insertVertex(K key)	|	Amortized $O(n)*$ (?)	|
	|	removeVertex(K key)	|	$O(n)$	|
	|	areAdjacent(Vertex v1, Vertex v2)	|	O(1)	|
	|	incidentEdges(Vertex v)	|	$O(n)$	|

3. **Adjacency List**

	![adj-list](https://github.com/alichtman/data-structures-cpp/blob/master/images/adjList.png)

	Combines adjacency matrices with edge lists.

	For each vertex, store an array of adjacenct vertices. Max size of array is $n - 1$.

	$2m$ list nodes. (?)

	Example:


	| Operation | Run Time  |
	| ---	|	---	|
	|	insertVertex(K key)	|	O(1)	|
	|	removeVertex(K key)	|	O(deg(v))	|
	|	areAdjacent(Vertex v1, Vertex v2)	|	O( min(deg(v1), deg(v2)) )	|
	|	incidentEdges(Vertex v)	|	O(deg(v))	|
