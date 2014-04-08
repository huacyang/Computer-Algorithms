## Greedy Algorithms

#### What is the main principle behind greedy algorithms?

> The __Greedy algorithms__ build up a solution piece by piece, always choosing the next piece that offers the most obvious and immediate benefit. 

#### Why does the greedy algorithm work for the coin changing problem given the US coin system?

> __Theorem.__ Greed is optimal for U.S. coinage: 1, 5, 10, 25, 100.

> __Proof.__ (by induction on _x_)  
> * Consider optimal way to change _c<sub>k</sub> &le; x &lt; c<sub>k+1</sub>_ : greedy takes coin k.
> * We claim that any optimal solution must also take coin _k_.
>	- if not, it needs enough coin of type _c<sub>1</sub>, ..., c<sub>k-1</sub>_ to add up to _x_
>	- table below indicates no optimal solution can do this.
> * Problem reduces to coin-changing _x - c<sub>k</sub>_ cents, which, by induction, is optimally solved by greedy algorithm.

> k | c<sub>k</sub> | Optimal solutions | Max value
> --- | --- | --- | ---
> 1 | 1 | P &le; 4 | -
> 2 | 5 | N &le; 1 | 4
> 3 | 10 | N + D &le; 2 | 4 + 5 = 9
> 4 | 25 | Q &le; 3 | 20 + 4 = 24
> 5 | 100 | no limit | 75 + 24 = 99

> __Example.__ Someone wants to give change to a customer in coins, what's the best way?  
> * The highest coin is chosen that does not exceed the amount of change currently left to give.
> * This loop continues until there is no more change to give.
> * Such that, if change is 35 cents, then it starts by selecting a quarter which is 25 cents, a dime, ..., so on.

#### What is the idea in Huffman encoding in order to achieve data compression? What is the prefix-free property?

> __Huffman Coding__ is used to compress data in order to save space.

> * In order to save space, Huffman coding uses a __prefix-free binary tree__ in order to encode.
> * In order to optimize the tree and save as much space as possible, we want to make sure each leaf corresponds to a symbol.
>	- In this method, the number of bits required for a symbol is exactly the depth of the tree.
> * Althernatively, we can calculate the cost by seeing that the frequency of any node is the sum of the frequencies of decendant leaves.

#### Provide the Huffman encoding algorithm and argue its running time.

> __Cost.__ The sum of the frequencies of all leaves and nodes except the root.
> * We also know that the lowest frequencies must be at the bottom of the tree.

> To construt the tree:
> * First find the two nodes with the lowest frequency _i_, _j_.
> * Then, assign them to a node with the frequency _i + j_.
> * Continue this process until all frequencies are represented as leaves in the tree.

> __Run Time.__ Building the tree will take _O(nlog(n))_, if a heap is used.

#### Describe the greedy algorithm for logical reasoning with Horn formulas.

> __Horns Formulas.__ A set of expressions with literals Implications and Negative Clauses.

> __Implications.__  
> * Left hand side is an __AND__ of any number of positive literals.
> * Right hand side is a single positive literal _(Z<sup>w</sup>) -> u_.

> __Negative Clauses.__  
> * Consist of an __OR__ of any number of negative literals (_!u_ OR _!v_ OR _!y_).

> __Strategy.__  
> * Start with all variables as false.
> * Then we start to make some true, one by one, to satisfy the implications (_RHS_).
> * Then turn to the negative clauses and make sure their satisfied.
> _Note._ If a certain set of variables is set to true, then they must be true in any satisfying assignment.

#### What is the property of the greedy algorithm for the set cover example? Prove it.

> __Example.__ You have a set of schools _S<sub>i</sub>_, and you want to see how many schools from the set will cover the country, essencially outputting a set of _S<sub>x</sub>_ schools.  
> * More generally, we can see that _B_ contains _n_ elements and that the optimal cover consists of _k_ sets, then the greedy will use __(k ln(n))__ sets.

