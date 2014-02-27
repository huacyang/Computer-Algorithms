## Asymptotic Notation

__&Theta;-notation__

* _f(n) = &Theta;(g(n))_ __and__ _g(n) = &Theta;(h(n))_ __imply__ _f(n) = &Theta;(h(n))_
* _f(n) = &Theta;(g(n))_ __is like__ _a = b_
* Proof: _f(n) = &Theta;(g(n))_
	* there exist positive constants _c<sub>1</sub>_, _c<sub>2</sub>_, and _n<sub>0</sub>_
	* such that _0 &le; c<sub>1</sub>g(n) &le; f(n) &le; c<sub>2</sub>g(n)_ for all _n &ge; n<sub>0</sub>_

__O-notation__

* _f(n) = O(g(n))_ __and__ _g(n) = O(h(n))_ __imply__ _f(n) = O(h(n))_
* _f(n) = O(g(n))_ __is like__ _a &le; b_
* Proof: _f(n) = O(g(n))_
	* there exist positive constants _c_ and _n<sub>0</sub>_
	* such that _0 &le; f(n) &le; cg(n) for all n &ge; n<sub>0</sub>_

__&Omega;-notation__

* _f(n) = &Omega;(g(n))_ __and__ _g(n) = &Omega;(h(n))_ __imply__ _f(n) = &Omega;(h(n))_
* _f(n) = &Omega;(g(n))_ __is like__ _a &ge; b_
* Proof: _f(n) = &Omega;(g(n))_
	* there exist positive constants _c_ and _n<sub>0</sub>_
	* such that _0 &le; cg(n) &le; f(n) for all n &ge; n<sub>0</sub>_

## Logarithm

* _log<sub>b</sub>(xy) = log<sub>b</sub>(x) + log<sub>b</sub>(y)_
* _log<sub>b</sub>(x/y) = log<sub>b</sub>(x) - log<sub>b</sub>(y)_
* _log<sub>b</sub>(x<sup>n</sup>) = n log<sub>b</sub>x_
* _log<sub>b</sub>(x) = log<sub>a</sub>x / log<sub>a</sub>b_
* _x<sup>log(n)</sup> = n<sup>log(x)</sup>_

## Primality

__Prime Number Theorem__

_lim<sub>n -> &infin;</sub> &pi;(n)/(n/ln n) = 1_
