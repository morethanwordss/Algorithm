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
_Notice, any number n is not represented by the summation of two consecutive Fibonacci Numbers, as the summation of two consecutive fibonacci number will be another ficonacci number by the definition._ <br>
_Therefore,_ <br>
**5** _is not be represented as_ **F<sub>4</sub> + F<sub>3</sub>** , <br>
_instead_ **5** _is represented as_ **F<sub>5</sub**> <br>
_Any number can be uniquely encoded in the Fibonacci coding._ <br>
_And we can describe this representation with binary code_ **b<sub>0</sub>b<sub>1</sub>b<sub>1</sub>b<sub>2</sub>...b<sub>n</sub>1**. <br>
_Where_, **b<sub>i</sub>** _is_ **1** _if_ **F<sub>i+2</sub>** _is used in the representation, otherwise_ **0**. <br> 
_Again, notice the binary code representation ends with an additional_ **1** _at the end. This is the only occurance where two consecutive 1 appears (We have proved previously that any number n is not represented by the summation of two consecutive Fibonacci Numbers, as the summation of two consecutive fibonacci number will be another ficonacci number by the definition) which can be identified as the end of the representation._ <br>


