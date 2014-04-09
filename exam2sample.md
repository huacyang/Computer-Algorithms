#### An adjacency matrix representation can quickly detect if an edge exists but the representation requires _O(|V|<sup>3</sup>)_ space (i.e. _O|V|<sup>2</sup>_) for each vertex). An adjacency list has smaller space requirements [_O(V * log|V|)_ in general] but detecting edge existence is not constant time.

#### Consider a general graph G(V,E). The best known algorithm for finding a path from a specific vertex _s_ to a specific vertex _t_ in _G_ has better asymptotic running time (i.e. is faster) than the best known algorithm for finding the paths from all the vertices in _V_ to a vertex _t_ in _G_.

#### A shortest path cannot possibly contain a zero-weight cycle.

> __False.__  
> The shortest path algorithm can have zero-weight cycle. They are simply ignored by the algorithm, so that the shortest paths they find have no cycles.

#### Dijkstra's running time depends on the implementation of the priority queue data structure. An array implementation results in a running time of _O(|V|<sup>2</sup>)_ and is preferred in dense graphs. A binary heap implementation results in _O(|V|log|V| + |E|)_ and is preferred in sparse graphs.

> __False.__  
> A binary heap results in _O((|V| * |E|) log|V|).

> __Side-note.__  
> * You use __simple array__ if its dense and __binary heap__ if its sparse.
> * A simple array results in _O(|V|<sup>2</sup>)_.

#### On a sparse graph with non-negative edges it is preferable to run |V| times Dijkstra's algorithm using a binary heap in order to compute the shortest paths between all pairs of nodes than running Floyd-Warshall's algorithm, which has a running time of _&Theta;(|V|<sup>3</sup>)_.

> __True.__  
> * Sparse graph with binary heap will give a better complexity than Floyd-Warshall's algorithm.
> * Dijkstra's with Binary heap = __O(|V|<sup>2</sup>log|V|)__
> * Floyd-Warshall's = __O(|V|<sup>3</sup>)__

#### You are transferring (or robbing...) money from a bank and you have already filled _n_ duffel bags with case. Each duffel bag _i_ is unique, contains a known amount of money _m<sub>j</sub>_ and has a known volume _v<sub>i</sub>_. You are trying to fit the bags in the trunk of your car which has volume _V_, so as to maximize the amount of money that you can transfer in one trip. Provide a dynamic programming solution to this problem (i.e. identify the subproblems and show how are they combined to solve larger problems).

> __Subproblems.__  
> For the problem we can take volume _V_ (volume of the trunk) using a matrix our subproblems.  
> * When _v = 0_, what's the max amount of money I can take and with which bags (V=1, v=2, ..., v).
> * Since each bag is unique, we can't repeat any bags, so we need an additional variable to keep track the volume of the bags, the variable will also be part of our optimal solution.

> __Solution.__  
> ```c
> if (v<sub>i</sub> &gt; V)
>	K(i,v) = K(v, i-1)
> else
>	K(i,v) = max[K(v,i-1), k(v-v<sub>i</sub>, i-1 + v<sub>i</sub>)]
> return K(v,i)
> ```

> __Side-note.__  
> * This is the Knapsack problem without repetition.

#### What is the running time of the dynamic programming solution for the above problem and why?

> __O(nV)__

> Since we defined our subproblems according to  
> * V = the volume of the trunk
> * n = the amount of the bags we have

#### A subsequence is palindromic if it is the same whether read left to right or right to left. For instance, the sequence: A,C,G,T,G,T,C,A,A,A,A,T,C,G has many palindromic subsequences, including A,C,G,C,A and A,A,A,A (on the other hand, the subsquence A,C,T is not palindromic). Devise an algorithm that takes a sequence x[1,...,n] and returns the length of the longest palindromic subsequence. Its running time should be _O(n<sub>2</sub>)_.

> Apply the __longest common subsequence algorithm__.  
> * We have sequence S and T (S reversed).

> ```
> for i=0 to n
>	LPS[i,0] = 0
> for j=0 to n
>	LPS[0,j] = 0
>
> for i=1 to n
> 	for j=1 to n
>		if [Si == Ti]
>			LPS[i,j] = LPS[i-1,j-1]
>		else
>			LPS[i,j] = max[LPS(i-1,j), LPS(i,j-1)]
> return LPS[n,n]
> ```

#### Provide the depth-first search tree for the given graph below, starting from node 0. Break ties by visiting first nodes that have a smaller index. Indicate the pre-visit and post-visit order for each node on the given table.

![depth-first search graph](img/breath-first-search-graph.png)






