# Fibonacci Numbers
## Introduction
The Fibonacci sequence is defined as follows:
<pre>
F<sub>0</sub> = 0
F<sub>1</sub> = 1
F<sub>n</sub> = F<sub>n-1</sub> + F<sub>n-2</sub>
</pre>
The First elements of the Sequence are,
<pre>
0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89, ...
</pre>
## Properties
_Cassini's Identity:_
<pre>
F<sub>n-1</sub>.F<sub>n+1</sub> - F<sub>n</sub><sup>2</sup> = (-1)<sup>n</sup>
</pre>
_The "Addition" Rule:_
<pre>
F<sub>n+k</sub> = F<sub>k</sub>.F<sub>n+1</sub> + F<sub>k-1</sub>.F<sub>n</sub>
</pre>
For `k == n`,
<pre>
   F<sub>2n</sub> = F<sub>n</sub>.F<sub>n+1</sub> + F<sub>n-1</sub>.F<sub>n</sub>
>> F<sub>2n</sub> = F<sub>n</sub>(F<sub>n+1</sub> + F<sub>n-1</sub>)
</pre>
Therefore, we can say that,
<pre>
>> For any positive integer k , F<sub>nk</sub> is a multiple of F<sub>n</sub>
>> If F<sub>m</sub> is a multiple of F<sub>n</sub> , m is a multiple of n
</pre>
_GCD Identity:_
<pre>
GCD(F<sub>m</sub> , F<sub>n</sub>) = F<sub>GCD(m, n)</sub>
</pre>
Fibonacci numbers are the worst possible inputs for Euclidean algorithm <br>
According to Zeckendorf's theorem, any natural number `n` can be uniquely represented as a sum of Fibonacci numbers
<pre>
 1   = 1             = F<sub>2</sub>
 2   = 2             = F<sub>3</sub>
 6   = 5 + 1         = F<sub>5</sub> + F<sub>2</sub>
 8   = 8             = F<sub>6</sub>
 9   = 8 + 1         = F<sub>6</sub> + F<sub>2</sub>
19   = 13 + 5 + 1    = F<sub>7</sub> + F<sub>5</sub> + F<sub>2</sub>
</pre>
Notice, any number `n` is not represented by the summation of two consecutive Fibonacci Numbers, as the summation of two consecutive fibonacci number will be another ficonacci number by the definition. <br>
For example,
<pre>
5 is not represented as F<sub>4</sub> + F<sub>3</sub> , but
5 is represented as F<sub>5</sub>
</pre>
Any number can be uniquely encoded in the Fibonacci coding, and we can describe this representation with binary code as <pre>b<sub>0</sub>b<sub>1</sub>b<sub>1</sub>b<sub>2</sub>...b<sub>n</sub>**1**
Where, b<sub>i</sub> is `1` if F<sub>i+2</sub> is used in the representation, otherwise `0` </pre> 
Again, notice the binary code representation ends with an additional `1` at the end. This is the only occurance where `two consecutive 1` appears (_We have previously proved that any number_ `n` _is not represented by the summation of two consecutive Fibonacci Numbers, as the summation of two consecutive fibonacci number will be another ficonacci number by the definition_) which can be identified as the end of the representation.
<pre>
 1   = 1             = F2              = (11)<sub>F</sub>
 2   = 2             = F3              = (011)<sub>F</sub>
 6   = 5 + 1         = F5 + F2         = (10011)<sub>F</sub>
 8   = 8             = F6              = (000011)<sub>F</sub>
 9   = 8 + 1         = F6 + F2         = (100011)<sub>F</sub>
19   = 13 + 5 + 1    = F7 + F5 + F2    = (1001011)<sub>F</sub>
</pre>
The encoding of an integer `n` can be done with a simple greedy algorithm.
<pre>
1. Iterate through the Fibonacci numbers from the largest to the smallest until you find one less than or equal to n .
2. Suppose this number was F<sub>i</sub> .
   Subtract F<sub>i</sub> from n and put a 1 in the (i - 2) position of the code word (indexing from 0 from the leftmost to the rightmost bit).
