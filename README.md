# 🔢 Prime Sieve

A fast, no-nonsense Python script to find all prime numbers up to `n` using the **Sieve of Eratosthenes**.

![Python](https://img.shields.io/badge/Python-3.x-blue?logo=python&logoColor=white)
![License](https://img.shields.io/badge/License-MIT-green)
![Status](https://img.shields.io/badge/Status-Stable-success)

---

## 📋 Table of Contents

- [How it works](#-how-it-works)
- [Usage](#-usage)
- [Example](#-example)
- [Complexity](#-complexity)
- [Code](#-code)
- [FAQ](#-faq)

---

## 🧠 How it works

The **Sieve of Eratosthenes** marks off multiples of every prime starting from 2, leaving only primes unmarked.

```
1. Assume all numbers 2..n are prime
2. Start from the smallest prime (2)
3. Mark all its multiples as NOT prime
4. Move to the next unmarked number, repeat
5. Whatever's left unmarked = primes
```

<details>
<summary>📐 Click to see a visual walkthrough (n = 30)</summary>

```
Start:  2  3  4  5  6  7  8  9 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24 25 26 27 28 29 30
Mark 2: 2  3  X  5  X  7  X  9  X 11  X 13  X 15  X 17  X 19  X 21  X 23  X 25  X 27  X 29  X
Mark 3: 2  3  X  5  X  7  X  X  X 11  X 13  X  X  X 17  X 19  X  X  X 23  X 25  X  X  X 29  X
Mark 5: 2  3  X  5  X  7  X  X  X 11  X 13  X  X  X 17  X 19  X  X  X 23  X  X  X  X  X 29  X

Result: [2, 3, 5, 7, 11, 13, 17, 19, 23, 29]
```

</details>

---

## 🚀 Usage

```bash
python3 primes.py
```

You'll be prompted to enter a value for `n`:

```
Enter n: 50
```

<details>
<summary>⚙️ Want to use it as a function instead?</summary>

```python
from primes import primes_upto

result = primes_upto(100)
print(result)
```

</details>

---

## 💻 Example

| Input (`n`) | Output |
|---|---|
| `10` | `[2, 3, 5, 7]` |
| `30` | `[2, 3, 5, 7, 11, 13, 17, 19, 23, 29]` |
| `50` | `[2, 3, 5, 7, 11, 13, 17, 19, 23, 29, 31, 37, 41, 43, 47]` |

```
$ python3 primes.py
Enter n: 50
Primes up to 50: [2, 3, 5, 7, 11, 13, 17, 19, 23, 29, 31, 37, 41, 43, 47]
Count: 15
```

---

## ⏱️ Complexity

| Metric | Value |
|---|---|
| Time | `O(n log log n)` |
| Space | `O(n)` |

<details>
<summary>📊 Why is this faster than trial division?</summary>

Trial division checks each number individually against all smaller numbers — `O(n√n)` overall. The sieve instead eliminates composites in batches by marking multiples, which is dramatically cheaper at scale. For `n = 10^6`, the difference is seconds vs. near-instant.

</details>

---

## 📄 Code

```python
def primes_upto(n):
    if n < 2:
        return []
    sieve = [True] * (n + 1)
    sieve[0] = sieve[1] = False
    for i in range(2, int(n**0.5) + 1):
        if sieve[i]:
            for j in range(i*i, n + 1, i):
                sieve[j] = False
    return [i for i, is_prime in enumerate(sieve) if is_prime]

if __name__ == "__main__":
    n = int(input("Enter n: "))
    result = primes_upto(n)
    print(f"Primes up to {n}: {result}")
    print(f"Count: {len(result)}")
```

---

## ❓ FAQ

<details>
<summary>What's the largest n this can handle?</summary>

Limited mainly by RAM — the sieve list is size `n+1`. `n = 10^8` uses roughly 100MB and runs in a few seconds on a typical machine.

</details>

<details>
<summary>Does it work for n = 0 or 1?</summary>

Yes — returns an empty list `[]`, since there are no primes below 2.

</details>

<details>
<summary>Can I check if a single number is prime instead?</summary>

This script finds *all* primes up to n. For a single primality check, a trial-division function (testing divisibility up to √n) is more efficient than running the full sieve.

</details>

---

**License:** MIT — do whatever you want with it.
