# Fibonacci Numbers
## Introduction
_The Fibonacci sequence is defined as follows:_
<pre>
F<sub>0</sub> = 0
F<sub>1</sub> = 1
F<sub>n</sub> = F<sub>n-1</sub> + F<sub>n-2</sub>
</pre>
_The First elements of the Sequence are,_
<pre>
0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89, ...
</pre>
## Properties
_Cassini's Identity:_
<pre>
F<sub>n-1</sub>.F<sub>n+1</sub> - F<sub>n</sub><sup>2</sup> = (-1)<sup>n</sup>
</pre>
_The "Addition" Rule:_
<pre>
F<sub>n+k</sub> = F<sub>k</sub>.F<sub>n+1</sub> + F<sub>k-1</sub>.F<sub>n</sub>
</pre>
_If_ `k == n`,
<pre>
   F<sub>2n</sub> = F<sub>n</sub>.F<sub>n+1</sub> + F<sub>n-1</sub>.F<sub>n</sub>
>> F<sub>2n</sub> = F<sub>n</sub>(F<sub>n+1</sub> + F<sub>n-1</sub>)
</pre>
_Therefore, we can say that_,
<pre>
>> For any positive integer k , F<sub>nk</sub> is a multiple of F<sub>n</sub>
   
>> If F<sub>m</sub> is a multiple of F<sub>n</sub> , m is a multiple of n
</pre>
_GCD Identity:_
<pre>
GCD(F<sub>m</sub> , F<sub>n</sub>) = F<sub>GCD(m, n)</sub>
</pre>
_Fibonacci numbers are the worst possible inputs for Euclidean algorithm_ <br>
_According to Zeckendorf's theorem, any natural number_ `n` _can be uniquely represented as a sum of Fibonacci numbers_
<pre>
 1 = 1          = F<sub>2</sub>
 2 = 2          = F<sub>3</sub>
 6 = 5 + 1      = F<sub>5</sub> + F<sub>2</sub>
 8 = 8          = F<sub>6</sub>
 9 = 8 + 1      = F<sub>6</sub> + F<sub>2</sub>
19 = 13 + 5 + 1 = F<sub>7</sub> + F<sub>5</sub> + F<sub>2</sub>
</pre>


