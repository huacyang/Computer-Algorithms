## Exam 1 Review

__Give a justiﬁcation why improvements in hardware are typically not sufﬁcient to make an algorithm with exponential running time reasonably tractable.__
> The algorithm will be so slow that even massive improvements in hardware won't have a useful impact. Exponential growth (running time) > multiplication growth (Moore's Law).

__We have 3 algorithms for the same problem where the ﬁrst runs in _exponential time_, the second in _logarithmic time_ and the third in _linear time_ as a function of the same input. Which algorithm do you prefer to use?__
> __logarithmic time__ &gt; __linear time__ &gt; __Exponential time__

__You may be provided running times of different algorithms and asked to show which running time dominates asymptotically__
> See [Asymptotic Notation](laws.md#asymptotic-notation) 

__Provide the definition of _Big-O_, _Omega_, and _Theta_.__
>	* __O-notation__ is the `asymptotic upper bound`
>		* _f(n) = O(g(n))_ __imply__ f(n) > g(n)
>	* __&Omega;-notation__ is the `asymptotic lower bound`
>		* _f(n) = &Omega;(g(n))_ __imply__ f(n) < g(n)
>	* __&Theta;-notation__ asymptotically bounds a function from `above and below`
>		* _f(n) = &Theta;(g(n))_ __imply__ f(n) = g(n)

> See [Asymptotic Notation](laws.md#asymptotic-notation)

__You may be provided certain statements about asymptotic analysis of running times and asked to show if they are correct or not. For instance: “n<sup>a</sup> dominates n<sup>b</sup> if a > b”.__ 
> See [Asymptotic Notation](laws.md#asymptotic-notation) 

__What is the “primality” problem and what is the “factoring” problem? Which one of the two is tractable? What are the advantages of the intractability of the other problem?__
> __Primality Testing Problem__ (_PTP_): Given a positive integer greater than 1, determine whether or not it is prime.

>	* This problem can be solved by the _AKS_ algorithm deterministically and unconditionally in _O(log(n))_.
>	* _PTP_ is `tractable`

> __Integer Factorization Problem__ (_IFP_): Given a positive integer _n &gt; 1_, find a factor _1 &lt; a &lt; n_ of _n_ such that _n = ab_ for _1 &lt; b &lt; n_.

>	* _IFP_ is `intractable`

> See [Primality](laws.md#primality) 

__How many digits do you need to represent a number _N_ in base _b_?__
> &lfloor;log<sub>b</sub>N&rfloor; + 1

__How much does the size of the representation of a number changes when we change bases?__
>	* Recall the rule for converting [Logarithms](laws.md#Logarithm) from base _a_ to base _b_:
>		* _log<sub>b</sub>N = (log<sub>a</sub>N)/(log<sub>a</sub>b)_
>		* _log<sub>b</sub>N = (log<sub>a</sub>N) &times; 1/(log<sub>a</sub>b)_
>		* _log<sub>b</sub>N = (log<sub>a</sub>N) &times;_ constant
>	* The size of integer _N_ in base _a_ is the same as its size in base _b_, times a constant factor _log<sub>a</sub>b_. 
>	* In big-_O_ notation, the base (a constant in this case) is irrelevant. Therefore we write the size simply as __O(log N)__.

__What is the running time of the addition operation for two _n_-bit numbers (think in terms of bit complexity)?__
>	* For adding two binary representations, the maximal number of bit operations for the sum is _n_ additions with carries. At most _2n_ bit operations are used to perform the addition of two _n_-bit integers.
>	* Run-time is _O(2n)_ = __O(n)__.

> See [Arithmetic](laws.md#arithmetic) 

__What is the running time of the traditional multiplication operation taught in grade school for two _n_-bit numbers (think in terms of bit complexity)?__
>	* The grade-school algorithm for multiplying two _n_-bit binary numbers _x_ and _y_ consists of adding together _n_ copies of _x_, each appropriately left-shifted. Each copy, when shifted, is at most _2n_ bits long.
>	* Run-time is __O(n<sup>2</sup>)__.

> See [Arithmetic](laws.md#arithmetic) 

__Provide a recursive formula for the multiplication of two numbers.__
> __function multiply(x, y)__

>	* `Input` two n-bit integers x and y, where y &ge; 0
>	* `Output` the product
>	* if _y = 0_: return _0_
>	* _z =_ multiply(_x, &lfloor;y/2&rfloor;_)
>	* if _y_ is even:
>		* return _2z_
>	* else:
>		* return _x + 2z_

> Run-time is __O(n<sup>2</sup>)__

> See [Arithmetic](laws.md#arithmetic) 

__What is the complexity of modular addition and modular multiplication for two _n_-bit numbers?__
>	* The complexity of `modular addition` is __O(n)__ (linear),
>		* where _n = &lceil;log N&rceil;_ is the size of _N_
>	* The complexity of `modular multiplication` is __O(n<sup>2</sup>)__ (quadratic),
>		* to compute _x &times; y mod N_, multiply (quadratic) then divide (quadratic) to get the remainder.

> See [Modular Arithmetic](laws.md#modular-arithmetic) 

__Give a private key protocol for a cryptography application. Given an example of how it can be compromised.__
> In a __private key protocol__, both the sender and receiver meet beforehand and together choose a secret codebook, with which they encrypt all future correspondence between them. 

> In order to compromise the encrypted message without the secret key _d(x)_, you would have to collect some encoded messages and use them to at least partially figure out the codebook.

> See [Cryptography](laws.md#cryptography) 

__RSA is based on which basic property of modulo arithmetic?__
> Modern cryptography is about the following important idea: __factoring is hard and primality is easy__. We cannot factor large numbers, but we can easily test huge numers for primality!

__What are the basic operations that need to be performed according to the Rivest-Shamir-Adleman (_RSA_) protocol and what is their running time?__
> 1. Start by picking two large _n_-bit random primes _p_ and _q_
> 2. 

> Run-time is _O(n<sup>2</sup>)_

__You may be provided an example message and asked to describe the operations of the RSA protocol on it.__
> See [Practice Midterm](exam_one_sample.md)

__What does Fermat’s Little Theorem specify? Prove it.__ 
> If _p_ is prime, then for every _1 &le; a &lt; p_, __a<sup>p-1</sup> &equiv; 1 (mod p)__

> For proof, see [Primality](laws.md#primality)

__What is the importance of Fermat’s little theorem in the RSA protocol?__
> The __Fermat's little theorem__ is needed in the proof of correctness of the _RSA_ algorithm. 

__How can we efﬁciently perform modular exponentiation? What is the running time of the approach?__
> We can do better by starting with _x_ and __squaring repeatedly__ modulo _N_ 

> `x mod N -> x^2 mod N -> x^4 mod N -> x^8 mod N -> ... -> x^(2*floor(log y)) mod N`  

> Each takes just O(log<sup>2</sup> N) time to compute, and in this case there are only _log y_ multiplications.

> The running time of this approach is __O(n<sup>2</sup>)__.

__What does Euclid’s rule specify? Prove it.__
> Given two integers _a_ and _b_, it finds the largest integer that divides both of them, known as their __greatest common divisor__ (_gcd_).

> For proof, see [Modular Exponentiation](laws.md#modular-exponentiation)

__What is Euclid’s algorithm for ﬁnding the greatest common divisor? What is its running time and why?__
> __Euclid's rule__:  
> if _x_ and _y_ are positive integers with _x &ge; y_, then _gcd(x,y) = gcd(x mod y, y)_

> __Run-time__:  
> If _x_ and _y_ are _n_-bit integers, then the base case will be reached within _2n_ recursive calls. Each call involves a quadratic-time division (_x mod y_), the total run-time is __O(n<sup>3</sup>)__.

__Show that if _d_ divides both _a_ and _b_, and _d = ax + by_ for some integers _x_ and _y_, then _d = gcd(a, b)_.__
> __Let d = gcd(a, b)__  

>	* __by definition:__ there exist integers _a&prime;_ and _b&prime;_  
>		* such that _a = a&prime;d_ and _b = b&prime;d_  
>	* __by substitution:__ _a&prime;dx + b&prime;dy = d_  
>	* __by dividing _d_:__ _a&prime;x + b&prime;y = 1_  

> __Let e = gcd(x, y)__  

>	* __by definition:__ there exist integers _x&prime;_ and _y&prime;_  
>		* such that _x = ex&prime;_ and _y = ey&prime;_  
>	* __by substitution:__ _a&prime;ex&prime; + b&prime;ey&prime; = 1_  
>	* __by reduction:__ _e(a&prime;x&prime; + b&prime;y&prime;) = 1_  
>		* since _a&prime;x&prime; + b&prime;y&prime;_ is an integer  
>	* __by implication:__ _e = 1_ or _e = -1_  
>	* __by definition:__ _e = 1_ (gcd must be positive)

__What is the extended Euclid’s algorithm for ﬁnding the greatest common divisor _d_ of two numbers _a_ and _b_, as well as numbers _x_ and _y_, so that _d = ax + by_? Prove its correctness (you will need to prove Euclid’s algorithm ﬁrst and then the extension)__

__When does the multiplicative inverse of a number _x_ exists modulo _N_ and why?__
> The __multiplicative inverse__ exists when _gcd(a, N) &le; 1_

> __Let _a_ and _N_ be even numbers__

>	* then _a_ mod _N_ is always even
>		* since _a_ mod _N = a - kN_ for some _k_
>		* we can be certain that _gcd(a, N)_ divides _ax mod N_, because it can be rewritten as: _ax + kN_
>	* so if _gcd(a, N) > 1_, then _ax &#8800; 1_ mod _N_
>		* no matter what _x_ might be
>	* therefore, _a_ cannot have a multiplicative inverse modulo N

> See [Modular Arithmetic](laws.md#modular-arithmetic)

__How can you compute the multiplicative inverse modulo _N_ for two relative prime numbers? What is the running time of the corresponding algorithm?__
> Ain't got any clue @_@  
> Run-time is __O(n<sup>3</sup>)__

__Describe a test for evaluating whether a number is prime. What is the probability of this test returning the correct answer and why? Can you increase the probability of success for this test?__
> You can use __Fermat’s Little Theorem__ and its probability for returning the correct answer is _1/n_ where _n_ is the number of bits in _N_.

> To decrease the error use larger numbers because as the numbers increase the chance that the number generated by Fermat’s or number that passed Fermat’s is going to be prime. In other words as _1/n_ approaches infinity = _0_

__What does Lagrange’s Prime Number Theorem specify and why is it helpful for primality testing?__
> __Lagrange’s Prime Number Theorem__ specifies the number of primes less than a certain number _x_. Can accurately test whether a number is prime or not.

> This is helpful because we want to see the probability that an _n_-bit number is really prime. Helps us understand the prob that a number is prime and that by increasing the number of bits we increase the chance that a number is prime.

__What properties should a good hash function provide?__
> Hash functions should be random and consistent at the same time. In other words random so it scatters the data around evenly distributing across the structure and consistent so we get the same result everytime we apply it. The distribution should be uniform so that space is not wasted.

__What is the property of universal hashing families of functions? Provide a universal hashing family of functions for an example problem and prove the corresponding property__
> 1. Choose the number of buckets _n_ to be a prime number
> 2. Every entry _x_ has to be a quadruple
> 3. Now map each entry _x_ to the bucket that corresponds to _x_ mod _N_
> 4. The probability of collision of any of these entries therefore is just _1/number_ of buckets or _1/n_

__What are the basic principles of divide-and-conquer algorithms?__
>	* Breaking the problem into sub-problems that are themselves smaller instances of the same type of problem.
>	* Recursively Solving these subproblems
>	* Appropriately combining their answers

__Describe an approach for multiplication of two n-bit numbers that has a better running time than O(n<sup>2</sup>). Prove its running time__
>	* Using Gauss’s you can multiply two n-bit numbers faster.
>	* This splits the two into two parts
>	* Total runtime is __O(n<sup>log<sub>2</sub>3</sup>)__ which is about __O(n<sup>1.5</sup>)__, which is faster than the _O(n<sup>2</sup>)_ runtime we had before.

__What does the Master theorem specify? Prove it.__
> Used to analyse __recursive / recurrences__ (black box for solving recurrences)

> Three run-times associated with this theorem:

>	* __b__ is the factor by which the input size shrinks from recursion
>	* __d__ is the amount of work done outside of the recursive calls
>	* These are all independent on the input size n
>	* Three cases are listed below:
>		* _O(nd * log(n))_ if _a = bd_
>		* _O(nd)_ if _a < bd_
>		* _O(nlogb(a))_ if _a > bd_

> The general formula for this method is the following:  
> &emsp;__T(n) &le; aT(n/b) + O(n<sup>d</sup>)__

__You may be provided a divide-and-conquer algorithm and asked to argue about its running time by using the Master theorem.__
> Pikachu!

__How does mergesort work, what is its running time and why? How does the iterative version of mergesort work?__
>	* Splits a list in half and recursively sorts each half, then merges the halves back together.
>	* Run-time is __O(nlog(n))__
>	* The iterative version of merge sort works by having a set of active arrays that are merged into pairs to give the next batch of active arrays.
>	* These arrays can be organized in a queue and processed by repeatedly removing two arrays merging them and putting the result in the end of the queue.

__What are comparison sorting algorithms? What is the lower limit for the running time of comparison sorting algorithms?__
> Compares a list of numbers by determining which number is greater than the other and switch.

> &lceil;log<sub>2</sub>n!&rceil;

__How does quick-sort work? When does the worst-case running time arise? When does the best-case running time arise?__
> Sorts in place  

> __Worst Case__ occurs when the list is already sorted.  
> Average runtime is __O(n2)__

> __Best Case__ occurs when the partitioning splits evenly _n/2_ and _n/2-1_  
> Average runtime is __O(nlog(n))__ 

__Provide a rigorous proof for the worst-case performance of quick-sort.__
> Pikachu!

__Provide a rigorous proof for the expected running time of quick-sort.__
> Pikachu!

__How can we efﬁciently compute the median of a set of numbers? What is the running time of this solution?__
>	* Randomly choose a number from the split arrays and determine if it is the middle number.
>	* On each iteration we shrink the array by a certain number of elements
>	* On average this will produce a result after __O(n)__ iterations.

__What is the main idea behind counting sort? Provide a description of the algorithm and argue about its running time.__
> It is an integer sorting algorithm that sorts based on integer keys. This algo takes _O(k+n)_ runtime where _k_ is the outer and _n_ is the inner loop

__What is the main idea behind radix sort? Provide a description of the algorithm and argue about its running time__
> Sorting the data with integer keys and sorting by the significant value

> __Worst Case__  
> Average runtime is __O(kn)__

__Prove the correctness of radix sort.__
> Pikachu!

__What is the main idea behind bucket sort? Provide a description of the algorithm. Prove its running time__
> Partitions an array into a certain number of buckets. Then the buckets are sorted using another sorting algorithm. 

> __Worst Case__  
> Average runtime is __O(n<sup>2</sup>)__

> __Best Case__  
> Average runtime is __O(n + k)__

__What is the main principle behind greedy algorithms?__
> Build up a solution peice by peice always choosing the next piece that offers the most obvious benefit. 

__Why does the greedy algorithm work for the coin changing problem given the US coin system?__
> Determines the min number of coins to give when providing change. This works because it will select the highest coin without going over the needed change. Less than the current amount owed.

__What is the idea in Huffman encoding in order to achieve data compression? What is the preﬁx-free property?__
>	* Used for data compression using a data table to keep track of the elements and a tree to access the elements
>	* Sample at regular intervals yielding a sequence of real numbers
>	* Each real-valued sample is quantized approximated by a nearby number from a finite set. 
>	* The resulting string of length _T_ over alphabet _j_ is encoded in binary
>	* Therefore we use a prefix tree to do the encoding of the data which is represented by a full binary tree
>	* Takes __O(nlog(n))__ to create the huffman tree

__Provide the Huffman encoding algorithm and argue its running time.__
> Pikachu!

__Prove the greedy choice property for the Huffman encoding algorithm (ﬁrst lemma).__
> Achieve a min weighted path, but each weighted keyword but be less than some constant.  This takes __O(nL)__ where _L_ is the length of the keyword. This however will take more time than a typical huffman coding.

__Prove the optimal substructure property for the Huffman encoding algorithm (second lemma).__
> Must use a binary tree in order to get the optimal result , the alphabetical order of inputs and outputs must be identical.

