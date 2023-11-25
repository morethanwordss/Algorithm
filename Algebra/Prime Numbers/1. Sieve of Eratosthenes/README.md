# Sieve of Eratosthenes
Sieve of Eratosthenes is an algorithm for finding all the prime numbers in a segment $[1;n]$ using $O(n \log \log n)$ operations.

The algorithm is very simple:
at the beginning we write down all numbers between 2 and $n$.
We mark all proper multiples of 2 (since 2 is the smallest prime number) as composite.
A proper multiple of a number $x$, is a number greater than $x$ and divisible by $x$.
Then we find the next number that hasn't been marked as composite, in this case it is 3.
Which means 3 is prime, and we mark all proper multiples of 3 as composite.
The next unmarked number is 5, which is the next prime number, and we mark all proper multiples of it.
And we continue this procedure until we processed all numbers in the row.

The idea behind is this:
A number is prime, if none of the smaller prime numbers divides it.
Since we iterate over the prime numbers in order, we already marked all numbers, who are divisible by at least one of the prime numbers, as divisible.
Hence if we reach a cell and it is not marked, then it isn't divisible by any smaller prime number and therefore has to be prime.


## Sieving till root
```c++
int const N = 1e7;
bool prime[N + 1];    // 0, if prime. 1 otherwise.

void primeSieve() {
    prime[0] = prime[1] = 1;
    for (int i = 2; i * i <= N; i ++ ) {
        if (prime[i] == 0) { 
            for (int j = i * i; j <= N; j += i) {
                prime[j] = 1;
            }
        }
    }
}
```

This code first marks all numbers except zero and one as potential prime numbers (marks 0), then it begins the process of sifting composite numbers.
For this it iterates over all numbers from $2$ to $n$.
If the current number $i$ is a prime number, it marks all numbers that are proper multiples of $i$ as composite numbers (marks 1), starting from $i^2$.
Obviously, to find all the prime numbers until $n$, it will be enough just to perform the sifting only by the prime numbers, which do not exceed the root of $n$.

## Sieving by the odd numbers only
```c++
int const N = 1e7;
bool prime[N + 1];    // 0 if prime, 1 otherwise

void primeSieve() {
    prime[0] = prime[1] = 1;
    for (int i = 3; i * i <= N; i += 2) {    // skipped proper multiples of 2, check this into account while coding
        if (prime[i] == 0) { 
            for (int j = i * i; j <= N; j += 2 * i) {
                prime[j] = 1;
            }
        }
    }
}
```
Since all even numbers (except $2$) are composite, we can stop checking even numbers at all. Instead, we need to operate with odd numbers only.

It will reduce the number of operations performing by algorithm approximately in half.

### Segmented Sieve

It follows from the optimization "sieving till root" that there is no need to keep the whole array `is_prime[1...n]` at all time.
For sieving it is enough to just keep the prime numbers until the root of $n$, i.e. `prime[1... sqrt(n)]`, split the complete range into blocks, and sieve each block separately.

Let $s$ be a constant which determines the size of the block, then we have $\lceil {\frac n s} \rceil$ blocks altogether, and the block $k$ ($k = 0 ... \lfloor {\frac n s} \rfloor$) contains the numbers in a segment $[ks; ks + s - 1]$.
We can work on blocks by turns, i.e. for every block $k$ we will go through all the prime numbers (from $1$ to $\sqrt n$) and perform sieving using them.
It is worth noting, that we have to modify the strategy a little bit when handling the first numbers: first, all the prime numbers from $[1; \sqrt n]$  shouldn't remove themselves; and second, the numbers $0$ and $1$ should be marked as non-prime numbers.
While working on the last block it should not be forgotten that the last needed number $n$ is not necessary located in the end of the block.

