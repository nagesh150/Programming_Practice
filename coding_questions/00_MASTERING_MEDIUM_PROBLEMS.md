# 🚀 Mastering Medium Coding Questions: A Guide for Embedded Engineers

As an embedded engineer with 5 years of experience, you already have superpowers that many pure software engineers lack: **you understand memory, pointers, and how data actually lives in hardware.**

The frustration you feel with "Medium" complexity problems is usually not a lack of coding skill, but a lack of **"Algorithmic Pattern Recognition"**.

This guide is designed to bridge the gap between **Embedded Thinking** (Registers, ISRs, Memory) and **Algorithmic Thinking** (Complexity, Abstract Patterns).

---

## 🧠 The Mindset Shift

| Embedded approach                            | Algorithmic approach                                      |
| :------------------------------------------- | :-------------------------------------------------------- |
| "How do I manipulate these bits/bytes?"      | "What is the most efficient way to get the answer?"       |
| Optimization = Less RAM/Flash, Faster Cycles | Optimization = Lower Big-O (Time/Space Complexity)        |
| Tools: Debugger, Oscilloscope                | Tools: Hash Maps, Patterns (Two Pointers, Sliding Window) |

**You don't need to relearn coding.** You just need to map your existing knowledge to new patterns.

---

## 🛠 The 4-Step Strategy for Medium Problems

When you see a new medium problem and feel stuck: **STOP. Do not write code yet.**

### Step 1: Default to Brute Force (The "Naive" Driver)

First, solve it the way you would if performance didn't matter.

- "I'll just check every single subarray."
- "I'll comparing every number with every other number."
- **Write this logic down (or pseudo-code it).**
- _Why?_ Getting ONE working solution breaks the mental block.

### Step 2: Visualization (The "Oscilloscope" View)

Draw the specific example input.

- Don't just look at the numbers. Draw them as boxes.
- Use arrows to represent pointers (indexes).
- **Manually** solve the problem on paper. Watch your own eyes/hand.
  - Did you scan back?
  - Did you jump ahead?
  - That "jump" is the optimization you need to code!

### Step 3: Identify the Bottleneck (Profiling)

Look at your Brute Force approach.

- Are you re-calculating the same thing over and over?
- Are you checking data you already know isn't the answer?

### Step 4: Apply a Pattern (The "Hardware Accelerator")

Most "Medium" array/string problems fall into just 3 buckets suitable for embedded minds:

1.  **Two Pointers**: Like standard RX/TX ring buffer pointers.
2.  **Sliding Window**: Like processing a signal sample window (moving average).
3.  **Hash Map / Frequency Array**: Like a Lookup Table (LUT) or Register Map.

---

## 💡 Pattern 1: The Sliding Window (Signal Processing)

**Use when**: You need to find a subarray/substring that meets a criteria (longest, shortest, sum equals X).

**Embedded Analogy**: Think of it like a **Moving Average filter** or an **oscilloscope window**. You have a `start` and `end` pointer defining the visible data.

### Example: "Longest Substring Without Repeating Characters"

Input: `abcabcbb`

**Brute Force ($O(N^2)$)**:
Check `a`, `ab`, `abc`, `abca` (fail), start over from `b`...

**Embedded/Sliding Window Approach ($O(N)$)**:
Imagine a UART FIFO buffer.

1.  `Right` pointer pushes data in (New char arrives).
2.  Check: "Do I already have this char in my active buffer?"
    - **Yes**: `Left` pointer pops data out (increment `Left`) until the duplicate is gone.
3.  Calculate Window Size (`Right - Left + 1`).
4.  Repeat.

```c
// Pseudo-C Visualization
while (right < n) {
    char newChar = buffer[right];

    // If 'newChar' is already inside current window [left...right-1]
    while (existsInWindow(newChar)) {
        removeChar(buffer[left]);
        left++; // Shrink window from start
    }

    addChar(newChar);
    updateMaxLength();
    right++; // Expand window
}
```

---

## 💡 Pattern 2: Two Pointers (Ring Buffers)

**Use when**: Sorted arrays, or swapping values.

**Embedded Analogy**: `Head` and `Tail` pointers in a Circular Buffer / Ring Buffer.

### Example: "Container With Most Water" (Classic Medium)

You have an array of heights. Find two lines that form the biggest container.

**The Logic**:

1.  Put one pointer at the **Start** (`left`) and one at the **End** (`right`).
2.  Calculate area.
3.  **Move the "weaker" pointer.**
    - If `height[left] < height[right]`, moving `right` in can ONLY make the area smaller (width decreases, height is limited by left).
    - So, we MUST move `left` to hope for a better height.

---

## 💡 Pattern 3: Lookup Tables (Hash Maps)

**Use when**: You need to check "Have I seen this before?" or "Where is X located?" instantly.

**Embedded Analogy**: **Look-up Tables (LUTs)** or **Direct Memory Access**.
Instead of searching through memory (Loop), you use the value as an _offset_ to jump directly to the address.

- `map[key] = value` is just `base_address[offset] = data`.

---

## 🗓 Suggested Practice Plan (Bootloader Mode)

Don't grind random questions. Build a driver.

**Week 1: The Sliding Window**

- Focus ONLY on Sliding Window problems.
- Problem: Max Consecutive Ones III (Medium)
- Problem: Longest Substring Without Repeating Characters (Medium)
- Problem: Permutation in String (Medium)

**Week 2: Two Pointers**

- Problem: Container With Most Water (Medium)
- Problem: 3Sum (Medium)

**Week 3: Lookup Tables (Hash Maps)**

- Problem: Subarray Sum Equals K (Medium)
- Problem: Group Anagrams (Medium)

Remember: **Frustration is just the debugger telling you that the logic isn't compiling in your brain yet.** It means you are learning. Deep breath. Draw the boxes.
