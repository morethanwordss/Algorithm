# Binary GCD
## Introduction
<pre>
Modulo Operations are much slower than addition, subtraction, bitwise operations
The Binary GCD algorithm is an optimization to the normal Euclidean algorithm.
</pre>
## Algorithm
<pre>
1.  If both numbers are even, then we can factor out a two of both and compute the GCD of the remaining numbers:  
    gcd(2a, 2b) = 2 * gcd(a, b)
  
2.  If one of the numbers is even and the other one is odd, then we can remove the factor 2 from the even one:  
    gcd(2a, b) = gcd(a, b) if b is odd
  
3.  If both numbers are odd, then subtracting one number of the other one will not change the GCD:  
    gcd(a, b) = gcd(b, a-b) 
</pre>
## Implementation
```cpp
/* c++ */
int gcd(int a, int b) {
    if (!a || !b)
        return a | b;
    unsigned shift = __builtin_ctz(a | b);
    a >>= __builtin_ctz(a);
    do {
        b >>= __builtin_ctz(b);
        if (a > b)
            swap(a, b);
        b -= a;
    } while (b);
    return a << shift;
}
```
