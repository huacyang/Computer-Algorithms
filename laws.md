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
