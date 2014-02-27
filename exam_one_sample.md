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

__In an RSA cryptosystem, `p = 7` and `q = 11`. Find appropriate exponents `d` and `e`.__  
> Find the __gcd(e, (7 &minus; 1)(11 &minus; 1)) = 1__
>	_gcd(e, (7 &minus; 1)(11 &minus; 1)) = 1_
>	_gcd(e, 60) = 1_
>	__e = 7__
> Solve for __d__
>	_d = e<sup>-1</sup>_ mod _(p &minus; 1)(q &minus; 1)_
>	_d = 7<sup>-1</sup>_ mod _60_
>	_7 &times; d = 1_ mod _60_
> Find the __gcd(7, 60) = 1__
>	_60 = 8 &times; 7 &plus; 4_
>	_7 = 1 &times; 4 &plus; 3_
>	_4 = 1 &times; 3 &plus; 1_
>	_3 = 3 &times; 1 &plus; 0_
> Find the __linear combination__
>	_1 = 4 &minus; 1 &times; 3_
>	_1 = 4 &minus; (7 &minus; 1 &times; 4)_
>	_1 = 4 &minus; 7 &plus; 4_
>	_1 = &minus;7 &plus; 2(60 &minus; 8 &times; 7)_
>	_1 = &minus;7 &plus; (2 &times; 60) &minus; (16 &times; 7)_
>	_1 = (2 &times; 60) &plus; (&minus;17 &times; 7)_
> Use __1 = ax &plus; by__
>	__b = d = -17__
> Substitute __d__
>	_d = x_ mod _60_
>	_-17 = x_ mod _60_
>	_x = 43_ mod _60_
>	__d = 43 mod 60__



