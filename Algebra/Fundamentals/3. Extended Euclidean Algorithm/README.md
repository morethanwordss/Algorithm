# Extended Euclidean Algorithm
<pre>a.x + b.y = gcd(a, b)</pre>

## Theory
<img width="518" alt="Screenshot 2023-11-23 150056" src="https://github.com/t0-ji/Algorithm/assets/108709544/4bf74c87-3ec6-4dd0-999a-d42985cf1bc2"> <br>
<pre>
This process ends with `b == 0` and `a = g`.
</pre>
<pre>
>> a.x + b.y = g
>> g.x + 0.y = g
A solution is (x, y) = (1, 0)
</pre>
The change in `(x, y)` change during the transition from `(b, a mod b)` to `(a, b)` as we go backwards up the recusrsive calls.
For the coefficient `(x', y')` for `(b, a mod b)` , the Equation is, 
<pre>b.x' + (a mod b).y' = g</pre>
Substituting `a mod b` with `a - ceil(a / b).b`,

<pre>
          b.x' + (a mod b).y'               = g          
>>        b.x' + (a - ceil(a/b).b).y'       = g          
>>        b.x' + a.y' - ceil(a/b).b.y'      = g
>>        a.y' + b.x' - ceil(a/b).b.y'      = g
>>        a.y' + b(x' - ceil(a/b).y')       = g
</pre>
<pre>
x = y'
y = x' - ceil(a / b) . y'
</pre>
## Implementation
### Recursive
```c++
int gcd(int a, int b, int& x, int& y) {
    if (b == 0) {
        x = 1;
        y = 0;
        return a;
    }
    int _x, _y;
    int d = gcd(b, a % b, _x, _y);
    x = _y;
    y = _x - _y * (a / b);
    return d;
}
```
### Iterative
```c++
int gcd(int a, int b, int& x, int& y) {
    x = 1, y = 0;
    int _x = 0, _y = 1, _a = a, _b = b;
    while (_b) {
        int q = _a / _b;
        tie(x, _x) = make_tuple(_x, x - q * _x);
        tie(y, _y) = make_tuple(_y, y - q * _y);
        tie(_a, _b) = make_tuple(_b, _a - q * _b);
    }
    return _a;
}
```