> __Strategy.__  
> * Use greedy to grab the largest sets first without going over the contraint.
> * School example (grab school that covers the largest without going over and second largest without going over and so on).
> * Let _nt_ be the number of elements still not covered after _t_ iterations, _k_ sets are needed for optimal therefore _nt/k_ extra will be needed.
> * _nt + 1 <= nt - nt/k = nt(1 - 1/k)_

> __Run-time.__ The approximation value of this greedy vs. optimal is _ln(n)_.

## Elements of Dynamic Programming

#### How does the dynamic programming approach decompose the chain-matrix multiplication into subproblems and how are their solutions combined in order to solve a larger problem?

> __Note.__ Matrix multiplication is not _commutative_ (_A x B &#8800; B x A_), but it is _associative_ (_A x (B x C) = (A x B) x C)_).

> __Example.__  
> * Suppose that we want to multiply four matrices, _A x B x C x D_, of dimensions _50 x 20, 20 x 1, 1 x 10,_ and _10 x 100_, respectively.  
> * Multiplying an _m x n_ matrix by an _n x p_ matrix takes _mnp_ multiplications, to a good enough approximation.
> * The order of multiplications makes a big difference in the final running time!.  
> * _Greedy approach.__ Always perform the cheapest matrix multiplication available, leads to the second parenthesization shown here and is therefore a failter.
> * Use a binary tree.

> Parenthesization | Cost computation | Cost
> --- | --- | ---
> A x ((B x C) x D) | 20 x 1 x 10 __+__ 20 x 10 x 100 __+__ 50 x 20 x 100 | 120,200
> (A x (B x C)) x D | 20 x 1 x 10 __+__ 50 x 20 x 10 __+__ 50 x 10 x 100 | 60,200
> (A x B) x (C x D) | 50 x 20 x 1 __+__ 1 x 10 x 100 __+__ 50 x 1 x 100 | 7,000

#### What is the dynamic programming algorithm for chain-matrix multiplication? What is its running time?

> In general, we can find the minimum cost using the following __recursive algoirthm__.  
> * Take the sequence of matrices and separate it into two subsequences.
> * Find the minimum cost of multiplying out each subsequence.
> * Add these costs together, and add in the cost of multiplying the two result matrices.
> * Do this for each possible position at which the sequence of matrices can be split, and take the minimum over all of them.

> __Psudocode.__  
> ```c
> for i = 1 to n: C(i,i) = 0
> for s = 1 to n - 1:
> 	for i = 1 to n - s:
>		j = i + s
>		// splitting point k for which this is smallest
>		C(i,j) = min{C(i,k) + C(k + 1,j) + m of i-1 x m of j: i <= k < j}
> return C(1, n)
> ```

> __Run-time.__ The subproblems constitute a two-dimensional table, each of whose entries takes _O(n)_ time to compute. The overall running time is thus __O(n<sup>3</sup>)__.

#### You may be asked to compute a product of matrices using the dynamic programming approach and report the number of operations required given the dimensionality of the input matrices.

> [See Sample Problems.](exam_2_sample.md)

#### What type of subproblems does the dynamic programming approach consider for solving the longest increasing subsequence and how does it combine them in order to solve larger ones? What is the running time of the dynamic programming solution for the longest increasing subsequence problem?

> __Psudocode.__  
> ```c
> for j = 1,2, ..., n:
>	// L(j) is the length of the longest path, ending at j
> 	L(j) = 1 + max{L(i,j) element of E}
> return max of j L(j)
> ```

> __Subproblems.__  
> * We have to define a collection of subproblems {_L(j) : 1 &le; j &le; n_} with the following key property that allows them to be solved in a single pass:
> 	- There is an ordering on the subproblems, and a relation that shows how to solve a subproblem given the answers to "smaller" subproblems, that is, subproblems that appear earlier in the ordering.
> * Solved by using the relation:
> 	- L(j) = 1 + max{L(i) : (i,j) &#8712; E}

> __Run-time.__  
> * Building the graph takes _O(n)_.
> * Running _n_ subproblems to find the result takes __O(n<sup>2</sup>)__.

#### You may be given an example sequence and asked to compute its longest increasing subsequence following a dynamic programming approach. Your solution should provide the intermediate values computed by the algorithm (e.g., length of longest subsequence, previous pointer for each digit).

> [See Sample Problems.](exam_2_sample.md)

#### What are the subproblems defined by the dynamic programming approach for the longest common subsequence problem and how are they combined to solve larger problems? What is the running time of the dynamic programming solution for the longest common subsequence problem?

> __Defition.__ The _Longest Common Subsequence_ (LCS) problem is as follows. We are given two strings: string _S_ of length _n_, and string _T_ of length _m_. Our goal is to produce their longest common subsequence: the longest sequence of characters that appear __left-to-right__.

#### You may be given two strings and asked to compute their longest common subsequence following a dynamic programming approach. Your solution should provide the intermediate values computed by the algorithm (e.g., the matrix of values corresponding to the cost of the matching and the parent pointers).

> [See Sample Problems.](exam_2_sample.md)

#### What are the subproblems defined by the dynamic programming approach for the knapsack problem with repetition (or without repetition) and how are they combined to solve larger problems? What is the running time of the dynamic programming solution for the knapsack problem with repetition (or without repetition)?

> __Repetition.__  
> * Subproblems:
>	- We can either look at smaller knapsack capacities _w &le; W_, or
>	- We can look at fewer items (items _1, 2, ..., j_, for _j &le; n_)
>	- K(w) = maximum value achievable with a knapsack of capacity w
> * __Psudocode.__  
> ```c
> 	K(0) = 0
> 	for w = 1 to W:
> 		K(w) = max{K(w - wi) + vi: wi <= w}
> 	return K(W)
> ```
> * __Run-time.__
>	- This algorithm fills in a one-dimensional table of length _W + 1_, in left-to-right order.
> 	- Each entry can take up to _O(n)_ time to compute.
>	- The overall running time is __O(nW)__.

> __Without Repetition.__  
> * Subproblems:
>	- Add a second parameter due to no repetition.
>	- 0 &le; j &le; n
>	- K(w, j) = maximum value achievable using a knapsack of capacity w and item 1, ..., w.
> * Smaller subproblems:
>	- K(w, j) = max{K(w - w<sub>j</sub>, j - 1) + v<sub>j</sub>, K(w, j - 1)}
> * __Psudocode.__  
> ```c
> 	Initialize all K(0,j) = 0 and all K(w,0) = 0
>	for j = 1 to n:
>		for w = 1 to W:
>			if wj > w: K(w,j) = K(w, j - 1)
>			else: K(w,j) = max{K(w, j - 1), K(w - wj, j - 1) + wj}
>	return K(W,n)
> ```
> * __Run-time.__
>	- The algorithm consists of filling out a two-dimensional table, with _W + 1_ rows and _n + 1_ columns.
>	- Each table entry takes just constant time.
>	- The overall running time is __O(nW)__.

#### You may be given the parameters of a knapsack problem and asked to compute the answer following a dynamic programming approach (for either case: with or without repetition). Your solution should provide the intermediate values computed by the algorithm (e.g., the vector or matrix of intermediate payoffs and objects selected by the intermediate solutions).

> [See Sample Problems.](exam_2_sample.md)

#### If the input to a problem is x<sub>1</sub>, . . . , x<sub>n</sub> and the subproblems identified by a dynamic programming solution have the form x<sub>1</sub>, . . . , x<sub>i</sub> (i &le; n), how many subproblems exists? Similarly, for inputs x<sub>1</sub>, . . . , x<sub>n</sub> and y<sub>1</sub>, . . . , y<sub>m</sub>, where the subproblems are x<sub>1</sub>, . . . , , x<sub>i</sub>, (i &le; n) and y<sub>1</sub>, . . . , y<sub>j</sub>, (j &le; m). Similarly, for input x<sub>1</sub>, . . . , x<sub>n</sub> and subproblems x<sub>i</sub>, . . . , x<sub>j</sub>.

> Pikachu!

#### What are the advantages and disadvantages of an adjacency matrix representation for graphs? What are the advantages and disadvantages of an adjacency list representation for graphs?

> __Adjacency Matrix Representation.__  
> * __Advantages:__  
> 	- Finding out whether or not an edge exists is an __O(1)__ operation.
> * __Disadvantages:__  
> 	- It requires __O(v<sup>2</sup>)__ space, where _v_ is the number of vertices.
>	- In practice, many graphs are _sparse_, meaning that they have relatively few edges.

> __Adjacency List Representation.__  
> * __Advantages:__
> 	- Space required is __O(e)__, where _e_ is the number of edges.
>	- For _sparse graphs_, this representation could occupy significantly less space than an _adjacency matrix_.
> * __Disadvantage:__
> 	- Finding out whether or not a particular edge exists is an __O(e)__ operation.
>	- The list of edges would need to be searched sequentially.

## Depth-First Search

#### Provide an algorithm that discovers in linear time the set of nodes in a graph reachable from a speciﬁc node. Argue about its correctness.

> __Psudocode.__  
> ```c
> // Input: G = (V,E) is a graph; v element of V
> // Output: visited(u) is set to true for all nodes u reachable from v
> procedure explore(G,v)
> 	visited(v) = true
> 	previsit(v)
> 	for each edge (v,u) element of E:
> 		if not visited(u): explore(u)
> 	postvisit(v)
> ```

#### Provide an algorithmic description for depth-ﬁrst search. What is its running time?

> __Psudocode.__  
> ```c
> procedure dfs(G)
> 	for all v element of V:
>		visited(v) = false
> 	for all v element of V:
>		if not visited(v): explore(v)
> ```

> __Run-time.__  
> * The total work done in step 1 is _O(|v|)_.
> * The total work done in step 2 is _O(|e|)_.
> * The overall running time of the depth-first search is __O(|v| + |e|)__, linear in the size of its input.

#### What is the pre-visit and post-visit order of nodes in depth-ﬁrst search?

> __Pre-visit.__ _The moment of first discovery_.  
> ```c
> procedure previsit(v)
> 	pre[v] = clock
>	clock = clock + 1
> ```

> __Post-visit.__ _The final departure_.  
> ```c
> procedure postvisit(v)
>	post[v] = clock
>	clock = clock + 1
> ```

> __Property.__ For any nodes _u_ and _v_, the two intervals [pre(_u_),post(_u_)] and [pre(_v_),post(_v_)] are either disjoint or one is contained within the other.

#### How can depth-ﬁrst search be used in order to detect the connected components of a graph?

> __Kosaraju's Algorithm.__ Uses two passes of _depth first search_.  
> * The first, in the original graph, is used to choose the order in which the outer loop of the second depth first search tests vertices for having been visisted already and recursively explores them if not.
> * The second depth first search is on the _transpose graph_ of the original graph, and each recursive exploration finds a single new strongly connected component.

#### You may be provided an undirected or directed graph, a start node and asked to provide the search tree arising from a depth-ﬁrst search. You may also be asked to identify tree edges, forward edges, back edges and cross edges (directed cases).

> [See Sample Problems.](exam_2_sample.md)

#### Show that a directed graph has a cycle if and only if its depth-ﬁrst search reveals a back edge.

> __Proof.__ One direction is quite easy.  
> * If (u,v) is a back edge, then there is a cycle consisting of this edge together with the path from _v_ to _u_ in the search tree.

#### What is a directed acyclic graph (DAG)? What is the topological ordering of nodes in a DAG and why it is useful?

> Good for modeling relations like causalities, hierarchies, and temporal dependencies.

> __Topological Order.__ We would like if possible to linearize, to order the vertices one after the other in such a way that each edge goes from an earlier vertex to a later vertex, so that all precedence constraints are satisifed.

> __Property.__ In a _DAG_, every edge leads to a vertex with a lower post number.

> __Run-time.__ This gives us a linear-time algorithm for ordering the nodes of a _DAG_.

#### How is it possible to identify a sink node or a source node in a DAG using depth-ﬁrst search?

> Since a _DAG_ is linearized by decreasing _post numbers_, the vertex with the smallest post number comes last in this linearization, and it must be a __sink node__&#8212;no outgoing edges.

> Symmetrically, the one with the highest post is a __source node__, a node with no incoming edges.

#### What is the deﬁnition of strongly connected components? How is it possible to compute the decomposition of a directed graph into its strongly connected components? Provide an algorithm and argue about its running time.

> A directed graph is called __strongly connected__ if there is a _path_ in each direction between each pair of verticies of the graph.

> In a directed graph _G_ that may not itself be strongly connected, a pair of vertices _u_ and _v_ are said to be __strongly connected__ to each other if there is a path in each direction between them.

## Breadth-First Search

#### Provide the algorithm that performs breadth-ﬁrst search on a graph. What is the inductive argument for the correctness of the approach? What is the running time of the algorithm?

#### What is the deﬁnition of a single-source shortest path problem? What is the deﬁnition of a single-destination shortest path problem? What is the deﬁnition of a single-pair shortest path problem? What is the deﬁnition of all-pairs shortest path problem? Which of these problems are equivalent? Do we know faster algorithms for the single-pair shortest path problem than the single-source shortest path problem?

#### What is the “optimal substructure” property of shortest paths? Prove its validity.

#### What happens with shortest paths on graphs that contain negative cycles? Can a shortest path contain positive cycles?

## Dijkstra's Algorithm

#### Provide the algorithm that performs breadth-ﬁrst search on a graph. What is the inductive argument for the correctness of the approach? What is the running time of the algorithm?

#### What is the deﬁnition of a single-source shortest path problem? What is the deﬁnition of a single-destination shortest path problem? What is the deﬁnition of a single-pair shortest path problem? What is the deﬁnition of all-pairs shortest path problem? Which of these problems are equivalent? Do we know faster algorithms for the single-pair shortest path problem than the single-source shortest path problem?

#### What is the “optimal substructure” property of shortest paths? Prove its validity.

#### What happens with shortest paths on graphs that contain negative cycles? Can a shortest path contain positive cycles?

## Bellman-Ford and Floyd-Warshall Algorithm

#### Provide the algorithm that performs breadth-ﬁrst search on a graph. What is the inductive argument for the correctness of the approach? What is the running time of the algorithm?

#### What is the deﬁnition of a single-source shortest path problem? What is the deﬁnition of a single-destination shortest path problem? What is the deﬁnition of a single-pair shortest path problem? What is the deﬁnition of all-pairs shortest path problem? Which of these problems are equivalent? Do we know faster algorithms for the single-pair shortest path problem than the single-source shortest path problem?

#### What is the “optimal substructure” property of shortest paths? Prove its validity.

#### What happens with shortest paths on graphs that contain negative cycles? Can a shortest path contain positive cycles?

## Floyd-Warshall and Johnson's Algorithm

#### Provide the Floyd-Warshall algorithm for solving all-pair shortest path problems. What is the running time of the approach?

#### You may be provided a graph and asked to compute the dynamic programming matrix that arises from a few iterations of the Floyd-Warshall algorithm.

#### What is the transitive closure of a graph and how can it be computed following a dynamic programming approach? What is the relation to the Floyd-Warshall algorithm?

#### If a graph has non-negative edges, is it preferable to run the Floyd-Warshall algorithm to solve an all-pair shortest path problem or is it preferable to call |V| times Dijkstra’s algorithm?

#### What is the main idea in Johnson’s algorithm and why can it be preferable over the Floyd-Warshall algorithm when solving all-pair shortest path problems?

#### Prove the following: if we define a value h : V --> R for every vertex of a graph G(V,E) and update the weight w of a graph according to the rule: &#373;(u,v) = w(u,v) + h(u) - h(v) for every edge (u,v) &isin; E, then a path p = \< u<sub>0</sub>, v<sub>1</sub>, . . ., v<sub>k</sub> \> is a shortest path on G according to weight &#373; only if it is also a shortest path according to weights w. Futhermore, a negative cycles exist on the graph G according to the weight &#373; only if they exist for the weights w as well.

#### Given the above transformation of weights for a graph G(V, E), how should the values h be computed for the vertices of the graph so that all weights end up having non-negative values?

#### Describe Johnson’s algorithmic steps. What is its running time?
