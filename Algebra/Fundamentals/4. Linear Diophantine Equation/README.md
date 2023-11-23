# Linear Diophantine Equation
## Introduction

<pre>
Problem Statement:

a.x + b.y = c
Given the value of (a, b, c), We have to find out the value of (x, y) such that it satisfies the equation.
</pre>

## Theory

### Degenerate Case
<pre>
Case: (a, b) = (0, 0)
   
   a.x + b.y = c
>> 0.x + 0.y = c [replacing (a, b) with(0, 0)]
>> 0 + 0 = c
>> c = 0
</pre>
<pre>
Therefore, for (a, b) = (0, 0),
   
if c = 0, many solution exists,
Otherwise there is no solution.
</pre>

### Usual Case
<pre>
Let denote gcd(a, b) with g.
Now, (a.x + b.y) | g  because, (a.x | g) and (b.y | g)
As c = a.x + b.y, there exist solutions if and only if c | g
</pre>

### Finding Any Solution
<pre>
Euclidean Extended Algorithm:
   
   a.x' + b.y'       = g   
>> (a.x' + b.y').k   = g.k   [Let k be any integer]
>> a.x'.k + b.y'.k   = g.k
>> a.x'.k + b.y'.k   = c     [let g.k == c]
>> a.x + b.y         = c
</pre>
<pre>
Therefore, 
x   = x' . k 
    = x' . (c/g)   [As c = g.k]
   
y   = y' . k 
    = y' . (c/g)   [As c = g.k]

</pre>
### Overview
<pre>
if (x',y') is the solution for g, and
   (x , y) is the solution for c, then
   
The transition is (x, y) = (x', y') * (c/g)
</pre>
```c++
int gcd(int a, int b, int &x, int &y) {
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

bool gcdSoln(int a, int b, int c, int &x, int &y, int &g) {
    g = gcd(a, b, x, y);
    if (c % g != 0) return false;
    x *= c / g;
    y *= c / g;
    return true;
}
```
## Finding All Solution
<pre>
   a.x<sub>0</sub> + b.y<sub>0</sub> = c
>> a.x<sub>0</sub> + b.y<sub>0</sub> + ((a.b) / g) - ((a.b) / g) = c
>> a.x<sub>0</sub> + ((a.b) / g) + b.y<sub>0</sub> - ((a.b) / g) = c
>> a(x<sub>0</sub> + b/g) + b(y<sub>0</sub> - a/g) = c
>> a.x<sub>1</sub> + b.y<sub>1</sub> = c

Solution 0: (x<sub>0</sub> + 0 . b/g, y<sub>0</sub> - 0 . a/g)
Solution 1: (x<sub>0</sub> + 1 . b/g, y<sub>0</sub> - 1 . a/g)
Solution 2: (x<sub>0</sub> + 2 . b/g, y<sub>0</sub> - 2 . a/g)
........................................
Solution k: (x<sub>0</sub> + k . b/g, y<sub>0</sub> - k . a/g)
</pre>

## Finding a solution with minimum value of (x + y)
<pre>
  x<sub>k</sub> + y<sub>k</sub>
= x<sub>0</sub> + k . (b/g) + y<sub>0</sub> - k . (a/g)
= x<sub>0</sub> + y<sub>0</sub> + (k . b/g) - (k . a/g)
= x<sub>0</sub> + y<sub>0</sub> + k . (b/g - a/g)
= x<sub>0</sub> + y<sub>0</sub> + k . (b - a) / g

if (b > a) (x + y)<sub>min</sub> = k<sub>min</sub>; [less pos]
if (b < a) (x + y)<sub>min</sub> = k<sub>max</sub>; [maxx neg]
if (b == a) all same
</pre>
