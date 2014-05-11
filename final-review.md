## Minimum Spanning Trees

#### What kind of graph-based optimization problems require as a solution the computation of a Minimum Spanning Tree? Why the solution to such problems does not contain cycles?

> __Usage.__ The cheapest path that would cover all the nodes.

> In the Generic-MST method on a connected graph `G = (V,E)`, the set _A_ is always acyclic. Otherwise, a minimum spanning tree including _A_ would contain a cycle, which is a _contradiction_. The MST can only go through each node once!

#### Provide a generic description of an algorithm for the computation of minimum spanning trees.

```java
Generic_MST(G,w)
1  A = 0
2  while A does not form a spanning tree
3    find an edge (u,v) that is safe for A
4    A = A U {(u,v)}
5  return A
```

> __Initialization.__ After line 1, the set A trivially satisfies the loop invariant.

> __Maintenance.__ The loop in lines 2-4 maintains the invariant by adding only safe edges.

> * __Safe edge__ is an edge (u,v) that can be added to A without violating the invariant, such that A U {(u,v)} is also a subset of a MST.
> * The loop executes __|V|-1__ times because it finds one of the _|V|-1_ edges of a MST in each iteration.

> __Termination.__ All edges added to A are in a minimum spanning tree, and so the set A returned in line 5 must be a minimum spanning tree.

#### What is a cut of a graph? When does an edge cross a cut? When does a cut respect a set of edges? What is the definition of a light edge?

> A __cut__ `(S,V-S)` of an undirected graph `G = (V,E)` is a partition of _V_.

> An edge `(u,v) element of E` __crosses__ the cut `(S,V-S)` if one of its endpoints is in _S_ and the other is in _V - S_.

> A cut __respects__ a set _A_ of edges if no edge in _A_ crosses the cut.

> An edge is a __light edge__ crossing a cut if its weight is the minimum of any edge crossing the cut.

#### Assume a connected, undirected graph G(V, E) with weights w and a set of edges A &sub; E that is a subset of minimum spanning tree T. Consider then any cut (S, V − S) that respects the set A. Prove that if (u, v) is a light-edge crossing (S, V − S), then (u, v) can be safely be added to A as an edge that is part of a minimum spanning tree of G.

> __Proof.__

> * Let _T_ be a minimum spanning tree that includes _A_, and assume that _T_ does not contain the light edge `(u,v)`, otherwise the proof is done.
> * Construct another minimum spanning tree _T'_ that includes `A U {(u,v)}` by using a cut-and-paste technique, thereby showing that `(u,v)` is a safe edge for _A_.
> * The edge `(u,v)` forms a cycle with the edges on the simple path _p_ from _u_ to _v_ in _T_.
> * Since _u_ and _v_ are on opposite sides of the cut `(S,V-S)`, at least one edge in _T_ lies on the simple path _p_ and also crosses the cut.
> * Let `(x,y)` be any such edge. The edge `(x,y)` is not in _A_, because the cut respects _A_.
> * Since `(x,y)` is on the unique simple path from _u_ to _v_ in _T_, removing `(x,y)` breaks _T_ into two components.
> * Adding `(u,v)` reconnects them to form a new spanning tree __T' = T - {(x,y)} &cup; {(u,v)}__
> * We show that _T'_ is a minimum spanning tree. Since `(u,v)` is a light edge crossing `(S,V-S)` and `(x,y)` also crosses this cut `w(u,v) <= w(x,y)`.

```java
w(T prime) = w(T) - w(x,y) + w(u,v)
          <= w(T)
```

> * Since T is a MST, so that `w(T) <= w(T')`, _T'_ must be a MST as well.

> * Since _A &sub; T_ and _(x,y) &notin; A_; thus _A &cup; {(u,v)} &sube; T'_.

> * Since _T'_ is a minimum spanning tree, `(u,v)` is safe for _A_.

#### Given the above statement, prove the following: Let C = (V<sub>C</sub> , E<sub>C</sub> ) be a connected component (tree) in the forest GA (V, A). If (u, v) is a light-edge connecting C to another component in G<sub>A</sub>, then (u, v) is safe for A.

> __Proof.__

> The cut _(V<sub>C</sub>,V-V<sub>C</sub>)_ respects _A_, and `(u,v)` is a light edge for this cut. Therefore, `(u,v)` is safe for _A_.

## Kruskal’s and Prim’s algorithms

#### Given the generic algorithm for the computation of a minimum spanning tree, how is the safe edge computed in Kruskal’s algorithm and how is it computed in Prim’s algorithm?

> __Kruskal's Algorithm.__ Safe edge is computed from an increasing order of set vertices, the find_set() method prevents any cycles from forming.

