## Sample Problems

__How many digits do you need to represent a number `N` in base `b`__  
> &lfloor;log<sub>b</sub>N&rfloor; + 1

__Prove the following: if a &#8800; b, then log<sub>b</sub>N = &Theta;(log<sub>a</sub>N)__  
> Using the change of base formula, you can change the base of any log to another. So asymptotically, they are the same.

__If algorithm A run time is a `logarithmic function` of its input and algorithm B run time is a `linear function` of its input, which is asymptotically faster?__
> Algorithm A is faster, because logarithmic functions &gt; linear function

__Prove the following: n<sup>3</sup> = O(4<sup>log(n)</sup>)__
> __Reduce O(4<sup>log(n)</sup>)__  
> 4<sup>log(n)</sup> = n<sup>log<sub>2</sub>(4)</sup> = n<sup>2</sup>  
> __Find constant _c_ such that n<sup>3</sup> = &Omega;(4<sup>log(n)</sup>)__  
> n<sup>3</sup> &gt; _c_ &times; n<sup>2</sup> with _c_ = 1  
> n<sup>3</sup> &le; _c_ &times; n<sup>2</sup> with _c_ &ge; n  
> Thus, n<sup>3</sup> = &Omega;(4<sup>log(n)</sup>) with constant _c_ = n

__What is the security of the `RSA protocol` based on?__
> Based on the __factoring problem__, because of the difficulty of factoring the product of two large prime numbers.

__A sender sends `N` packets, where each packet has a unique ID from `1 to N`. The receiver receives all but 1 packet. How does the receiver know which packet is missing?__  
> &Sigma;<sub>sender</sub> (1 to N) - &Sigma;<sub>receiver</sub> (1 to N)

__In an RSA cryptosystem, `p = 7` and `q = 11`. Find appropriate exponents `d` and `e`.__  
><dl>
>	<dt>Find the __gcd(e, (7 &minus; 1)(11 &minus; 1)) = 1__</dt>
>		<dd>_gcd(e, (7 &minus; 1)(11 &minus; 1)) = 1_</dd>
>		<dd>_gcd(e, 60) = 1_</dd>
>		<dd>__e = 7__</dd>
>	<dt>Solve for __d__</dt>
>		<dd>_d = e<sup>-1</sup>_ mod _(p &minus; 1)(q &minus; 1)_</dd>
>		<dd>_d = 7<sup>-1</sup>_ mod _60_</dd>
>		<dd>_7 &times; d = 1_ mod _60_</dd>
>	<dt>Find the __gcd(7, 60) = 1__</dt>
>		<dd>_60 = 8 &times; 7 &plus; 4_</dd>
>		<dd>_7 = 1 &times; 4 &plus; 3_</dd>
>		<dd>_4 = 1 &times; 3 &plus; 1_</dd>
>		<dd>_3 = 3 &times; 1 &plus; 0_</dd>
>	<dt>Find the __linear combination__</dt>
>		<dd>_1 = 4 &minus; 1 &times; 3_</dd>
>		<dd>_1 = 4 &minus; (7 &minus; 1 &times; 4)_</dd>
>		<dd>_1 = 4 &minus; 7 &plus; 4_</dd>
>		<dd>_1 = &minus;7 &plus; 2(60 &minus; 8 &times; 7)_</dd>
>		<dd>_1 = &minus;7 &plus; (2 &times; 60) &minus; (16 &times; 7)_</dd>
>		<dd>_1 = (2 &times; 60) &plus; (&minus;17 &times; 7)_</dd>
>	<dt>Use __1 = ax &plus; by__</dt>
>		<dd>__b = d = -17__</dd>
>	<dt>Substitute __d__</dt>
>		<dd>_d = x_ mod _60_</dd>
>		<dd>_-17 = x_ mod _60_</dd>
>		<dd>_x = 43_ mod _60_</dd>
>		<dd>__d = 43 mod 60__</dd>
></dl>



