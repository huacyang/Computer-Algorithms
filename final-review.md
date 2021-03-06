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

> ![Light edge weight proof](img/light-edge-weight.png)

> * Since T is a MST, so that `w(T) <= w(T')`, _T'_ must be a MST as well.

> * Since _A &sub; T_ and _(x,y) &notin; A_; thus _A &cup; {(u,v)} &sube; T'_.

> * Since _T'_ is a minimum spanning tree, `(u,v)` is safe for _A_.

#### Given the above statement, prove the following: Let C = (V<sub>C</sub> , E<sub>C</sub> ) be a connected component (tree) in the forest GA (V, A). If (u, v) is a light-edge connecting C to another component in G<sub>A</sub>, then (u, v) is safe for A.

> __Proof.__

> The cut _(V<sub>C</sub>,V-<sub>C</sub>)_ respects _A_, and `(u,v)` is a light edge for this cut. Therefore, `(u,v)` is safe for _A_.

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

#### What is the running time of Prim’s algorithm given an array implementation of a priority queue? What is the running time of the algorithm given a binary heap implementation of a priority queue?

> __Binary Heap.__

> * We can use the BUILD-MIN-HEAP procedure to perform lines 1-5 in __O(V)__ times.
> * The body of the while loop executes _|V|_ times, and since each EXTRACT-MIN operations takes _O(log V)_ time, the total time for all calls to EXTRACT-MIN is __O(V log V)__.
> * The for loop in lines 8-11 executes __O(E)__ times altogether, since the sum of the lengths of all adjacency lists is _2|E|_.
> * Within the for loop, we can implement the test for membership in Q in line 9 in constant time by keeping a bit for each vertex that tells whether or not it is in Q, and updating the bit when the vertex is removed from Q.
> * The assignment in line 11 involves an implicit DECREASE-KEY operation on the min-heap, which a binary min-heap supports in __O(log V)__ time.
> * The total time for Prim's algorithm is _O(V log V + E log V)_ = __O(E log V)__.

## The class of NP problems

#### What is the satisfiability problem? What is the worst-case running time of the best known algorithm for this problem? What is the running time of checking whether a candidate solution is truly solving the problem or not?

> The satisfiability problem is a __Boolean formula in Conjunctive Normal Form__ (_CNF_). It is a collection of _clauses_ (the parentheses), each consisting of the disjunction (logical _or_, denoted as &or;) of several literals.

> __The SAT Problem.__ Given a Boolean formula in _CNF_, either find a satisfying truth assignment or else report that none exists.

> * A __literal__ is either a Boolean variable (such as _x_) or the negation of one (such as _&not;x_).
> * A __satisfying truth assignment__ is an assignment of _false_ or _true_ to each variable so that every clause contains a literal whose value is _true_.

> The worst-case running time is __exponential__.

> The running time of checking whether a candidate solution is truly solving the problem or not is __polynomial__.

#### Are there versions of the general satisfiability problem that can be solved in polynomial time? Describe two of them.

> __Horn formula.__ If all clauses contain at most one positive literal, and can be satisfied by the Greedy algorithm.

> __2SAT__ contains two literals, and can be solved by finding the strongly connected components of a particular graph.

#### What is the traveling salesman problem? What is a dynamic programming approach for the traveling salesman approach? What is the running time of this approach?

> The __Traveling Salesman Problem__ is a _search problem_: find a _tour_, a cycle that passes through every vertex exactly once, within the given budget&#8212;or to report that no such tour exists.

> __Dynamic programming approach.__

> * __Subproblem__:
>   - For a subset of cities _S &sube; {1,2,...,n}_ that includes _1_, and _j &isin; S_, let _C(S,j)_ be the length of the shortest path visiting each node in _S_ exactly once, starting at _1_ and ending at _j_.
> * __Code__

```java
1  C({1},1) = 0
2  for s = 2 to n:
3    for all subsets S subset of {1,2,...,n} of size s and containing 1:
4      C(S,1) = infinity
5      for all j element of S, j != 1
6        C(S,j) = min{C(S - {j},i) + d of ij : i element of S, i != j}
7  return min of j C({1,...,n},j) + d of j1
```