As discussed previously, the typical implementation of the Sieve of Eratosthenes is limited by the speed how fast you can load data into the CPU caches.
By splitting the range of potential prime numbers $[1; n]$ into smaller blocks, we never have to keep multiple blocks in memory at the same time, and all operations are much more cache-friendlier.
As we are now no longer limited by the cache speeds, we can replace the `vector<bool>` with a `vector<char>`, and gain some additional performance as the processors can handle read and writes with bytes directly and don't need to rely on bit operations for extracting individual bits.
The benchmark ([link](https://gist.github.com/jakobkogler/e6359ea9ced24fe304f1a8af3c9bee0e)) shows, that using a `vector<char>` is about 3x faster in this situation than using a `vector<bool>`.
A word of caution: those numbers might differ depending on architecture, compiler, and optimization levels.

Here we have an implementation that counts the number of primes smaller than or equal to $n$ using block sieving.

```cpp
int count_primes(int n) {
    const int S = 10000;

    vector<int> primes;
    int nsqrt = sqrt(n);
    vector<char> is_prime(nsqrt + 2, true);
    for (int i = 2; i <= nsqrt; i++) {
        if (is_prime[i]) {
            primes.push_back(i);
            for (int j = i * i; j <= nsqrt; j += i)
                is_prime[j] = false;
        }
    }

    int result = 0;
    vector<char> block(S);
    for (int k = 0; k * S <= n; k++) {
        fill(block.begin(), block.end(), true);
        int start = k * S;
        for (int p : primes) {
            int start_idx = (start + p - 1) / p;
            int j = max(start_idx, p) * p - start;
            for (; j < S; j += p)
                block[j] = false;
        }
        if (k == 0)
            block[0] = block[1] = false;
        for (int i = 0; i < S && start + i <= n; i++) {
            if (block[i])
                result++;
        }
    }
    return result;
}
```

The running time of block sieving is the same as for regular sieve of Eratosthenes (unless the size of the blocks is very small), but the needed memory will shorten to $O(\sqrt{n} + S)$ and we have better caching results.
On the other hand, there will be a division for each pair of a block and prime number from $[1; \sqrt{n}]$, and that will be far worse for smaller block sizes.
Hence, it is necessary to keep balance when selecting the constant $S$.
We achieved the best results for block sizes between $10^4$ and $10^5$.

## Find primes in range

Sometimes we need to find all prime numbers in a range $[L,R]$ of small size (e.g. $R - L + 1 \approx 1e7$), where $R$ can be very large (e.g. $1e12$).

To solve such a problem, we can use the idea of the Segmented sieve.
We pre-generate all prime numbers up to $\sqrt R$, and use those primes to mark all composite numbers in the segment $[L, R]$.

```cpp
vector<char> segmentedSieve(long long L, long long R) {
    // generate all primes up to sqrt(R)
    long long lim = sqrt(R);
    vector<char> mark(lim + 1, false);
    vector<long long> primes;
    for (long long i = 2; i <= lim; ++i) {
        if (!mark[i]) {
            primes.emplace_back(i);
            for (long long j = i * i; j <= lim; j += i)
                mark[j] = true;
        }
    }

    vector<char> isPrime(R - L + 1, true);
    for (long long i : primes)
        for (long long j = max(i * i, (L + i - 1) / i * i); j <= R; j += i)
            isPrime[j - L] = false;
    if (L == 1)
        isPrime[0] = false;
    return isPrime;
}
```
Time complexity of this approach is $O((R - L + 1) \log \log (R) + \sqrt R \log \log \sqrt R)$.

It's also possible that we don't pre-generate all prime numbers:

```cpp
vector<char> segmentedSieveNoPreGen(long long L, long long R) {
    vector<char> isPrime(R - L + 1, true);
    long long lim = sqrt(R);
    for (long long i = 2; i <= lim; ++i)
        for (long long j = max(i * i, (L + i - 1) / i * i); j <= R; j += i)
            isPrime[j - L] = false;
    if (L == 1)
        isPrime[0] = false;
    return isPrime;
}
```

Obviously, the complexity is worse, which is $O((R - L + 1) \log (R) + \sqrt R)$. However, it still runs very fast in practice.

## Linear time modification

We can modify the algorithm in a such a way, that it only has linear time complexity.
This approach is described in the article [Linear Sieve](prime-sieve-linear.md).
However, this algorithm also has its own weaknesses.

## Practice Problems

* [Leetcode - Four Divisors](https://leetcode.com/problems/four-divisors/)
* [Leetcode - Count Primes](https://leetcode.com/problems/count-primes/)
* [SPOJ - Printing Some Primes](http://www.spoj.com/problems/TDPRIMES/)
* [SPOJ - A Conjecture of Paul Erdos](http://www.spoj.com/problems/HS08PAUL/)
* [SPOJ - Primal Fear](http://www.spoj.com/problems/VECTAR8/)
* [SPOJ - Primes Triangle (I)](http://www.spoj.com/problems/PTRI/)
* [Codeforces - Almost Prime](http://codeforces.com/contest/26/problem/A)
* [Codeforces - Sherlock And His Girlfriend](http://codeforces.com/contest/776/problem/B)
* [SPOJ - Namit in Trouble](http://www.spoj.com/problems/NGIRL/)
* [SPOJ - Bazinga!](http://www.spoj.com/problems/DCEPC505/)
* [Project Euler - Prime pair connection](https://www.hackerrank.com/contests/projecteuler/challenges/euler134)
* [SPOJ - N-Factorful](http://www.spoj.com/problems/NFACTOR/)
* [SPOJ - Binary Sequence of Prime Numbers](http://www.spoj.com/problems/BSPRIME/)
* [UVA 11353 - A Different Kind of Sorting](https://uva.onlinejudge.org/index.php?option=com_onlinejudge&Itemid=8&page=show_problem&problem=2338)
* [SPOJ - Prime Generator](http://www.spoj.com/problems/PRIME1/)
* [SPOJ - Printing some primes (hard)](http://www.spoj.com/problems/PRIMES2/)
* [Codeforces - Nodbach Problem](https://codeforces.com/problemset/problem/17/A)
* [Codeforces - Colliders](https://codeforces.com/problemset/problem/154/B)
