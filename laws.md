## Arithmetic

__Addition__
<dl>
	<dt>Given two binary numbers _x_ and _y_, where _x_ and _y_ are each _n_ bits long, the sum of _x_ and _y_ is __n &plus; 1__</dt>
	<dt>`Run-time`</dt>
		<dd>The total running time for the addition algorithm is therefore of the form _c<sub>0</sub> &plus; c<sub>1</sub>n_, where _c<sub>0</sub>_ and _c<sub>1</sub>_ are some constants. In other other words, the run-time is `linear`, denoted as __O(n)__.</dd>
</dl>

__Multiplication__
<dl>
	<dt>If _x_ and _y_ are both _n_ bits, then there are _n_ intermediate rows, with lengths of up to _2n_ bits (taking the shifting into account).</dt>
	<dt>Bit-wise multiplication uses the `left-shift` technique.</dt>
	<dt>`Run-time`</dt>
		<dd>The total time taken to add up these rows, doing two numbers at a time, is</dd>
		<dd>_O(n) &plus; O(n) &plus; ... &plus; O(n) = n &minus; 1_ times.</dd>
		<dd>The run-time is `quadratic` in the size of the inputs, denoted as __O(n<sup>2</sup>)__.</dd>
</dl>

__Division__
<dl>
	<dt>To divide an integer _x_ by another integer _y &#8800; 0_ means to find a quotient _q_ and a remainder _r_, where _x = yq &plus; r_ and _r &lt; y_.</dt>
	<dt>Bit-wise division uses the `right-shift` technique.</dt>
	<dt>`Run-time`</dt>
		<dd>Like multiplication, the run-time is `quadratic`.</dd>
</dl>

__Recursion__
<dl>
	<dt>`Rule` _x &times; y:_</dt>
		<dd>_= 2(x &times; &lfloor;y/2&rfloor;)_ if _y_ is even</dd>
		<dd>_= x &plus; 2(x &times; &lfloor;y/2&rfloor;)_ if _y_ is odd</dd>
	<dt>---------------</dt>
	<dt>_function multiply (x, y)_</dt>
	<dt>`Input` two _n_-bit integers _x_ and _y_, where _y &ge; 0_</dt>
	<dt>`Output` their product</dt>
		<dd>if _y = 0:_ return _0_</dd>
		<dd>_z =_ multiply_(x, &lfloor;y/2&rfloor;)_</dd>
		<dd>if _y_ is even:</dd>
		<dd>&nbsp;&nbsp;&nbsp;&nbsp;return _2z_</dd>
		<dd>else:</dd>
		<dd>&nbsp;&nbsp;&nbsp;&nbsp;return _x &plus; 2z_</dd>
	<dt>---------------</dt>
	<dt>`Run-time`</dt>
		<dd>The program terminates after _n_ recursive calls, because at each call _y_ is halved&mdash;that is, its number of bits is decreased by one.</dd>
		<dd>Each recursive call requires the following operations:</dd>
		<dd>&nbsp;&nbsp;&nbsp;&nbsp;&spades; a division by 2 (right shift)</dd>
		<dd>&nbsp;&nbsp;&nbsp;&nbsp;&spades; a test for odd/even (looking up the last bit)</dd>
		<dd>&nbsp;&nbsp;&nbsp;&nbsp;&spades; a multiplication by 2 (left shift)</dd>
		<dd>&nbsp;&nbsp;&nbsp;&nbsp;&spades; possibly one addition</dd>
		<dd>Thus the run-time is __O(n<sup>2</sup>)__</dd>
</dl>

## Cryptography

__Symmetric (Private Key) Cryptography Protocol__

~~~
Initial setup:
	1. Alice and Bob publicly agree on a cryptosystem.
For each message Alice -> Bob:
	1. Alice and Bob privately agree on a key.
	2. Alice enciphers her plaintext using the agreed key.
	3. Alice sends the ciphertext message to Bob.
	4. Bob deciphers the ciphertext message to obtain the plaintext.
~~~

__Public Key Cryptography Protocol__

~~~
Initial setup:
	1. Alice and Bob publicly agree on a cryptosystem.
	2. Bob sends Alice his public key.
For each message Alice -> Bob:
	1. Alice enciphers her plaintext using Bob's public key.
	2. Alice sends the ciphertext message to Bob.
	3. Bob deciphers the ciphertext message using his private key.
~~~

## Asymptotic Notation

__&Theta;-notation__

* _f(n) = &Theta;(g(n))_ __and__ _g(n) = &Theta;(h(n))_ __imply__ _f(n) = &Theta;(h(n))_
* _f(n) = &Theta;(g(n))_ __is like__ _a = b_
<dl>
	<dt>`Proof` _f(n) = &Theta;(g(n))_</dt>
		<dd>there exist positive constants _c<sub>1</sub>_, _c<sub>2</sub>_, and _n<sub>0</sub>_,</dd>
		<dd>such that _0 &le; c<sub>1</sub>g(n) &le; f(n) &le; c<sub>2</sub>g(n)_ for all _n &ge; n<sub>0</sub>_</dd>
</dl>