> * There are at most 2<sup>n</sup> &times; n subproblems, and each one takes linear time to solve. The total running time is therefore __O(n<sup>2</sup>2<sup>n</sup>)__.

#### Show that any optimization problem can be reduced to a search problem. Show that any search problem can be reduced to an optimization problem. Why do we typically prefer to work with search problems when studying the computational complexity of algorithms?

> __Optimization Problem__ &rarr; __Search Problem__

> * Any algorithm that solves the optimization _TSP_ also readily solves the search problem: find the optimum tour and if it is within budget, return it; if not, there is no solution.

> __Search Problem__ &rarr; __Optimization Problem__

> * Suppose that we somehow knew the _cost_ of the optimum tour; then we could find this tour by calling the algorithm for the search problem, using the optimum cost as the budget. We then find the optimum cost by __binary search!__

#### What is an Eulerian tour? When does a graph have an Eulerian tour?

> A __Euler tour__ of a connected, directed graph `G = (V,E)` is a cycle that traverses each _edge_ of _G_ exactly once, although it is allowed to visit each vertex more than once.

> __Condition.__ If and only if (a) the graph is connected and (b) every vertex, with the possible exception of two vertices (the start and final vertices of the walk), has even degree.

#### What is the Rudrata cycle/path problem? Is there a polynomial time algorithm for this problem?

> __Rudrata Cycle.__ Given a graph, find a _cycle_ that visits each vertex exactly once&#8212;or report that no such cycle exists.

> __Rudrata Path.__ Is just like the Rudrata Cycle, except the goal is now to find a _path_ rather than a _cycle_.

> There are no polynomial time algorithm for this problem. The Rudrata cycle is very similar to the _TSP_.

#### What is the independent set problem? Describe a dynamic programming solution for computing an independent set on trees. What is the running time of this solution? Is there a polynomial time algorithm for this problem on general graphs?

> A subset of nodes _S &sub; V_ is an independent set of graph `G = (V,E)` if there are no edges between them.

> The __independent-set problem__ is to find a maximum-size independent set in _G_.

> When the graph happens to be a tree, the problem can be solved in linear time, __O(|V| + |E|)__ using dynamic programming.

> __Dynamic Programming__

> * Start by rooting the tree at any node _r_. Now, each node defines a subtree&#8212;the one hanging from it.
> * _I(u)_ = size of largest independent set of subtree hanging from _u_.
> * Final goal is _I(r)_.

#### What is the vertex cover problem? What is the clique problem? Are there polynomial time algorithms for these problems?

> A __vertex cover__ of an undirected graph `g = (V,E)` is a subset _V &sube; V_ such that if _(u,v) &isin; E_, then _u &isin; V'_ and/or _v &isin; V'_. A vertex cover for _G_ is a set of vertices that covers all the edges in _E_.

> The __vertex-cover problem__ is to find a vertex cover of minimum size in a given graph. Restating this optimization problem as a decision problem, we wish to determine whether a graph has a vertex cover of a given size _k_.

> The vertex-cover problem is a NP complete problem. A polynomial-time __approximation algorithm__ can obtain near-optimal solutions to the vertex-cover problem.

> A __clique__ of an undirected graph `G = (V,E)` is a subset _V' &sube; V_ of vertices, each pair of which is connected by an edge in _E_. In other words, a clique is a complete subgraph of _G_.

> The __clique problem__ is the optimization problem of finding a clique of maximum size in a graph. As a decision problem, we ask simply whether a clique of a given size _k_ exists in the graph.

> There isn't a polynomial-time algorithm for clique, because it is NP-hard.

## The Reduction of NP complete problems

#### What is the minimum cut problem? Is there a polynomial time algorithm for this problem?

> A __cut__ is a set of edges whose removal leaves a graph disconnected. It is often of interest to find small cuts.

> The __minimum cut problem__ is, given a graph and a budget _b_, to find a cut with at most _b_ edges.

> This problem can be solved in polynomial time by __n - 1 max-flow computations__.

