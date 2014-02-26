__What is the number of bits needed to represent number N in base b?__  
[log<sub>b</sub>N] + 1

__Prove the following: if a &#8800; b, then log<sub>b</sub>N = &Theta;(log<sub>a</sub>N)__  
Using the change of base formula, you can change the base of any log to another. So asymptotically, they are the same. (See [[Asymptotic Notation|#Asymptotic Notation]])

__A sender sends `N` packets, where each packet has a unique ID from `1 to N`. The receiver receives all but 1 packet. How does the receiver know which packet is missing?__  
&Sigma;<sub>sender</sub> (1 to N) - &Sigma;<sub>receiver</sub> (1 to N)

# Asymptotic Notation

* f(n) = O(f(n))
* if (f)
* log<sub>a</sub>N = &Theta;(log<sub>b</sub>N) if a,b > 1

