# Linear Diophantine Equation
## Introduction
A Linear Diophantine Equation is an equation of the general form,
<pre>a.x + b.y = c </pre>
Where `a`, `b`, `c` are given integers, and `x`, `y` are unknown integers.

There are 4 classical problems on this equation, 
- Finding one solution
- Finding all solution
- Finding the number of solutions and the solutions themselves in a given interval
- finding a solution with minimum value of `x + y`
## Analysis
>> If a == 0 and b == 0
<pre>
   a.x + b.y = c
>> 0.x + 0.y = c
>> 0 + 0 = c
>> c = 0
</pre>
Therefore, if `a == 0` and `b == 0`, the equation `a.x + b.y = c` has no solution if `c != 0` and has infinite many solution if `c == 0` .
>> If a != 0 and b != 0

In the equation `a.x + b.y = c`,
- `a` is divisible by `gcd(a, b)`
- `a.x` is disible by `gcd(a, b)`
- `b` is divisible by `gcd(a, b)`
- `b.y` is divisible by `gcd(a, b)`
- `a.x + b.y` is divisble by `gcd(a, b)`
  
As, `c = a.x + b.y` and `a.x + b.y` is divisble by `gcd(a, b)`, `c` also has to be divisbile by `gcd(a, b)`.

If `c` is not divisible by `gcd(a, b)`, there is no solution to the equation, `a.x + b.y = c`

## Finding One Solution
From the Extended Euclidean Algorithm we can find the value of `(x', y')` for the equation `a.x' + b.y' = gcd(a, b)`.