> * Give each edge a capacity of 1, and find the maximum flow between some fixed node and every single other node.
> * The smallest such flow will correspond (via the max-flow min-cut theorem) to the smallest cut.

#### Consider the following approach for computing a minimum cut: run Kruskal’s algorithm on an unweighted graph and remove the last edge of the resulting minimum spanning tree to define a cut (randomize the selection of the edges among multiple equivalent choices). Show that the probability of this cut being the minimum cut is at least 1/n<sup>2</sup>. What is the running time n of the randomized approach that computes the minimum cut with high probability through Kruskal’s algorithm?

> Proof of 1/n<sup>2</sup> probability:

> * The number of edges incident to each component must be at least _C_, the size of the minimum cut in _G_.
> * So if there are _k_ components in the graph, the number of eligible edges is at least _kC/2_
>   - each of the _k_ components has at least C edges leading out of it, and we need to compensate for the double-counting of each edge.
> * Since the edges were randomly ordered, the chance that the next eligible edge in the list is from the minimum cut is at most C/(kC/2) = 2/k.
> * Thus, with probability at least 1 - 2/k = (k - 2)/k, the choice leaves the minimum cut intact.
> * But now the chance that Kruskal's algorithm leaves the minimum cut intact all the way up to the choice of the last spanning tree edge is at least:

