# Sieve of Eratosthenes
## Introduction
<pre>
Sieve of Eratosthenes is an algorithm for finding all the Prime Numbers for 1 to n
in O(n log log n) time
</pre>

## Theory
A number is prime if none of the smaller prime numbers divides it.
If a number is prime, we mark all of its multiple till n as non prime.

### Implementation 1
```c++
int const N = 1e7;
bool prime[N + 1]; // 0, if prime. 1 otherwise.

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
### Imoplementation 2
```c++
// skipped 2's multiple, check this into account while coding
int const N = 1e7;
bool prime[N + 1]; // 0 if prime, 1 otherwise

void primeSieve() {
    prime[0] = prime[1] = 1;
    for (int i = 3; i * i <= N; i += 2) {
        if (prime[i] == 0) { 
            for (int j = i * i; j <= N; j += 2 * i) {
                prime[j] = 1;
            }
        }
    }
}
```
