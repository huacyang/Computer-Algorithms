## Exam 1 Review

__Give a justiﬁcation why improvements in hardware are typically not sufﬁcient to make an algorithm with exponential running time reasonably tractable.__  
> The algorithm will be so slow that even massive improvements in hardware won't have a useful impact.  
> Exponential growth (running time) > multiplication growth (Moore's Law)

__We have 3 algorithms for the same problem where the ﬁrst runs in `exponential time`, the second in `logarithmic time` and the third in `linear time` as a function of the same input. Which algorithm do you prefer to use?__  
> logarithmic time &gt; linear time &gt; Exponential time  

__You may be provided running times of different algorithms and asked to show which running time dominates asymptotically__    
> See [Asymptotic Notation](laws.md#asymptotic-notation) 

__Provide the definition of `Big-O`, `Omega`, and `Theta`.__  
> * __O-notation__ is the `asymptotic upper bound`  
> * __&Omega;-notation__ is the `asymptotic lower bound`  
> * __&Theta;-notation__ asymptotically bounds a function from `above and below`  
> * _f(n) = O(g(n))_ __imply__ f(n) > g(n)  
> * _f(n) = &Omega;(g(n))_ __imply__ f(n) < g(n)  
> * _f(n) = &Theta;(g(n))_ __imply__ f(n) = g(n)  

> See [Asymptotic Notation](laws.md#asymptotic-notation) 

__You may be provided certain statements about asymptotic analysis of running times and asked to show if they are correct or not. For instance: “n<sup>a</sup> dominates n<sub>b</sub> if a > b”.__ 
> See [Asymptotic Notation](laws.md#asymptotic-notation) 

__What is the “primality” problem and what is the “factoring” problem? Which one of the two is tractable? What are the advantages of the intractability of the other problem?__  
> * __Primality__ : determing whether a number is a prime or not.  
> * __Factoring__ : given a number _n_, express it as a product of its prime factors.  
> * __Primality__ is tractable whereas __factoring__ is intractable.  

> See [Primality](laws.md#primality) 

__How many digits do you need to represent a number `N` in base `b`__  
> [log<sub>b</sub>N] + 1