__O-notation__

* _f(n) = O(g(n))_ __and__ _g(n) = O(h(n))_ __imply__ _f(n) = O(h(n))_
* _f(n) = O(g(n))_ __is like__ _a &le; b_
<dl>
	<dt>`Proof` _f(n) = O(g(n))_</dt>
		<dd>there exist positive constants _c_ and _n<sub>0</sub>_,</dd>
		<dd>such that _0 &le; f(n) &le; cg(n)_ for all _n &ge; n<sub>0</sub>_</dd>
</dl>

__&Omega;-notation__

* _f(n) = &Omega;(g(n))_ __and__ _g(n) = &Omega;(h(n))_ __imply__ _f(n) = &Omega;(h(n))_
* _f(n) = &Omega;(g(n))_ __is like__ _a &ge; b_
<dl>
	<dt>`Proof` _f(n) = &Omega;(g(n))_</dt>
		<dd>there exist positive constants _c_ and _n<sub>0</sub>_,</dd>
		<dd>such that _0 &le; cg(n) &le; f(n)_ for all _n &ge; n<sub>0</sub>_</dd>
</dl>

## Factorization

__Integer Factorization Problem__ (_IFP_): Given a positive integer _n &gt; 1_, find a factor _1 &lt; a &lt; n_ of _n_ such that _n = ab_ for _1 &lt; b &lt; n_.

*	Given a large positive composite integer _n &gt; 1_, find _p_ and _q_, `n = p * q`, where _p_ and _q_ are primes.
*	This is the problem that the most famous _RSA_ cryptosystem is based on.
*	To factor a general integer, it takes _O(exp((64/9)<sup>1/3</sup>(log n)<sup>1/3</sup>(log log n)<sup>2/3</sup>))_
*	To factor a special integer, it takes _O(exp((32/9)<sup>1/3</sup>(log n)<sup>1/3</sup>(log log n)<sup>2/3</sup>))_
*	_IFP_ is `intractable`

## Logarithm

* _log<sub>b</sub>(xy) = log<sub>b</sub>(x) &plus; log<sub>b</sub>(y)_
* _log<sub>b</sub>(x/y) = log<sub>b</sub>(x) &minus; log<sub>b</sub>(y)_
* _log<sub>b</sub>(x<sup>n</sup>) = n log<sub>b</sub>x_
* _log<sub>b</sub>(x) = log<sub>a</sub>x / log<sub>a</sub>b_
* _x<sup>log(n)</sup> = n<sup>log(x)</sup>_

## Modular Arithmetic

__Modular Arithmetic__ : a system for dealing with restricted ranges of integers. We define _x modulo N_ to be the remainder when _x_ is divided by _N_; that is, if _x = qN + r_ with _0 &le; r &le; N_, then _x_ modulo _N_ is equal to _r_.
<dl>
		<dd>_x &equiv; y_ (mod _N_) <= => _N_ divides (_x - y_)</dd>
	<dt>`Substitution Rule`</dt>
		<dd>If _x &equiv; x&prime;_ (mod _N_) and _y &equiv; y&prime;_ (mod _N_), then:</dd>
		<dd>_x &plus; y &equiv; x&prime; + y&prime;_ (mod _N_) and _xy &equiv; x&prime;y&prime;_ (mod _N_)</dd>
</dl>

__Modular Addition__
<dl>
	<dt>The complexity of `modular addition` is __O(n)__ (linear),</dt>
		<dd>where _n = &lceil;log N&rceil;_ is the size of _N_</dd>
</dl>
~~~
  (30 + 26 + 8 + 29 + 28 + 5) mod 31
= (((((30 + 26) mod 31 + 8) mod 31 + 29) mod 31 + 28) mod 31 + 5) mod 31
= ((((25 + 8) mod 31 + 29) mod 31 + 28) mod 31 + 5) mod 31
= (((2 + 29) mod 31 + 28) mod 31 + 5) mod 31
= ((0 + 28) mod 31 + 5) mod 31
= (28 + 5) mod 31
= 2
~~~

__Modular Multiplication__
<dl>
	<dt>The complexity of `modular multiplication` is __O(n<sup>2</sup>)__ (quadratic),</dt>
		<dd>to compute _x &times; y mod N_, multiply (quadratic) then divide (quadratic) to get the remainder.</dd>
</dl>
~~~
  (30 x 26 x 8 x 29 x 28 x 5) mod 31
= (((((30 x 26) mod 31 x 8) mod 31 x 29) mod 31 x 28) mod 31 + 5) mod 31
= ((((5 x 8) mod 31 x 29) mod 31 x 28) mod 31 x 5) mod 31
= (((9 + 29) mod 31 x 28) mod 31 x 5) mod 31
= ((13 x 28) mod 31 x 5) mod 31
= (23 x 5) mod 31
= 22
~~~

## Primality

__Primality Testing Problem__ (_PTP_): Given a positive integer greater than 1, determine whether or not it is prime.

*	This problem can be solved by the _AKS_ algorithm deterministically and unconditionally in _O(log(n))_.
*	_PTP_ is `tractable`

__Fermat's Little Theorem__


