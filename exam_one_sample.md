## Sample Problems

__True/False: the number of bits needed to represent a number _N_ in base _b_ is _&lceil;log<sub>b</sub>N&rceil;_.__
> __[False]__

> &lfloor;log<sub>b</sub>N&rfloor; + 1

__True/False: if a &#8800; b, then log<sub>b</sub>N &#8800; &Theta;(log<sub>a</sub>N)__
> __[False]__

> Using the change of base formula, you can change the base of any log to another. So asymptotically, they are the same.

__If algorithm A run time is a `logarithmic function` of its input and algorithm B run time is a `linear function` of its input, which is asymptotically faster?__
> Algorithm A is faster, because logarithmic functions &gt; linear function

__True/False: n<sup>3</sup> = O(4<sup>log(n)</sup>)__
> __[True]__

> __Reduce O(4<sup>log(n)</sup>)__

>	* 4<sup>log(n)</sup> = n<sup>log<sub>2</sub>(4)</sup> = n<sup>2</sup>

> __Find constant _c_ such that n<sup>3</sup> = &Omega;(n<sup>2</sup>)__

>	* n<sup>3</sup> &gt; _c_ &times; n<sup>2</sup> with _c_ = 1
>	* n<sup>3</sup> &le; _c_ &times; n<sup>2</sup> with _c_ &ge; n
>	* Thus, n<sup>3</sup> = &Omega;(n<sup>2</sup>) with constant _c_ = n

__What is the security of the `RSA protocol` based on?__
> Based on the __factoring problem__, because of the difficulty of factoring the product of two large prime numbers.

__In an RSA cryptosystem, `p = 7` and `q = 11`. Find appropriate exponents `d` and `e`.__
> __Find the gcd(e, (7 - 1)(11 - 1)) = 1__

>	* _gcd(e, (7 - 1)(11 - 1)) = 1_
>	* _gcd(e, 60) = 1_
>	* __e = 7__

> __Solve for d__

>	* _d = e<sup>-1</sup>_ mod _(p - 1)(q - 1)_
>	* _d = 7<sup>-1</sup>_ mod _60_
>	* _7 &times; d = 1_ mod _60_

> __Find the gcd(7, 60) = 1__

>	* _60 = 8 &times; 7 + 4_
>	* _7 = 1 &times; 4 + 3_
>	* _4 = 1 &times; 3 + 1_
>	* _3 = 3 &times; 1 + 0_

> __Find the linear combination__

>	* _1 = 4 - 1 &times; 3_
>	* _1 = 4 - (7 - 1 &times; 4)_
>	* _1 = 4 - 7 + 4_
>	* _1 = -7 + 2(60 - 8 &times; 7)_
>	* _1 = -7 + (2 &times; 60) - (16 &times; 7)_
>	* _1 = (2 &times; 60) + (-17 &times; 7)_

> __Use 1 = ax + by__

>	* _1 = (2)(60) + (-17)(7)_
>	* __b = d = -17__

> __Substitute d__

>	* _d = x_ mod _60_
>	* _-17 = x_ mod _60_
>	* _x = 43_ mod _60_
>	* __d = 43 mod 60__

__What does the Master theorem specify?__
> Explains the routine of divide & conquer algorithm.

> __T(n) = a &times; T(n/b) + O(n<sup>d</sup>)__

>	* __a__ = the branching factor
>	* __b__ = the reduction of each call
>	* __d__ = the merge cost of sub-problems
>	* there are __log<sub>b</sub>(n)__ sublevels

> __Run-time__

>	* __O(n<sup>d</sup>)__ if _d > log<sub>b</sub>a_
>	* __O(n<sup>log<sub>b</sub>a</sup>)__ if _d < log<sub>b</sub>a_
>	* __O(n<sup>d</sup>log(n))__ if _d = log<sub>b</sub>a_

__Provide a recursive formula for performing modular exponentiation__
> Pikachu!

__Give a divide-and-conquer algorithm for integer multiplication that takes advantage of Gauss' observation so as to achieve a better running time than _O(n<sup>2</sup>)_.__
> __xy = 2<sup>n</sup>x<sub>l</sub>y<sub>l</sub> + 2<sup>n/2</sup>(x<sub>l</sub>y<sub>r</sub> + x<sub>r</sub>y<sub>l</sub>) + x<sub>r</sub>y<sub>r</sub>__

__Use the Master theorem to compute the running time of the above divide-and-conquer algorithm for integer multiplication__
> __T(n) = a &times; T(n/b) + O(n<sup>d</sup>)__   
> __a__ = branching factor = integer multiplication = 3  
> __b__ = reduction of each call (best case) = 2  
> __d__ = merge cost (best case) = 1

> __Compare _d_ with _log<sub>b</sub>a_:__  
> &emsp;1 ? log<sub>2</sub>3  
> &emsp;1 < log<sub>2</sub>3  
> Run-time is __O(n<sup>log<sub>2</sub>3</sup>)__

__Describe a divide-and-conquer approach for selecting the _k_-th element in a set of numbers.__
> Pick a random _v_ where _v_ is assumed to be in _a[0...n]_

> Create 3 arrays, one for `less than` _v_, `greater than` _v_, and `equal to` _v_

>	* S<sub>L</sub>, S<sub>V</sub>, S<sub>R</sub>

> __selection(S, k)__

>	* __selection(S<sub>L</sub>, K)__ if _k &le; |S<sub>L</sub>|_
>	* __v__ if _|S<sub>L</sub>| < k &le; |S<sub>L</sub>| + |S<sub>V</sub>|_
>	* __selection(S<sub>R</sub>, K - |S<sub>L</sub>| - |S<sub>V</sub>)__ if _k > |S<sub>L</sub>| + |S<sub>V</sub>|_

__What is the running time of the above solution?__
> __T(n) &le; T(3/4n) + O(n)__ <-- memorize this!

> __Find _a_, _b_, and _d_ from above__  

>	* T(n) = a &times; T(n/b) + O(n<sup>d</sup>)
>	* T(n) = 1 &times; T(n/(3/4)) + O(n<sup>1</sup>)
>	* so __a__ = 1, __b__ = 4/3, and __d__ = 1

> __Find run-time from above__

>	* d ? log<sub>b</sub>a
>	* 1 ? log<sub>4/3</sub>1
>	* 1 > log<sub>4/3</sub>1
>	* Run-time is O(n<sup>d</sup>) = O(n<sup>1</sup>) = __O(n)__

__Consider an alphabet _A_ where characters have frequencies _f(c), Select<sub>c</sub> within A_ and _x,y_ are the two lowest frequency characters. Show that there exists an optimal prefix code for alphabet _A_, where _x_ and _y_ have the same length and differ only in the last bit.__
> Use __Hoffman tree__, where the lowest frequent characters are located at the leafs.  

> To do this, specify that _f(a) > f(x)_ and _f(b) > f(y)_.   
> &emsp;Insert _a_ and _b_ into the tree,  
> &emsp;switch _a_ with _x_ and _b_ with _y_  
> &emsp;such that _a_ is the parent of _x_ and _b_ is the parent of _y_.

> As a result, _x_ and _y_ are now at the bottom (leaves of the tree) because they have the lowest frequency. Additionally they are siblings of each other because they both differ by one bit

