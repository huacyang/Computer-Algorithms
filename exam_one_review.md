## Asymptotic Notation

* f(n) = O(f(n))
* __if__ f(n) = O(g(n)) __and__ g(n) = O(h(n)) __then__ f(n) = O(h(n)) 
* f(n) = O(g(n)) __iff__ g(n) = &Omega;(f(n))
* f(n) = &Theta;(g(n)) __iff__ g(n) = &Theta;(f(n))
* log<sub>a</sub>N = &Theta;(log<sub>b</sub>N) __if__ a,b > 1
* a<sup>n</sup> &#8800; &Theta;(b<sup>n</sup>) __if__ a &#8800; b

## Logarithm

* log<sub>b</sub>(xy) = log<sub>b</sub>(x) + log<sub>b</sub>(y)
* log<sub>b</sub>(x/y) = log<sub>b</sub>(x) - log<sub>b</sub>(y)
* log<sub>b</sub>(x<sup>n</sup>) = n log<sub>b</sub>x
* log<sub>b</sub>(x) = log<sub>a</sub>x / log<sub>a</sub>b
* x<sup>log(n)</sup> = n<sup>log(x)</sup>

## Practice Problems

__Give a justiﬁcation why improvements in hardware are typically not sufﬁcient to make an algorithm with exponential running time reasonably tractable.__  
> The algorithm will be so slow that even massive improvements in hardware won't have a useful impact.  
> Exponential growth (running time) > multiplication growth (Moore's Law)

__We have 3 algorithms for the same problem where the ﬁrst runs in `exponential time`, the second in `logarithmic time` and the third in `linear time` as a function of the same input. Which algorithm do you prefer to use?__  
> Exponential time &gt; logarithmic time &gt; linear time

__You may be provided running times of different algorithms and asked to show which running time dominates asymptotically__  
> See [Asymptotic Notation](## Asymptotic_Notation)  
> See [Asymptotic Notation](##Asymptotic_Notation)  
> See [Asymptotic Notation](## AsymptoticNotation)  
> See [Asymptotic Notation](##Asymptotic Notation) 

__Provide the definition of `Big-O`, `Omega`, and `Theta`.__  
> 

__You may be provided certain statements about asymptotic analysis of running times and asked to show if they are correct or not. For instance: “n<sup>a</sup> dominates n<sub>b</sub> if a > b”.__  
> 

__What is the “primality” problem and what is the “factoring” problem? Which one of the two is tractable? What are the advantages of the intractability of the other problem?__  
> 

__How many digits do you need to represent a number `N` in base `b`__  
> [log<sub>b</sub>N] + 1

