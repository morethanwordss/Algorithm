⁰¹²³⁴⁵⁶⁷⁸⁹
# Binary Exponentiation
## Introduction
<pre>
Binary exponentiation is also known as exponentiation by squaring.
By using this trick we can calculate aⁿ in O(log n) instead of O(n).
</pre>
## Algorithm
<pre>
a<sup>n</sup> = 1 if n == 0
              = (a<sup><sup>n</sup>/<sub>2</sub></sup>)<sup>2</sup> if n is even
              = (a<sup><sup>(n-1)</sup>/<sub>2</sub></sup>)<sup>2</sup> • a if n is odd
  