3. Repeat until there is no remainder.
4. Add a final 1 to the codeword to indicate its end.
</pre>
<pre>
Example:
The format: b<sub>0</sub>b<sub>1</sub>b<sub>1</sub>b<sub>2</sub>...b<sub>n</sub>
Initially (for i = 0 to n) b<sub>i</sub> = 0

13 = F<sub>7</sub> + F<sub>5</sub> + F<sub>2</sub>

For F<sub>7</sub>, b<sub>7-2</sub> = b<sub>5</sub> = 1
For F<sub>5</sub>, b<sub>5-2</sub> = b<sub>3</sub> = 1
For F<sub>2</sub>, b<sub>2-2</sub> = b<sub>0</sub> = 1
   
Resulting Code: 100101
After adding a final 1 to the code to indicate its end: 1001011
</pre>
## N<sup>th</sup> Fibonacci Number
### Binet's Formula
<pre>
Let c<sub>1</sub>  = (1 + sqrt(5)) / 2
and c<sub>2</sub> = (1 - sqrt(5)) / 2
F<sub>n</sub> = (c<sub>1</sub><sup>n</sup> - c<sub>2</sub><sup>n</sup>) / sqrt(5) ..... (Binet's Formula)
</pre>
Notice, c<sub>2</sub> is always less than 1 and it also decreases exponentially. Hence c<sub>1</sub> alone is "Almost" F<sub>n</sub> .
So, this can be written strictly as,
<pre>
F<sub>n</sub> = round(c<sub>1</sub> / sqrt(5))
</pre>
As these two formulas would require very high accuracy when working with fractional numbers, they are of little use in practical calculations.
### In Linear Time
```c++
/* c++ */
int fib(int n) {
    int a = 0;
    int b = 1;
    for (int i = 0; i < n; i++) {
        int tmp = a + b;
        a = b;
        b = tmp;
    }
    return a;
}
```
```python
# Python
def fib(n):
    a, b = 0, 1
    for i in range(n):
        tmp = a + b
        a, b = b, tmp
    return a
```
### Matrix Form
Notice the following relation, <br>
<img width="189" alt="Screenshot 2023-11-21 215833" src="https://github.com/t0-ji/Algorithm/assets/108709544/6b0b9e36-ac7f-47b1-b797-60e30035fa75"> <br>
We can find F<sub>n</sub> in `O(log n)` Time by applying Binary Exponentiation to raise the matrix to `n`.
```c++
/* c++ */
struct matrix {
    long long mat[2][2];
    matrix friend operator *(const matrix &a, const matrix &b){
        matrix c;
        for (int i = 0; i < 2; i++) {
          for (int j = 0; j < 2; j++) {
              c.mat[i][j] = 0;
              for (int k = 0; k < 2; k++) {
                  c.mat[i][j] += a.mat[i][k] * b.mat[k][j];
              }
          }
        }
        return c;
    }
};

matrix matpow(matrix base, long long n) {
    matrix ans{ {
      {1, 0},
      {0, 1}
    } };
    while (n) {
        if(n&1)
            ans = ans*base;
        base = base*base;
        n >>= 1;
    }
    return ans;
}

long long fib(int n) {
    matrix base{ {
      {1, 1},
      {1, 0}
    } };
    return matpow(base, n).mat[0][1];
}
```
```python
# Python
class Matrix:
    def __init__(self, mat):
        self.mat = mat

    def __mul__(self, other):
        c = [[0, 0], [0, 0]]
        for i in range(2):
            for j in range(2):
                c[i][j] = 0
                for k in range(2):
                    c[i][j] += self.mat[i][k] * other.mat[k][j]
        return Matrix(c)

def matpow(base, n):
    ans = Matrix([[1, 0], [0, 1]])
    while n:
        if n & 1:
            ans = ans * base
        base = base * base
        n >>= 1
    return ans

def fib(n):
    base = Matrix([[1, 1], [1, 0]])
    return matpow(base, n).mat[0][1]
```

