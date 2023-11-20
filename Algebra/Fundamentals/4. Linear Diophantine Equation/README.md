# Linear Diophantine Equation
## Introduction
A Linear Diophantine Equation is an equation of the general form,
<pre>a.x + b.y = c </pre>
Where `a`, `b`, `c` are given integers, and `x`, `y` are unknown integers. <br>
There are 4 classical problems on this equation, 
- Finding one solution
- Finding all solution
- Finding the number of solutions and the solutions themselves in a given interval
- Finding a solution with minimum value of `x + y`
## Analysis
>> If a == 0 and b == 0
<pre>
   a.x + b.y = c
>> 0.x + 0.y = c
>> 0 + 0 = c
>> c = 0
</pre>
Therefore, if `a == 0` and `b == 0`, the equation `a.x + b.y = c` has no solution if `c != 0` and has many solution if `c == 0` .
>> If a == 0 or b == 0

If a == 0, the equation,
<pre>
   a.x + b.y = c
>> 0.x + b.y = c
>> b.y = c
>> y = c/b
x can be any integer
</pre>
In the same way, if `b == 0`, `x = c/a` and `y` can be any integer.  
>> If a != 0 and b != 0

In the equation `a.x + b.y = c`,
- `a` is divisible by `gcd(a, b)`
- `a.x` is disible by `gcd(a, b)`
- `b` is divisible by `gcd(a, b)`
- `b.y` is divisible by `gcd(a, b)`
- `a.x + b.y` is divisble by `gcd(a, b)`
  
As, `c = a.x + b.y` and `a.x + b.y` is divisble by `gcd(a, b)`, `c` also has to be divisbile by `gcd(a, b)`. <br>
If `c` is not divisible by `gcd(a, b)`, there is no solution to the equation, `a.x + b.y = c`

## Finding One Solution
From the Extended Euclidean Algorithm we can find the value of `(x', y')` for the equation `a.x' + b.y' = gcd(a, b)`. <br>
As `c` is divisible by `gcd(a, b) = 0`, <br>
Let `k = c / gcd(a, b)`,
<pre>
   a.x' + b.y'       = gcd(a, b)
>> (a.x' + b.y') . k = gcd(a, b) . k
>> a.x'.k + b.y'.k   = gcd(a, b) . k
>> a.x'.k + b.y'.k   = c
</pre>
Comparing this with the equation `a.x + b.y = c`,
<pre>
x = x' . k
  = x' . (c / gcd(a, b))
</pre>
and, 
<pre>
y = y' . k
  = y' . (c / gcd(a, b)
</pre>
## Implimentation
```c++
/* c++ */
int gcd(int a, int b, int &x, int &y) {
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

bool find_any_solution(int a, int b, int c, int &x, int &y, int &g) {
    g = gcd(a, b, x, y);
    if (c % g) {
        return false;
    }
    x *= c / g;
    y *= c / g;
    return true;
}
```
```python
# Python
# Outside of the function, declare x = [0], y = [0], g = [0] as python doesn't support pass-by-refference
def gcd(a, b, x, y):
    if b == 0:
        x = 1
        y = 0
        return a
    x1, y1 = 0, 0
    d = gcd(b, a % b, x1, y1)
    x[0] = y1
    y[0] = x1 - y1 * (a // b)
    return d

def find_any_solution(a, b, c, x, y, g):
    g[0] = gcd(a, b, x, y)
    if c % g[0]:
        return False
    x[0] *= c // g[0]
    y[0] *= c // g[0]
    return True
```
## Finding All Solution
Lets denote `gcd(a, b)` with `g` and <br>
Let the base solution for the equation `a.x + b.y = c` is `(x1, y1)`. Now,
<pre>
   a.x<sub>0</sub> + b.y<sub>0</sub> = c
>> a.x<sub>0</sub> + b.y<sub>0</sub> + ((a.b) / g) - ((a.b) / g) = c
>> a.x<sub>0</sub> + ((a.b) / g) + b.y<sub>0</sub> - ((a.b) / g) = c
>> a(x<sub>0</sub> + b/g) + b(y<sub>0</sub> - a/g) = c
>> a.x<sub>1</sub> + b.y<sub>1</sub> = c
</pre>
Therefore, `(x1, y1)` is also a solution for the equation `a.x + b.y = c`, where,
<pre>
x<sub>1</sub> = x<sub>0</sub> + b/g
y<sub>1</sub> = y<sub>0</sub> - a/g
</pre>
Notice, this process can be repeated again. So, the general form of all the solution is,
<pre>
x<sub>k</sub> = x<sub>0</sub> + (b/g) . k
y<sub>k</sub> = y<sub>0</sub> - (a/g) . k
</pre>
## Finding a solution with minimum value of (x + y)
We know that,
<pre>
x<sub>k</sub> = x<sub>0</sub> + (b/g) . k
y<sub>k</sub> = y<sub>0</sub> - (a/g) . k
</pre>
Now, 
<pre>
  x<sub>k</sub> + y<sub>k</sub>
= x<sub>0</sub> + (b/g) . k + y<sub>0</sub> - (a/g) . k
= x<sub>0</sub> + k + y<sub>0</sub> + (b/g . k) - (a/g . k)
= x<sub>0</sub> + k + y<sub>0</sub> + k . (b/g - a/g)
= x<sub>0</sub> + k + y<sub>0</sub> + k . (b - a) / g
</pre>
For the minimum value of `(x + y)`, `k . (b - a) / g` has to be minimum
<pre>
if b > a:
   for (k = minimum) k . (b - a) / g = minimum
if b < a:
   for (k = maximum) k . (b - a) / g = minimum
if b == a:
   for (any value of k) k . (b - a) / g = 0 
</pre>
