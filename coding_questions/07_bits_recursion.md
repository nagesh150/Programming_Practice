# 🎯 Part 7: Bit Manipulation & Recursion (Questions 76-85)

## 🔥 YOUR STRENGTH AS EMBEDDED DEVELOPER!

As an embedded developer, bit manipulation is your superpower!

---

## Question 76: Count Set Bits (1s in binary)

### Visualization

```
Number: 13
Binary: 1101

Count 1s:
┌────────────────────────────────────────────────┐
│ Method 1: Brian Kernighan Algorithm            │
│                                                │
│ n = 13 = 1101                                 │
│ n & (n-1) clears the rightmost set bit!       │
│                                                │
│ n = 1101, n-1 = 1100                          │
│ n & (n-1) = 1100, count=1                     │
│                                                │
│ n = 1100, n-1 = 1011                          │
│ n & (n-1) = 1000, count=2                     │
│                                                │
│ n = 1000, n-1 = 0111                          │
│ n & (n-1) = 0000, count=3                     │
│                                                │
│ n = 0, STOP! Answer = 3 bits                  │
└────────────────────────────────────────────────┘
```

### C Code

```c
int countSetBits(int n) {
    int count = 0;
    while (n) {
        n = n & (n - 1);  // Clear rightmost set bit
        count++;
    }
    return count;
}
```

---

## Question 77: Check if Power of 2

### Visualization

```
Powers of 2 have exactly ONE set bit:
1  = 0001
2  = 0010
4  = 0100
8  = 1000
16 = 10000

Trick: n & (n-1) == 0 for powers of 2!
┌────────────────────────────────────────────────┐
│ n=8: 1000                                      │
│ n-1: 0111                                      │
│    & ────                                      │
│      0000 ✓ Power of 2!                       │
│                                                │
│ n=6: 0110                                      │
│ n-1: 0101                                      │
│    & ────                                      │
│      0100 ✗ Not power of 2                    │
└────────────────────────────────────────────────┘
```

### C Code

```c
bool isPowerOfTwo(int n) {
    return (n > 0) && ((n & (n - 1)) == 0);
}
```

---

## Question 78: Find Single Number (Others appear twice)

### Visualization

```
Array: [4, 1, 2, 1, 2]

XOR Properties:
- a ^ a = 0    (same numbers cancel)
- a ^ 0 = a    (XOR with 0 gives same)
- XOR is commutative and associative

┌────────────────────────────────────────────────┐
│ 4 ^ 1 ^ 2 ^ 1 ^ 2                             │
│ = 4 ^ (1 ^ 1) ^ (2 ^ 2)                       │
│ = 4 ^ 0 ^ 0                                    │
│ = 4 ✓                                         │
└────────────────────────────────────────────────┘
```

### C Code

```c
int singleNumber(int arr[], int n) {
    int result = 0;
    for (int i = 0; i < n; i++) {
        result ^= arr[i];
    }
    return result;
}
```

---

## Question 79: Swap Two Numbers Without Temp

### Visualization

```
a = 5 (0101), b = 3 (0011)

Using XOR:
┌────────────────────────────────────────────────┐
│ a = a ^ b = 0101 ^ 0011 = 0110    (a=6)       │
│ b = a ^ b = 0110 ^ 0011 = 0101    (b=5)       │
│ a = a ^ b = 0110 ^ 0101 = 0011    (a=3)       │
│                                                │
│ Result: a=3, b=5 (SWAPPED!)                   │
└────────────────────────────────────────────────┘
```

### C Code

```c
void swap(int *a, int *b) {
    *a = *a ^ *b;
    *b = *a ^ *b;
    *a = *a ^ *b;
}
```

---

## Question 80: Set, Clear, Toggle Bit

### Visualization

```
EMBEDDED DEVELOPERS USE THIS DAILY!

Number n = 5 (0101), position pos = 1

┌────────────────────────────────────────────────┐
│ SET bit at position pos:                       │
│ n | (1 << pos)                                │
│ 0101 | 0010 = 0111 (7)                        │
│                                                │
│ CLEAR bit at position pos:                     │
│ n & ~(1 << pos)                               │
│ 0101 & 1101 = 0101 (5, bit was already 0)     │
│                                                │
│ TOGGLE bit at position pos:                    │
│ n ^ (1 << pos)                                │
│ 0101 ^ 0010 = 0111 (7)                        │
│                                                │
│ CHECK if bit is set:                           │
│ (n >> pos) & 1                                │
│ (0101 >> 1) & 1 = 0010 & 0001 = 0             │
└────────────────────────────────────────────────┘
```

### C Code

```c
// Set bit
int setBit(int n, int pos) {
    return n | (1 << pos);
}

// Clear bit
int clearBit(int n, int pos) {
    return n & ~(1 << pos);
}

// Toggle bit
int toggleBit(int n, int pos) {
    return n ^ (1 << pos);
}

// Check bit
int getBit(int n, int pos) {
    return (n >> pos) & 1;
}
```

