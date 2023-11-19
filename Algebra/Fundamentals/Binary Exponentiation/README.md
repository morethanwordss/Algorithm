⁰¹²³⁴⁵⁶⁷⁸⁹
# Binary Exponentiation
## Introduction
<pre>
Binary exponentiation is also known as exponentiation by squaring.
By using this trick we can calculate aⁿ in O(log n) instead of O(n).
</pre>
## Algorithm
<pre>
We know that,
a ⁺ = a <sup>b</sup> • a <sup>c</sup> <br>
Let, <br>
&nbsp a = 3 <br>
n = 13 <br> ⁰¹²³⁴⁵⁶⁷⁸⁹
Then,<br>
a<sup>n</sup> = 3<sup>13</sup> = 3<sup>1101<sub>2</sub></sup> = 3<sup>8</sup> • 3<sup>4</sup> • 3<sup>1</sup><br>

