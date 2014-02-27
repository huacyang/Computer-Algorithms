## Exam 1 Review

__Give a justiﬁcation why improvements in hardware are typically not sufﬁcient to make an algorithm with exponential running time reasonably tractable.__  
> The algorithm will be so slow that even massive improvements in hardware won't have a useful impact. Exponential growth (running time) > multiplication growth (Moore's Law).

__We have 3 algorithms for the same problem where the ﬁrst runs in _exponential time_, the second in _logarithmic time_ and the third in _linear time_ as a function of the same input. Which algorithm do you prefer to use?__  
> `logarithmic time` &gt; `linear time` &gt; `Exponential time`  

__You may be provided running times of different algorithms and asked to show which running time dominates asymptotically__    
> See [Asymptotic Notation](laws.md#asymptotic-notation) 

__Provide the definition of _Big-O_, _Omega_, and _Theta_.__  
><dl>
>	<dt>__O-notation__ is the `asymptotic upper bound`</dt>
>	<dd>_f(n) = O(g(n))_ __imply__ f(n) > g(n)</dd>
>	<dt>__&Omega;-notation__ is the `asymptotic lower bound`</dt>
>	<dd>_f(n) = &Omega;(g(n))_ __imply__ f(n) < g(n)</dd>
>	<dt>__&Theta;-notation__ asymptotically bounds a function from `above and below`</dt>
>	<dd>_f(n) = &Theta;(g(n))_ __imply__ f(n) = g(n)</dd>
></dl>

> See [Asymptotic Notation](laws.md#asymptotic-notation)


__You may be provided certain statements about asymptotic analysis of running times and asked to show if they are correct or not. For instance: “n<sup>a</sup> dominates n<sup>b</sup> if a > b”.__ 
> See [Asymptotic Notation](laws.md#asymptotic-notation) 

__What is the “primality” problem and what is the “factoring” problem? Which one of the two is tractable? What are the advantages of the intractability of the other problem?__  
><dl>
>	<dt>__Primality Testing Problem__ (_PTP_): Given a positive integer greater than 1, determine whether or not it is prime.</dt>
>	<dd>This problem can be solved by the _AKS_ algorithm deterministically and unconditionally in _O(log(n))_. _PTP_ is `tractable`</dd>
>	<dt>__Integer Factorization Problem__ (_IFP_): Given a positive integer _n &gt; 1_, find a factor _1 &lt; a &lt; n_ of _n_ such that _n = ab_ for _1 &lt; b &lt; n_.</dt>
>	<dd>_IFP_ is `intractable`</dd>
></dl>

> See [Primality](laws.md#primality) 

__How many digits do you need to represent a number _N_ in base _b_?__  
> &lfloor;log<sub>b</sub>N&rfloor; &plus; 1

__How much does the size of the representation of a number changes when we change bases?__  
><dl>
>	<dt>Recall the rule for converting [Logarithms](laws.md#Logarithm) from base _a_ to base _b_:</dt>
>	<dd>_log<sub>b</sub>N = (log<sub>a</sub>N)/(log<sub>a</sub>b)_</dd>
>	<dd>_log<sub>b</sub>N = (log<sub>a</sub>N) &times; 1/(log<sub>a</sub>b)_</dd>
>	<dd>_log<sub>b</sub>N = (log<sub>a</sub>N) &times;_ constant</dd>
>	<dt>The size of integer _N_ in base _a_ is the same as its size in base _b_, times a constant factor _log<sub>a</sub>b_.</dt> 
>	<dt>In big-_O_ notation, the base (a constant in this case) is irrelevant.</dt>
>	<dd>Therefore we write the size simply as __O(log N)__.</dd>
></dl>

__What is the running time of the addition operation for two _n_-bit numbers (think in terms of bit complexity)?__  
><dl>
>	<dt>For adding two binary representations, the maximal number of bit operations for the sum is _n_ additions with carries. At most _2n_ bit operations are used to perform the addition of two _n_-bit integers.</dt>
>	<dd>Run-time is _O(2n)_ = __O(n)__.</dd>
></dl>

> See [Arithmetic](laws.md#arithmetic) 

__What is the running time of the traditional multiplication operation taught in grade school for two _n_-bit numbers (think in terms of bit complexity)?__  
><dl>
>	<dt>The grade-school algorithm for multiplying two _n_-bit binary numbers _x_ and _y_ consists of adding together _n_ copies of _x_, each appropriately left-shifted. Each copy, when shifted, is at most _2n_ bits long.</dt>
>	<dd>Run-time is __O(n<sup>2</sup>)__.</dd>
></dl>

> See [Arithmetic](laws.md#arithmetic) 

__Provide a recursive formula for the multiplication of two numbers.__  
><dl>
>	<dt>__function multiply(x, y)__</dt>
>	<dt>`Input` two n-bit integers x and y, where y &ge; 0</dt>
>	<dt>`Output` the product</dt>
>		<dd>if _y = 0_: return _0_</dd>
>		<dd>_z =_ multiply(_x, &lfloor;y/2&rfloor;_)</dd>
>		<dd>if _y_ is even:</dd>
>		<dd>&nbsp;&nbsp;&nbsp;&nbsp;return _2z_</dd>
>		<dd>else:</dd>
>		<dd>&nbsp;&nbsp;&nbsp;&nbsp;return _x &plus; 2z_</dd>
>	<dt>`Run-time` is __O(n<sup>2</sup>)__</dt>
></dl>

> See [Arithmetic](laws.md#arithmetic) 

__What is the complexity of modular addition and modular multiplication for two _n_-bit numbers?__  
><dl>
>	<dt>The complexity of `modular addition` is __O(n)__ (linear),</dt>
>		<dd>where _n = &lceil;log N&rceil;_ is the size of _N_</dd>
>	<dt>The complexity of `modular multiplication` is __O(n<sup>2</sup>)__ (quadratic),</dt>
>		<dd>to compute _x &times; y mod N_, multiply (quadratic) then divide (quadratic) to get the remainder:</dd>
></dl>

> See [Modular Arithmetic](laws.md#modular-arithmetic) 

__Give a private key protocol for a cryptography application. Given an example of how it can be compromised.__  
> In a __private key protocol__, both the sender and receiver meet beforehand and together choose a secret codebook, with which they encrypt all future correspondence between them. 

> In order to compromise the encrypted message without the secret key _d(x)_, you would have to collect some encoded messages and use them to at least partially figure out the codebook.

> See [Cryptography](laws.md#cryptography) 

__RSA is based on which basic property of modulo arithmetic?__  
> Modern cryptography is about the following important idea: __factoring is hard and primality is easy__. We cannot factor large numbers, but we can easily test huge numers for primality!

__What are the basic operations that need to be performed according to the Rivest-Shamir-Adleman (_RSA_) protocol and what is their running time?__

__You may be provided an example message and asked to describe the operations of the RSA protocol on it.__  
> See [Practice Midterm](exam_one_sample.md)

__What does Fermat’s Little Theorem specify? Prove it.__ 
><dl> 
>	<dt>If _p_ is prime, then for every _1 &le; a &lt; p_,</dt>
>		<dd>_a<sup>p-1</sup> &equiv; 1_ (mod _p_)</dd>
></dl>

> For proof, see [Primality](laws.md#primality)

__What is the importance of Fermat’s little theorem in the RSA protocol?__

__How can we efﬁciently perform modular exponentiation? What is the running time of the approach?__

__What does Euclid’s rule specify? Prove it.__

__What is Euclid’s algorithm for ﬁnding the greatest common divisor? What is its running time and why?__

__Show that if _d_ divides both _a_ and _b_, and _d = a &times; x &plus; b &times; y_ for some integers _x_ and _y_, then _d = gcd(a, b)_.__

__What is the extended Euclid’s algorithm for ﬁnding the greatest common divisor d of two numbers _a_ and _b_, as well as numbers _x_ and _y_, so that _d = a &times; x &plus; b &times; y_? Prove its correctness (you will need to prove Euclid’s algorithm ﬁrst and then the extension)__

__When does the multiplicative inverse of a number _x_ exists modulo _N_ and why?__

__How can you compute the multiplicative inverse modulo _N_ for two relative prime numbers? What is the running time of the corresponding algorithm?__