#### You may be provided a graph and asked to trace the steps of Kruskal’s and Prim’s algorithms for the computation of the minimum spanning tree of the graph.



#### Provide Kruskal’s algorithm.

```java
MST-KRUSKAL(G, w)
1  A = empty set;
2  for each vertex element of G,V
3    MAKE-SET(v)
4  sort the edges of G,E into nondecreasing order by weight w
5  for each edge (u,v) element of G,E, taken in nondecreasing order by weight
6    if FIND-SET(u) != FIND-SET(v)
7      A = A U {(u,v)}
8      UNION(u,v);
9  return A
```

> * Lines 1–3 initialize the set _A_ to the empty set and create _|V|_ trees, one containing each vertex. Runtime is __O(|V|)__.
> * Line 4 sort the edges in an increasing order. Runtime is __O(E log E)__.
> * The for loop in lines 5–8 examines edges in order of weight, from lowest to highest. Runtime is __O(E)__ FIND-SET and UNION operations.
> * The loop checks, for each edge `(u,v)`, whether the endpoints _u_ and _v_ belong to the same tree.
> * If they do, then the edge `(u,v)` cannot be added to the forest without creating a cycle, and the edge is discarded. Otherwise, the two vertices belong to different trees.
> * In this case, line 7 adds the edge `(u,v)` to _A_, and line 8 merges the vertices in the two trees.
> * The overall runtime is __O(E log V)__.

#### Consider an implementation of the disjoint sets data structure with the union-by-rank heuristic as part of the implementation of Kruskal’s algorithm. What is the running time of Kruskal’s algorithm in this case and why? Consider an implementation of the disjoint sets data structure with the union-by-rank and the path compression heuristic. Furthermore, consider that the edge weights are upper bounded by the value |E|.  What is the running time of Kruskal’s algorithm in this case and why?

> __Union-by-rank.__ The approach is to make the root of the tree with fewer nodes point to the root of the tree with more nodes. Rather than explicitly keeping track of the size of the subtree rooted at each node, we shall use an approach that eases the analysis. For each node, we maintain a __rank__, which is an upper bound on the height of the node. In union by rank, we make the root with smaller rank point to the root with larger rank during a __union()__ operation.

> * Runtime = __O(m log n)__, where __m__ is the total number of makeset(), union(), and find_set() operations, and __n__ is the number of makeset() operations.

> __Path compression.__ The approach is used during the __find_set()__ operation, to make each node on the find path point directly to the root. Path compression does not change any ranks.

> __Union-by-rank + path compression heuristic.__

> * Assuming that _G_ is connected, where _|E| &ge; |V| - 1_, then the disjoint-set operations take _O(E &alpha;(V))_ time.

> * Since _&alpha;(|V|) = O(log V) = O(log E)_, the total runtime of Kruskal’s algorithm is _O(E log E)_.

> * Observing that _|E| < |V|<sup>2</sup>_, we have _log |E| = O(log V)_, and so the running time of Kruskal’s algorithm is restated as __O(E log V)__.

#### Describe the makeset, find_set and union functions of the disjoint sets data structure given the union-by rank heuristic. What is the running time of these operations? How does the find_set function change when you also use the path compression heuristic? What is the new running time of the find_set and union functions in this case?

> A __makeset()__ operation simply creates a tree with just one node.

> * The runtime is __O(1)__, but will be called V times.

```java
MAKE-SET(x)
1 x.p = x
2 x.rank = 0
```

> We perform a __find_set()__ operation by following parent pointers until we ﬁnd the root of the tree. The nodes visited on this simple path toward the root constitute the ﬁnd path.

> * Without Path Compression, the runtime is __O(log V)__.
> * With Path Compression, the runtime is __O(1)__.

```java
// without Path Compression
FIND-SET(x)
1  while x != x.p
2    x = x.p
3  return x

// with Path Compression
FIND-SET(x)
1  if x != x.p
2    x.p = FIND-SET(x.p)
3  return x.p
```

> A __union()__ operation causes the root of one tree to point to the root of the other.

> * With Union-by-Rank, the runtime is __O(log V)__.

```java
// with Union-by-Rank
UNION(x,y)
1  x = FIND-SET(x)
2  y = FIND-SET(y)
3  if x.rank > y.rank
4    y.p = x
5  else x.p = y
6    if x.rank == y.rank
7      y.rank = y.rank + 1
```

#### Provide Prim’s algorithm.

```java
MST-PRIM(G, w, r)
1  for each u element of G,V
2    u.key = infinity
3    u.pie = NIL
4  r.key = 0
5  Q = G.V
6  while Q != 0
7    u = EXTRACT-MIN(Q)
8    for each v element of G.Adj[u]
9      if v element of Q and w(u,v) < v.key
10       v.pie = u
11       v.key = w(u,v)
```
