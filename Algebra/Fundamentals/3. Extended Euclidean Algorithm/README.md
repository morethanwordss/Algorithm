# Extended Euclidean Algorithm
## Introduction
While the Euclidean Algorithm calculates only the GCD of two integers `a` and `b`, the the extended version also calculates such coefficients `x` and `y` for which:
<pre>a * x + b * y = gcd(a, b)</pre>

## Algorithm
Lets denote `gcd(a, b)` with `g` : <pre>a * x + b * y = g</pre>
If we recall the Euclidean Algorithm, 

<pre>
gcd(a, b) = a                If b == 0
          = gcd(b, a mod b)  Otherwise
</pre>
We can see that the algorithm ends with `b == 0` and `a = g`.

With this information we can easily find the value of `x` and `y` for `(a, b)` from the equation,
<pre>
   a * x + b * y = g
>> g * 1 + 0 * 0 = g
</pre>
Starting from these coefficients `(x, y) = (1, 0)` , we can go backwards up the recursive calls.

All we need to do is to figure out how the coefficients `x` and `y` change during the transition from `(b, a mod b)` to `(a, b)` as we go backwards up the recusrsive calls.

We want to find the pair `(x, y)` for `(a, b)` from the equation `a * x + b * y = g` assuming the coefficients `(x1, y1)` for `(b, a mod b)`.
For the coefficient `(x1, y1)` for `(a, b)` , the Equation is,  <pre>b * x<sub>1</sub> + (a mod b) * y<sub>1</sub> = g</pre>

And we want to find the pair `(x, y)` for `(a, b)` : `a * x + b * y = g`

We can represent `a mod b` as `a - ceil(a / b) * b`.  And so, substituting `a mod b` with `a - ceil(a / b) * b` gives us:

<pre>
             b * x<sub>1</sub> + (a mod b) * y<sub>1</sub>                    = g          
>>           b * x<sub>1</sub> + (a - ceil(a / b) * b) * y<sub>1</sub>        = g          
>>           (a - ceil(a / b) * b) * y<sub>1</sub> + b * x<sub>1</sub>        = g          
>>           a * y<sub>1</sub> +  b * x<sub>1</sub> - b * ceil(a / b)* y<sub>1</sub>     = g          
>>           a * y<sub>1</sub> +  b * (x<sub>1</sub> - ceil(a / b) * y<sub>1</sub>))     = g
</pre>
comparing this with the equation `a * x + b * y = g` ,
<pre>
x = y<sub>1</sub>
y = (x<sub>1</sub> - (ceil(<sup>a</sup>/<sub>b</sub>) * y<sub>1</sub>))
</pre>
## Implementation
### Euclidean ALgorithm for GCD (Recursive)
```c++
/* c++ */
int gcd (int a, int b) {
    if (b == 0)
        return a;
    else
        return gcd (b, a % b);
}
```
```py
# Python
def gcd(a, b):
    if b == 0:
        return a
    else:
        return gcd(b, a % b)
```
### Euclidean ALgorithm for GCD (Loop)
```c++
/* c++ */
int gcd (int a, int b) {
    while (b) {
        a %= b;
        swap(a, b);
    }
    return a;
}
```
```python
# Python
def gcd(a, b):
    while b:
        a %= b
        a, b = b, a
    return a
```
### Extended Euclidean Algorithm (Recursive)
```c++
/* c++ */
int gcd(int a, int b, int& x, int& y) {
    if (b == 0) {
        x = 1;
        y = 0;
        return a;
    }
    int x1, y1;
    int d = gcd(b, a % b, x1, y1);
    x = y1;
    y = x1 - y1 * (a / b);
    return d;
}
```
```python
# Python
# Outside of the function, declare x = [0], y = [0] as python doesn't support pass-by-refference 
def gcd(a, b, x, y):
    if b == 0:
        x[0] = 1
        y[0] = 0
        return a
    x1, y1 = [0], [0]
    d = gcd(b, a % b, x1, y1)
    x[0] = y1[0]
    y[0] = x1[0] - y1[0] * (a // b)
    return d
```
### Extended Euclidean Algorithm (Loop)
```c++
/* c++ */
int gcd(int a, int b, int& x, int& y) {
    x = 1, y = 0;
    int x1 = 0, y1 = 1, a1 = a, b1 = b;
    while (b1) {
        int q = a1 / b1;
        tie(x, x1) = make_tuple(x1, x - q * x1);
        tie(y, y1) = make_tuple(y1, y - q * y1);
        tie(a1, b1) = make_tuple(b1, a1 - q * b1);
    }
    return a1;
}
```
```python
# Python
# Outside of the function, declare x = [0], y = [0] as python doesn't support pass-by-refference
def gcd(a, b, x, y):
    x[0], y[0] = 1, 0
    x1, y1, a1, b1 = 0, 1, a, b
    while b1:
        q = a1 // b1
        x[0], x1 = x1, x[0] - q * x1
        y[0], y1 = y1, y[0] - q * y1
        a1, b1 = b1, a1 - q * b1
    return a1
```
