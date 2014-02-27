## Asymptotic Notation

__&Theta;-notation__

* _f(n) = &Theta;(g(n))_ __and__ _g(n) = &Theta;(h(n))_ __imply__ _f(n) = &Theta;(h(n))_
* _f(n) = &Theta;(g(n))_ __is like__ _a = b_
<dl>
	<dt>`Proof` _f(n) = &Theta;(g(n))_</dt>
	<dd>there exist positive constants _c<sub>1</sub>_, _c<sub>2</sub>_, and _n<sub>0</sub>_</dd>
	<dd>such that _0 &le; c<sub>1</sub>g(n) &le; f(n) &le; c<sub>2</sub>g(n)_ for all _n &ge; n<sub>0</sub>_</dd>
</dl>

__O-notation__

* _f(n) = O(g(n))_ __and__ _g(n) = O(h(n))_ __imply__ _f(n) = O(h(n))_
* _f(n) = O(g(n))_ __is like__ _a &le; b_
<dl>
	<dt>`Proof` _f(n) = O(g(n))_</dt>
	<dd>there exist positive constants _c_ and _n<sub>0</sub>_</dd>
	<dd>such that _0 &le; f(n) &le; cg(n)_ for all _n &ge; n<sub>0</sub>_</dd>
</dl>

__&Omega;-notation__

* _f(n) = &Omega;(g(n))_ __and__ _g(n) = &Omega;(h(n))_ __imply__ _f(n) = &Omega;(h(n))_
* _f(n) = &Omega;(g(n))_ __is like__ _a &ge; b_
<dl>
	<dt>`Proof` _f(n) = &Omega;(g(n))_</dt>
	<dd>there exist positive constants _c_ and _n<sub>0</sub>_</dd>
	<dd>such that _0 &le; cg(n) &le; f(n)_ for all _n &ge; n<sub>0</sub>_</dd>
</dl>

## Logarithm

* _log<sub>b</sub>(xy) = log<sub>b</sub>(x) + log<sub>b</sub>(y)_
* _log<sub>b</sub>(x/y) = log<sub>b</sub>(x) - log<sub>b</sub>(y)_
* _log<sub>b</sub>(x<sup>n</sup>) = n log<sub>b</sub>x_
* _log<sub>b</sub>(x) = log<sub>a</sub>x / log<sub>a</sub>b_
* _x<sup>log(n)</sup> = n<sup>log(x)</sup>_

## Factorization

__Integer Factorization Problem__ (_IFP_): Given a positive integer _n &gt; 1_, find a factor _1 &lt; a &lt; n_ of _n_ such that _n = ab_ for _1 &lt; b &lt; n_.

*	Given a large positive composite integer _n &gt; 1_, find _p_ and _q_ `n = p * q`, where _p_ and _q_ are primes.
*	This is the problem that the most famous _RSA_ cryptosystem is based on.
*	To factor a general integer, it takes _O(exp((64/9)<sup>1/3</sup>(log n)<sup>1/3</sup>(log log n)<sup>2/3</sup>))_
*	To factor a special integer, it takes _O(exp((32/9)<sup>1/3</sup>(log n)<sup>1/3</sup>(log log n)<sup>2/3</sup>))_
*	_IFP_ is `intractable`

## Primality

__Primality Testing Problem__ (_PTP_): Given a positive integer greater than 1, determine whether or not it is prime.

*	This problem can be solved by the _AKS_ algorithm deterministically and unconditionally in _O(log(n))_.
*	_PTP_ is `tractable`


