**Graph BFS/DFS**

Both BFS and DFS have optimal run times of $O(n + m)$.

For a DFS, just switch the Queue to a Stack.

BFS -- "CROSS"
DFS -- "BACK"

```cpp
void initBFS(Graoh g_) {
	// Set all vertex labels to "UNEXPLORED"
	for (auto v : g_.getVertices()) {
		g_.setVertexLabel(v, "UNEXPLORED");
	}

	// Set all edge labels to "UNEXPLORED"
	for (auto e : g_.getEdges()) {
		g_.setEdgeLabel(e, "UNEXPLORED");
	}

	// Runs BFS on all vertices
	for (auto v : g_.getVertices()) {
		if (g_.getLabel(v) == "UNEXPLORED") {
			BFS(g_, v);
		}
	}
}

void BFS(Graph g_, Vertex v) {
	Queue<Vertex> q;
	g_.setLabel(v, "EXPLORED");
	q.push(v);

	while (! q.empty()) {
		Vertex next = q.front();
		q.pop();

		for (auto adjV : g_.getAdjacentVertices(next)) {
			if (g_.getLabel(adjV) == "UNEXPLORED") {
				g_.setLabel(next, adjV, "DISCOVERY");
				q.push(adjV);
			} else g_.setLabel(next, adjV, "BACK");
		}
	}
}
```


##### Spanning Trees and Minimum Spanning Trees

Spanning Tree
: Every possible vertex in G is connected with minimum number of edges. Connected and acyclic.

Minimum Spanning Tree
: Spanning tree with the minimal total edge weights. Has $n-1$ edges.

Partition Property
: If there's an edge of minimum weight across the partition, it's a part of the MST.

To run MST algorithm, underlying graph must be connected. So, $m \geq n + c$.

Fibionacci Heap
: Decreases value of key while maintaining heap property in Amortized $O(1)$ time.

Negative weight cycles *break **everything***.

Both Kruskal and Prim's run in $O(m log(n))$

1. Kruskal's Algorithm (MST) -- Next lowest weight edge until MST formed
	![Kruskal](https://github.com/alichtman/data-structures-cpp/blob/master/images/Kruskal.jpg)
	1. Choose the shortest edge
	2. Choose the next lowest weighted edge on the graph, anywhere, that wouldn't create a cycle. Do this over and over until every vertex is in the tree.


| Priority Queue Implementation | Total Run Time |
| ---	| ---	|
| Heap	|	$O(n + m) + O(mlog(n))$ |
| Sorted Array	| $O(n + mlog(n)) + O(m)$	|


```cpp
void KruskalMST(Graph& graph) {
	// Get a list of all edges in the graph and sort them by increasing weight.
	queue<Edge> queue;
	std::vector<Edge> edges = graph.getEdges();
	std::sort(edges.begin(), edges.end());

	for (auto edgesIter = edges.begin(); edgesIter != edges.end(); edgesIter++) {
		queue.push(*edgesIter);
	}

	// Create a disjoint sets structure where each vertex is represented by a set
	DisjointSets forest;
	std::vector<Vertex> vertices = graph.getVertices();
	int numVertices = vertices.size();
	forest.addelements(vertices.size());

	/**
	 * Traverse the list from the start (i.e., from lightest weight to heaviest).
	 * Inspect the current edge. If that edge connects two vertices from different sets,
	 	union their respective sets and mark the edge as part of the MST.
	 	Otherwise there would be a cycle, so do nothing.
	 *   Repeat this until n−1 edges have been added, where n is the number of vertices in the graph.
	 */

	int numEdgesAdded = 0;

	while (numEdgesAdded < numVertices - 1) {
		Edge nextEdge = queue.front();
		queue.pop();
		Vertex source = nextEdge.source;
		Vertex dest = nextEdge.dest;

		if (forest.find(source) != forest.find(dest)) {
			graph.setEdgeLabel(source, dest, "MST");
			forest.setunion(source, dest);
			numEdgesAdded++;
		}
	}
}
```

2. [Prim's Algorithm (MST)](https://www.youtube.com/watch?v=cplfcGZmX7I) -- Partition
	![Prim](https://github.com/alichtman/data-structures-cpp/blob/master/images/Prim.jpg)
	1. Choose start vertex.
	2. Add the next lowest weighted incident edge that wouldn't create a cycle and is not already visited. Do this over and over until you have an MST.


```cpp
void Prim(Graph& g, Vertex start) {

	vector<int> dist;
	vector<Vertex> predecessor;

	//Set all initial distances to max, predecessors to NULL.
	for (int i = 0; i < g.getVertices().size(); i++) {
		dist[i] = +inf ***(use 99999);
		predecessor[i] = NULL
	}

	dist[start] = 0;

	Queue<Vertex> queue;

}

```

|	Implementation |	Adj. Matrix | Adj. List	|
|	---	| ---	|	--- |
| Heap	| $O(n^2 + mlog(n))$	|	$O(n log(n) + mlog(n))$|
| Unsorted Array	| $O(n^2)$	| $O(n^2)$	|

**Shortest Path Algorithms**

1. [Dijkstra's Algorithm](https://www.youtube.com/watch?v=_lHSawdgXpI) -- Closely related to Prim's
	+ Can look up distance to any node in $O(1)$ time
	+ Every edge needs a non-negative weight.
	+ Next vertex weight is the previous vertex weight plus the edge weight to get there.
	+ $O(m + nlog(n))$ when using Fibionnaci Trees (My notes say this is the same as Prim's?)

2. Floyd-Warshall
	+ Similar to Dijkstra, but can be used with negative edge weights.
	+ Time Complexity of $O(n^{3})$
