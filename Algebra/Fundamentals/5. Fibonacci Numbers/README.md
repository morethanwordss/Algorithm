# Fibonacci Numbers
## Introduction
The Fibonacci sequence is defined as follows:
<pre>
F<sub>0</sub> = 0
F<sub>1</sub> = 1
F<sub>n</sub> = F<sub>n-1</sub> + F<sub>n-2</sub>
</pre>
The First elements of the Sequence are,
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
For `k == n`,
<pre>
   F<sub>2n</sub> = F<sub>n</sub>.F<sub>n+1</sub> + F<sub>n-1</sub>.F<sub>n</sub>
>> F<sub>2n</sub> = F<sub>n</sub>(F<sub>n+1</sub> + F<sub>n-1</sub>)
</pre>
Therefore, we can say that,
<pre>
>> For any positive integer k , F<sub>nk</sub> is a multiple of F<sub>n</sub>
>> If F<sub>m</sub> is a multiple of F<sub>n</sub> , m is a multiple of n
</pre>
_GCD Identity:_
<pre>
GCD(F<sub>m</sub> , F<sub>n</sub>) = F<sub>GCD(m, n)</sub>
</pre>
Fibonacci numbers are the worst possible inputs for Euclidean algorithm <br>
According to Zeckendorf's theorem, any natural number `n` can be uniquely represented as a sum of Fibonacci numbers
<pre>
 1 = 1          = F<sub>2</sub>
 2 = 2          = F<sub>3</sub>
 6 = 5 + 1      = F<sub>5</sub> + F<sub>2</sub>
 8 = 8          = F<sub>6</sub>
 9 = 8 + 1      = F<sub>6</sub> + F<sub>2</sub>
19 = 13 + 5 + 1 = F<sub>7</sub> + F<sub>5</sub> + F<sub>2</sub>
</pre>
Notice, any number `n` is not represented by the summation of two consecutive Fibonacci Numbers, as the summation of two consecutive fibonacci number will be another ficonacci number by the definition. <br>
Therefore,
<pre>
5 is not represented as F<sub>4</sub> + F<sub>3</sub> , but
5 is represented as F<sub>5</sub>
</pre>
Any number can be uniquely encoded in the Fibonacci coding, and we can describe this representation with binary code as <pre>b<sub>0</sub>b<sub>1</sub>b<sub>1</sub>b<sub>2</sub>...b<sub>n</sub>**1**
Where, b<sub>i</sub> is `1` if F<sub>i+2</sub> is used in the representation, otherwise `0` </pre> 
Again, notice the binary code representation ends with an additional `1` at the end. This is the only occurance where `two consecutive 1` appears (_We have previously proved that any number_ `n` _is not represented by the summation of two consecutive Fibonacci Numbers, as the summation of two consecutive fibonacci number will be another ficonacci number by the definition_) which can be identified as the end of the representation.
<pre>
 1  =  1          = F<sub>2</sub>                                 = (11)<sub>F</sub>
 2  =  2          = F<sub>3</sub>                                 = (011)<sub>F</sub>
 6  =  5 + 1      = F<sub>5</sub> + F<sub>2</sub>                 = (10011)<sub>F</sub>
 8  =  8          = F<sub>6</sub>                                 = (000011)<sub>F</sub>
 9  =  8 + 1      = F<sub>6</sub> + F<sub>2</sub>                 = (100011)<sub>F</sub>
19  =  13 + 5 + 1 = F<sub>7</sub> + F<sub>5</sub> + F<sub>2</sub> = (1001011)<sub>F</sub>
</pre>


