## Exam 1 Sampling Problems

__How many digits do you need to represent a number `N` in base `b`__  
> [log<sub>b</sub>N] + 1

__Prove the following: if a &#8800; b, then log<sub>b</sub>N = &Theta;(log<sub>a</sub>N)__  
> Using the change of base formula, you can change the base of any log to another. So asymptotically, they are the same.

__If algorithm A run time is a `logarithmic function` of its input and algorithm B run time is a `linear function` of its input, which is asymptotically faster?__
> Algorithm A is faster, because logarithmic functions &gt; linear function

__Prove the following: n<sub>3</sub> = O(4<sup>log(n)</sup>)__
> 4<sup>log(n)</sup> = n<sup>log<sub>2</sub>(4)</sup> = n<sup>2</sup>
> n<sup>3</sup> = O(n<sub>2</sub>) because n<sub>3</sub> &gt; n<sub>2</sub>

__What is the security of the `RSA protocol` based on?__
> Based on the __factoring problem__, because of the difficulty of factoring the product of two large prime numbers.

__A sender sends `N` packets, where each packet has a unique ID from `1 to N`. The receiver receives all but 1 packet. How does the receiver know which packet is missing?__  
> &Sigma;<sub>sender</sub> (1 to N) - &Sigma;<sub>receiver</sub> (1 to N)
