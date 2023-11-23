# Extended Euclidean Algorithm

<pre>
Problem:
   
a.x + b.y = gcd(a, b)
Given the value of (a, b), We have to find out the value of (x, y) such that it satisfies the equation.
</pre>

## Theory
<img width="518" alt="Screenshot 2023-11-23 150056" src="https://github.com/t0-ji/Algorithm/assets/108709544/4bf74c87-3ec6-4dd0-999a-d42985cf1bc2"> <br>
<pre>
Let gcd(a, b) = g
This recursion ends with current (a, b) = (g, 0)
</pre>
<pre>
   a.x + b.y = g
>> g.x + 0.y = g [replacing (a, b) wiith (g, 0)]
</pre>
<pre>
For this equation, a solution for (x, y) is (1, 0) for (a, b) = (g, 0) --> This is the Base Case
</pre>
<pre>
Now we have to calculate how (x, y) changes as the recursion goes bottoms up from (b, a mod b) to (a, b).
g remains same in every state of the recursion while going bottom up.
And the toppest value of (x, y) will be our desired result for the final a.x + b.y = g
</pre>
<pre>
let (x, y) be the solution for (a, b) in any state of the recursion.
Lets assume in the next recursive call, (x, y) becomes (x', y') and by the defintion, (a, b) becomes(b, a mod b).  
</pre>

<pre>
Therefore, 
          
          b.x' + (a mod b).y'               = g          
>>        b.x' + (a - ceil(a/b).b).y'       = g    [substituting a mod b with a - ceil(a/b)*b]      
>>        b.x' + a.y' - ceil(a/b).b.y'      = g
>>        a.y' + b.x' - ceil(a/b).b.y'      = g
>>        a.y' + b(x' - ceil(a/b).y')       = g
</pre>
<pre>
from this equation, We can say that
x = y'
y = x' - ceil(a / b) . y' --> These two are the Function of how (x, y) changes while the recursion goes bottom up
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
