# Linear Diophantine Equation
<pre>a.x + b.y = c </pre>

## Theory
<pre>
if (a == 0 && b == 0):
   
   a.x + b.y = c
>> 0.x + 0.y = c
>> 0 + 0 = c
>> c = 0
   
So, (a == 0 && b == 0 && c != 0) has no soln
</pre>

<pre>
if (a == 0 || b == 0):
   
   a.x + b.y = c
>> 0.x + b.y = c [let a == 0 in this case]
>> b.y = c
>> y = c / b
   
if (a == 0) y = c / b;
if (b == 0) x = c / a;
</pre>

<pre>
if (a != 0 and b != 0):
   
(a.x + b.y) % g == 0 because,
>>  a.x % g == 0
>>  b.y % g == 0

So, (c % g != 0) has no soln
</pre>

## Finding One Solution
<pre>
   a.x' + b.y'       = g
>> (a.x' + b.y').k   = g.k
>> a.x'.k + b.y'.k   = g.k
>> a.x'.k + b.y'.k   = c     [let g.k == c]
   
x   = x'.k   = x'.(c/g)
y   = y'.k   = y'.(c/g)
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
..............................................................
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
