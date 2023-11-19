# Binary Exponentiation
## Introduction
Binary exponentiation is also known as exponentiation by squaring.

By using this trick we can calculate _a<sup>n</sup>_ in _O(log n)_ instead of _O(n)_.
## Algorithm
We know that,<br>
a <sup>b + c</sup> = a <sup>b</sup> • a <sup>c</sup> <br>
Let, <br>
<p allign = "center"> a = 3 <br>
n = 13 <br></p>
Then,<br>
a<sup>n</sup> = 3<sup>13</sup> = 3<sup>1101<sub>2</sub></sup> = 3<sup>8</sup> • 3<sup>4</sup> • 3<sup>1</sup><br>

