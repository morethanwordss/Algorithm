# Extended Euclidean Algorithm
<pre>a.x + b.y = gcd(a, b)</pre>

## Theory
<pre>
if (b == 0) gcd(a, b) = a;
else gcd(a, b) = gcd(b, a mod b);
</pre>
The process ends with `b == 0` and `a = g`. <br>
<pre>
>> a.x + b.y = g
>> g.x + 0.y = g
A solution is (x, y) = (1, 0)
</pre>
All we need to do is to figure out how the coefficients `x` and `y` change during the transition from `(b, a mod b)` to `(a, b)` as we go backwards up the recusrsive calls.
For the coefficient `(x1, y1)` for `(b, a mod b)` , the Equation is, 
<pre>b.x<sub>1</sub> + (a mod b).y<sub>1</sub> = g</pre>
Substituting `a mod b` with `a - ceil(a / b).b`,

<pre>
          b.x<sub>1</sub> + (a mod b).y<sub>1</sub>                   = g          
>>        b.x<sub>1</sub> + (a - ceil(a/b).b).y<sub>1</sub>           = g          
>>        b.x<sub>1</sub> + a.y<sub>1</sub> - ceil(a/b).b.y<sub>1</sub>          = g
>>        a.y<sub>1</sub> + b.x<sub>1</sub> - ceil(a/b).b.y<sub>1</sub>          = g
>>        a.y<sub>1</sub> + b(x<sub>1</sub> - ceil(a/b).y<sub>1</sub>            = g
</pre>
<pre>
x = y<sub>1</sub>
y = x<sub>1</sub> - ceil(<sup>a</sup>/<sub>b</sub>).y<sub>1</sub>
</pre>
## Extended Euclidean Algorithm (Recursive)
```c++
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
## Extended Euclidean Algorithm (Loop)
```c++
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
