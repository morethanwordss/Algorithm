# Binary Exponentiation
## Introduction
<pre>
Binary exponentiation is also known as exponentiation by squaring.
By using this trick we can calculate aⁿ in O(log n) instead of O(n).
</pre>
## Algorithm
<pre>
a<sup>n</sup>  = 1                 if n == 0
    
    = (a<sup><sup>n</sup>/<sub>2</sub></sup>)<sup>2</sup>            if n is even
    
    = (a<sup><sup>(n-1)</sup>/<sub>2</sub></sup>)<sup>2</sup> • a      if n is odd
</pre>
## Implementation
### i) Recursive 
```cpp
/* c++ */
long long pow(long long a, long long b) {
    if (b == 0)
        return 1;
    long long res = pow(a, b / 2);
    if (b % 2)
        return res * res * a;
    else
        return res * res;
}
```
```py
# Python
def power(a, b):
    if b == 0:
        return 1
    res = power(a, b // 2)
    if b % 2:
        return res * res * a
    else:
        return res * res
```
### ii) Loop
```cpp
/* c++ */
long long pow(long long a, long long b) {
    long long res = 1;
    while (b > 0) {
        if (b & 1)
            res = res * a;
        a = a * a;
        b >>= 1;
    }
    return res;
}
```
``` py
# Python
def power(a, b):
    res = 1
    while b > 0:
        if b & 1:
            res = res * a
        a = a * a
        b >>= 1
    return res
```

## Applications
<pre>
1. Effective computation of large exponents modulo a number
   Question: Compute x<sup>n</sup> mod m
   
2. Effective computation of Fibonacci numbers
   Question: Compute n<sup>th</sup> Fibonacci number (F<sub>n</sub>)
   
3. Applying a permutation k times
   Question: You are given a sequence of length n. Apply to it a given permutation k times
   
4. Fast application of a set of geometric operations to a set of points
   Question: Given n  points p<sub>i</sub>, apply m  transformations to each of these points.
   Each transformation can be a shift, a scaling or a rotation around a given axis by a given angle.
   There is also a "loop" operation which applies a given list of transformations k times ("loop" operations can be nested).
   You should apply all transformations faster than O(n * length), where
   length  is the total number of transformations to be applied (after unrolling "loop" operations).
   
5. Number of paths of length k in a graph
   Question: Given a directed unweighted graph of n  vertices,
   find the number of paths of length k from any vertex u to any other vertex v
   
6. Variation of binary exponentiation: multiplying two numbers modulo
   Question:  Multiply two numbers a and b modulo m.
   a and b  fit in the built-in data types, but their product is too big to fit in a 64-bit integer. 
</pre>
