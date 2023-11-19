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
</pre>
## Implementation
### Recusrsive
```cpp
long long binpow(long long a, long long b) {
    if (b == 0) return 1;
    long long res = binpow(a, b / 2);
    return res * res * ((b % 2) ? a : 1); 
}
```
### Loop
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
### a<sup>b</sup> mod m
```cpp
long long binpow(long long a, long long b, long long m) {
    a %= m;
    long long res = 1;
    while (b > 0) {
        if (b & 1) res = res * a % m;
        a = a * a % m;
        b >>= 1;
    }
    return res;
}
```