---

## Question 81: Factorial using Recursion

### Visualization

```
factorial(5) = 5 × 4 × 3 × 2 × 1 = 120

Recursive call stack:
┌────────────────────────────────────────────────┐
│ factorial(5)                                   │
│   └─ 5 * factorial(4)                         │
│         └─ 4 * factorial(3)                   │
│               └─ 3 * factorial(2)             │
│                     └─ 2 * factorial(1)       │
│                           └─ 1 (base case)    │
│                                                │
│ Unwinding:                                     │
│ factorial(1) = 1                              │
│ factorial(2) = 2 * 1 = 2                      │
│ factorial(3) = 3 * 2 = 6                      │
│ factorial(4) = 4 * 6 = 24                     │
│ factorial(5) = 5 * 24 = 120                   │
└────────────────────────────────────────────────┘
```

### C Code

```c
int factorial(int n) {
    if (n <= 1) return 1;  // Base case
    return n * factorial(n - 1);
}
```

---

## Question 82: Fibonacci using Recursion

### Visualization

```
Fibonacci: 0, 1, 1, 2, 3, 5, 8, 13...
F(n) = F(n-1) + F(n-2)

fib(5) call tree:
┌────────────────────────────────────────────────┐
│              fib(5)                            │
│            /       \                           │
│        fib(4)     fib(3)                      │
│        /    \      /    \                      │
│    fib(3) fib(2) fib(2) fib(1)               │
│    /   \    |      |                          │
│ fib(2) fib(1) ...  ...                       │
│                                                │
│ Notice: fib(3), fib(2) calculated multiple    │
│ times! This is why DP helps.                  │
└────────────────────────────────────────────────┘
```

### C Code

```c
// Simple recursion (slow)
int fib(int n) {
    if (n <= 1) return n;
    return fib(n-1) + fib(n-2);
}

// DP version (fast)
int fibDP(int n) {
    if (n <= 1) return n;
    int prev2 = 0, prev1 = 1;
    for (int i = 2; i <= n; i++) {
        int curr = prev1 + prev2;
        prev2 = prev1;
        prev1 = curr;
    }
    return prev1;
}
```

---

## Question 83: Reverse Number using Recursion

### Visualization

```
Number: 1234 → Reversed: 4321

┌────────────────────────────────────────────────┐
│ 1234 % 10 = 4 (last digit)                    │
│ 1234 / 10 = 123 (remaining)                   │
│                                                │
│ Build reversed: 4 * 1000 + reverse(123)       │
│                 = 4000 + 321                   │
│                 = 4321                         │
└────────────────────────────────────────────────┘
```

---

## Question 84: Check Palindrome Number

### Visualization

```
121 → Reversed = 121 → PALINDROME ✓
123 → Reversed = 321 → NOT PALINDROME ✗
```

### C Code

```c
bool isPalindromeNum(int n) {
    if (n < 0) return false;

    int original = n;
    int reversed = 0;

    while (n > 0) {
        reversed = reversed * 10 + n % 10;
        n /= 10;
    }

    return original == reversed;
}
```

---

## Question 85: GCD (Greatest Common Divisor)

### Visualization (Euclidean Algorithm)

```
GCD(48, 18):
┌────────────────────────────────────────────────┐
│ 48 = 18 * 2 + 12    → GCD(18, 12)            │
│ 18 = 12 * 1 + 6     → GCD(12, 6)             │
│ 12 = 6 * 2 + 0      → GCD(6, 0)              │
│                                                │
│ When remainder = 0, GCD = 6                   │
└────────────────────────────────────────────────┘
```

### C Code

```c
int gcd(int a, int b) {
    if (b == 0) return a;
    return gcd(b, a % b);
}

// LCM = (a * b) / GCD(a, b)
int lcm(int a, int b) {
    return (a * b) / gcd(a, b);
}
```

---

## Bit Manipulation Cheat Sheet

```
┌────────────────────────────────────────────────────┐
│ OPERATION          │ CODE                          │
├────────────────────┼──────────────────────────────┤
│ Set bit at pos     │ n | (1 << pos)              │
│ Clear bit at pos   │ n & ~(1 << pos)             │
│ Toggle bit at pos  │ n ^ (1 << pos)              │
│ Check bit at pos   │ (n >> pos) & 1              │
│ Clear lowest set   │ n & (n - 1)                 │
│ Get lowest set     │ n & (-n)                    │
│ Is power of 2?     │ n && !(n & (n-1))          │
│ Count set bits     │ Loop with n & (n-1)        │
│ Swap a, b          │ a^=b; b^=a; a^=b;          │
│ Even/Odd check     │ n & 1 (0=even, 1=odd)      │
│ Multiply by 2^k    │ n << k                      │
│ Divide by 2^k      │ n >> k                      │
└────────────────────┴──────────────────────────────┘
```