> ![Percent change calculation of Krushkal's with MST](img/kruskal-with-mst.png)

> The final runtime is __O(n<sup>2</sup> log n)__.

#### What is the balanced cut problem? Is there a polynomial time algorithm for this problem?

> __Balanced cut problem.__ Given a graph with n vertices and a budget _b_, partition the vertices into two sets _S_ and _T_ such that __|S|,|T| &ge; n/3__ and such that there are at most _b_ edges between _S_ and _T_.

> Since the balanced cut problem is a __NP-hard__ problem, there is no polynomial time algorithm for this problem.

#### What is the knapsack problem? Is there a polynomial time algorithm for this problem? What is the subset sum problem and how does it relate to the knapsack problem?

> __Knapsack Problem.__ Given a weight capacity _W_ and a goal _g_, find a set of items whose total weight is at most _W_ and whose total value is at least _g_.

> There is no polynomial time algorithm for this problem. The dynamic programming scheme for the Knapsack problem runs in __O(nW)__.

> __Subset Sum Problem.__ Provided that an item's value is equal to its weight, and the goal _g_ is the same as the weight capacity _W_, find a subset of a given set of integers that adds up to exactly _W_.

> The subset sum problem is a variant of the knapsack problem, except that the value of the item is directly porportional to its weight.

#### What is the class of NP problems? What is the class of P problems? What is the relation between these two classes of problems? For instance, is P = NP?

> We denote the class of all search problems by __NP__.

> We denote the class of all search problems that can be solved in polynomial time by __P__.

> The P versus NP problem is to determine whether every language accepted by some nondeterministic algorithm in polynomial time is also accepted by some (deterministic) algorithm in polynomial time.

#### What does it mean that you can reduce a search problem A to a search problem B? What do you need to do in order to provide such a reduction? (you can provide a drawing to explain your answer)

> A reduction from search problem A to search problem B is a polynomial-time algorithm _f_ that transforms any instance _I_ of _A_ into an instance f(I) of _B_, together with another polynomial-time algorithm _h_ that maps any solution _S_ of f(I) back into a solution h(S) of _I_

> If we denote a reduction from A to B by __A &rarr; B__, then we can say that difficulty flows in the direction of the arrow, while efficient algorithms move in the opposite direction.

#### What is the class of NP-complete problems? What is the class of NP-hard problems?

> A search problem is __NP-complete__ if all other search problems reduce to it.

> __NP-hard__ is a class of problems that are, informally, "at least as hard as the hardest problems in NP"

#### When is a problem in the class of co-NP problems? Provide an example of a co-NP problem.

> The __Complexity Class NP__ is a class of languages that can be verified by a polynomial-time algorithm.

> A language _L_ belongs to NP if and only if there exist a two-input polynomial-time algorithm _A_ and a constant _c_ such that:

> L = {x &isin; {0,1}* : there exists a certificate _y_ with _|y|_ = __O(|x|<sup>e</sup>)__, such that _A(x,y) = 1_}

> We say that algorithm _A_ __verifies__ language _L_ __in polynomial time__.

> __Example.__

> * The hamiltonian-cycle problem (TSP) &isin; NP
> * If _L_ &isin; P, then _L_ &isin; NP, since if there is a polynomial-time algorithm to decide _L_, the algorithm can be easily converted to a two-argument verification algorithm that simply ignores any certificate and accepts exactly those input strings it determines to be in _L_.
> * Thus, P &sube; NP

## Reductions between NP complete problems

#### Show that the general satisfiability (SAT) problem reduces to the 3-SAT problem.

> __SAT problem__ &rarr; __3-SAT problem__

> * Given an instance _I_ of SAT, use exactly the same instance for 3-SAT, except that any clause with more than three literals,
>   - __(a<sub>1</sub> &or; a<sub>2</sub> &or; ... &or; a<sub>k</sub>)__
> * Is replaced by a set of clauses,
>   - __(a<sub>1</sub> &or; a<sub>2</sub> &or; y<sub>1</sub>)(&not;y<sub>1</sub> &or; a<sub>3</sub> &or; y<sub>2</sub>)(&not;y<sub>2</sub> &or; a<sub>4</sub> &or; y<sub>3</sub>) ... (&not;y<sub>k-3</sub> &or; a<sub>k-1</sub> &or; a<sub>k</sub>)__
> * Where the _y<sub>i</sub>_'s are new variables.
> * Call the resulting 3-SAT instance _I'_, the conversion from _I_ to _I'_ is clearly polynomial time.
> * _I'_ is equivalent to _I_ in terms of satisfiability, because for any assignment to the _a<sub>i</sub>_'s,

> ![SAT to 3-SAT](img/sat-to-3-sat.png)

> * Suppose that the clauses on the right are all satisfied.
> * Then at least one of the literals _a<sub>1</sub>,...,a<sub>k</sub>_ must be true&#8212;otherwise _y<sub>1</sub>_ would have to be true, which would in turn force _y<sub>2</sub>_ to be true, and so on, eventually falsifying the last clause.
> * But this means _(a<sub>1</sub> &or; a<sub>2</sub> &or; ... &or; a<sub>k</sub>)_ is also satisfied.

#### Show that the 3-SAT problem reduces to the Independent Set problem.

> __3-SAT__ &rarr; __Independent Set__

> * Given an independent set _S_ of _g_ vertices in _G_, it is possible to efficiently recover a satisfying truth assignment to _I_.
> * If graph _G_ has no independent set of size _g_, then the Boolean formula _I_ is unsatisfiable.
> * Pikachu!

#### Show that the Independent Set problem reduces to the Vertex Cover problem.

> __Independent Set problem__ &rarr; __Vertex Cover problem__

> * Notice that a set of nodes _S_ is a vertex cover of graph `G = (V,E)` if and only if the remaining nodes, `V - S`, are an independent set of _G_.
> * Therefore, to solve an instance `(G,g)` of Independent Set, simply look for a vertex cover of _G_ with `|V| - g` nodes.
> * If such a vertex cover exists, then take all nodes _not_ in it.
> * If no such vertex cover exists, then _G_ cannot possibly have an independent set of size _g_.

#### Show that the Independent Set problem reduces to the Clique problem.

> __Independent Set problem__ &rarr; __Clique problem__

> * Define the _complement_ of a graph `G = (V,E)` to be __&not;G = (V,&not;E)__, where _&not;E_ contains precisely those unordered pairs of vertices that are not in _E_.
> * Then a set of nodes _S_ is an independent set of _G_ if and only if _S_ is a clique of _&not;G_.
>   - Paraphrase: these nodes hav eno edges between them in _G_ if and only if they have all possible edges between them in _&not;G_.
> * Therefore, we can reduce independent set to clique by mapping an instance _(G,g)_ of independent set to the corresponding instance _(&not;G,g)_ of clique; the solution to both is identical.

#### Show that the Circuit SAT problem reduces to the SAT problem. What is the importance of this reduction?

> __Circuit SAT problem__ &rarr; __SAT problem__

> * For each gate _g_ in the circuit we create a variable _g_, and we model the effect of the gate using a few clauses:

> ![Circuit SAT to SAT](img/circuit-sat-to-sat.png)

> * If _g_ is the output gate, we force it to be __true__ by adding the clause (g).
> * The resulting instance of SAT is equivalent to the given instance of Circuit SAT: the satisfying truth assignments of this conjunctive normal form are in one-to-one correspondence with those of the circuit.

## Intelligent Exhaustive Search, Approximation Algorithms

#### What is the idea behind backtracking search in order to solve NP-complete problems?

> __Backtracking__ explores the space of assignments, growing the tree only at nodes where there is uncertainty about the outcome, and stopping if at any stage a satisfying assignment is encountered.

#### Describe a general framework for backtracking search.

```java
1  Start with some problem P0
2  Let S = {P0}, the set of active subproblems
3  Repeat while S is nonempty:
4    _choose a subproblem P element of S and remove it from S
5    _expand it into smaller subproblems P1,P2,...,Pk
6    For each Pi:
7      If _test(Pi) succeeds: halt and announce this solution
8      If _test(Pi) fails: discard Pi
9      Otherwise: add Pi to S
10 Announce that there is no solution
```

> * The __choose__ procedure picks a clause
> * The __expand__ picks a variable within that clause
> * The __test__ looks at a subproblem and quickly declares one of the three outcomes:
>   - Failure: the subproblem has no solution
>   - Success: a solution to the subproblem is found
>   - Uncertainty

#### Describe the application of backtracking search to the satisfiability problem, i.e., which sub-problems are expanded at each iteration and which branching variable is considered?

> The nodes of the search tree, representing partial assignments, are themselves __SAT subproblems__.

> The application of __backtracking__ choose the subproblem that contains the _smallest_ clause and to then branch on a variable in that clause.

#### Describe the general branch-and-bound approach for optimization problems.

> * Define the subproblem: what is the (cost of the) best way to complete the solution?
> * Set the basis for eliminating partial solutions.
> * Reject a subproblem if the cost exceeds that of some other solution already encountered.
> * Use a quick _lower bound_ on the cost.

```java
1  Start with some problem P0
2  Let S = {P0}, the set of active subproblems
3  bestsofar = infinity
4  Repeat while S is nonempty:
5    _choose a subproblem P element of S and remove it from S
6    _expand it into smaller subproblems P1,P2,...,Pk
7    For each Pi:
8      If Pi is a complete solution: update bestsofar
9      else if _lowerbound(Pi) < bestsofar: add Pi to S
10 return bestsofar
```

#### Describe an application of branch-and-bound to the traveling salesman problem.

> * At each step of the __branch-and-bound__ algorithm, we extend a particular partial solution `[a,S,b]` by a single edge `(b,x)`, where _x &isin; V - S_.
> * There can be up to `|V - S|` ways to do this, and each of these branches leads to a subproblem of the form _[a,S&cup;{x},x]_.
> * Set the lower-bound of the cost to the sum of the following:
>   - The lightest edge from _a_ to `V - S`
>   - The lightest edge from _b_ to `V - S`
>   - The minimum spanning tree of `V - S`

#### How is the approximation ratio of an approximation algorithm computed?

> A problem has an __approximation ratio__ of _p(n)_ if, for any input of size _n_, the cost _C_ of the solution produced by the algorithm is within a factor of _p(n)_ of the cost _C*_ of an optimal solution:

> ![Approximation Algorithm's approximation ratio](img/approximation-ratio.png)

> For a __maximization problem__, _O &lt; C &le; C*_, and the ratio _C* / C_ gives the factor by which the cost of an optimal solution is larger than the cost of the approximate solution.

> For a __minimization problem__, _O &lt; C* &le; C_, and the ratio _C / C*_ gives the factor by which the cost of the approximate solution is larger than the cost of an optimal solution.

#### Provide an approximation algorithm for the vertex cover problem. What approximation ratio does it achieve?

> The better approximation algorithm for vertex cover is based on the notion of a __matchin__, a subset of edges that have no vertices in common.

> A matching is __maximal__ if no more edges can be added to it.

> Maximal matchings will help find good vertex covers, and moreover, they are easy to generate:

> * Repeatedly pick edges that are disjoint from the ones chosen already, until this is no longer possible.

```java
Find a maximal matching M subset of E
Return S = {all endpoints of edges in M}
```

> This simple algorithm has an approximation ratio of __&alpha;A &le; 2__.

## Approximation Algorithms, Local Search Heuristics

#### When does a distance function satisfy metric properties?

> __Metric Properties.__

> 1. _d(x,y)_ &ge; 0 for all _x,y_
> 2. _d(x,y)_ = 0 if and only if _x = y_
> 3. _d(x,y)_ = _d(y,x)_
> 4. _d(x,y)_ &le; d(x,z) + d(z,y)

#### What is the k-clustering NP-complete problem? Provide a simple approximation scheme for the k-clustering problem. What is the approximation ratio that it achieves. Prove it.

> __K-clustering NP-complete problem.__

> * Pick _k_ of the data points as cluster centers.
> * Assign each of the remaining points to the center closest to it, thus creating _k_ clusters.
> * The centers are picked one at a time
>   - Always pick the next center to be as far as possible from the centers chosen so far.

```java
1  Pick any point u1 element of X as the first cluster center
2  for i = 2 to k:
3    Let ui be the point in X that is farthest from u1,...,ui-1
4  Create k clusters: Ci = {all x element of X whose closest center is ui}
```

> __Approximation Scheme__

> * Similar to the scheme for __Vertex Cover__.
> * Computable Structure:
>   - A set of _k_ points that cover all of _X_ within some radius _r_
>   - While at the same time being mutually separated by a distance of at least _r_
> * This structure is used both to generate a clustering and to give a lower bound on the optimal clustering

#### Provide an approximation algorithm for the traveling salesman problem given that the underlying graph has edge weights that satisfy metric properties. What is the approximation ratio for this algorithm? Prove it.

#### Describe the general local search framework.

```java
1  let s be any initial solution
2  while there is some solution s` in the neighborhood of s
3    for which cost(s`) < cost(s): replace s by s`
4  return s
```

> * On each iteration, the current solution is replaced by a better one close to it, in its __neighborhood__.
> * This neighborhood structure is something we impose upon the problem and is the central design decision in local search.

#### Provide a local search approach for the traveling salesman problem.

> * Assume we have all interpoint distances between _n_ cities, giving a search space of `(n - 1)!` different tours.
> * The notion is to consider two tours as being close if they differ in just a few edges.
> * We define the _k_-change neighborhood of tour _s_ as being the set of tours that can be obtained by removing _k_ edges of _s_ and then putting in _k_ other edges.
> * The tour has __O(n<sup>k</sup>)__ neighbors.
> * The final tour is __locally optimal__&#8212;it is superior to the tours in its immediate neighborhood.

#### Provide a local search strategy for the graph partitioning problem.

> * __Local search algorithm.__ Focus on the special case _&alpha; = 1/2_, in which _A_ and _B_ are forced to contain exactly half the vertices.
> * Let _(A,B)_, with |A| = |B|, be a candidate solution.
> * We will define its neighbors to be all solutions obtainable by swapping one pair of vertices across the cut.
> * All solutions of the form __(A-{a}+{b}, B-{b}+a)__ where _a &isin; A_ and _b &isin; B_.

#### How can you deal with local optima in the context of local search?

> __Randomization.__

> * To pick a random initial solution (i.e. a random graph partition).
> * To choose a local move when several are available.

> Randomization is a way of making sure that there is at least some probability of getting to the right one.

> * The local search can be repeated several times, with a different random seed on each invocation, and the best solution returned.
> * The probability of reaching a good local optimum on any given run is _p_, then within __O(1/p)__ runs such a solution is likely to be found.
