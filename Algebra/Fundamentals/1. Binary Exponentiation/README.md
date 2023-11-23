# Binary Exponentiation
## Theory
<pre>
Calculating A<sup>n</sup> in O(log n) time
</pre>
<img width="465" alt="Screenshot 2023-11-23 144215" src="https://github.com/t0-ji/Algorithm/assets/108709544/c766b433-c0fc-439b-894d-496a1203bba2"> <br>
## Implementation
### Recursive 
```cpp
long long binpow(long long a, long long b) {
    if (b == 0) return 1;
    long long res = binpow(a, b / 2);
    if (b % 2) return res * res * a;
    else return res * res;
}
```
### Iterative
```cpp
long long binpow(long long a, long long b) {
    long long res = 1;
    while (b > 0) {
        if (b & 1) res = res * a;
        a = a * a;
        b >>= 1;
    }
    return res;
}
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
