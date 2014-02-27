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
> &lfloor;log<sub>b</sub>N&rfloor; + 1

__How much does the size of the representation of a number changes when we change bases?__

__What is the running time of the addition operation for two _n_-bit numbers (think in terms of bit complexity)?__

__What is the running time of the traditional multiplication operation taught in grade school for two _n_-bit numbers (think in terms of bit complexity)?__

__Provide a recursive formula for the multiplication of two numbers.__

__What is the complexity of modular addition and modular multiplication for two _n_-bit numbers?__

__Give a private key protocol for a cryptography application. Given an example of how it can be compromised.__

__RSA is based on which basic property of modulo arithmetic?__

__RSA is based on which basic property of modulo arithmetic?__

__What are the basic operations that need to be performed according to the RSA protocol and what is their running time?__

__You may be provided an example message and asked to describe the operations of the RSA protocol on it.__

__What does Fermat’s Little Theorem specify? Prove it.__

__What is the importance of Fermat’s little theorem in the RSA protocol?__

__How can we efﬁciently perform modular exponentiation? What is the running time of the approach?__

__What does Euclid’s rule specify? Prove it.__

__What is Euclid’s algorithm for ﬁnding the greatest common divisor? What is its running time and why?__

__Show that if _d_ divides both _a_ and _b_, and _d = a &times; x + b &times; y_ for some integers _x_ and _y_, then _d = gcd(a, b)_.__

__What is the extended Euclid’s algorithm for ﬁnding the greatest common divisor d of two numbers _a_ and _b_, as well as numbers _x_ and _y_, so that _d = a &times; x + b &times; y_? Prove its correctness (you will need to prove Euclid’s algorithm ﬁrst and then the extension)__

__When does the multiplicative inverse of a number _x_ exists modulo _N_ and why?__

__How can you compute the multiplicative inverse modulo _N_ for two relative prime numbers? What is the running time of the corresponding algorithm?__
