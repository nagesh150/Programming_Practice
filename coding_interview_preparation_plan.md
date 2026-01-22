# 🚀 Coding Interview Mastery Plan for Embedded Developers

## 📋 Table of Contents

1. [Understanding Your Challenge](#understanding-your-challenge)
2. [The Problem-Solving Framework (UMPIRE)](#the-problem-solving-framework)
3. [Phase 1: Foundation Building (Weeks 1-4)](#phase-1-foundation-building)
4. [Phase 2: Pattern Recognition (Weeks 5-8)](#phase-2-pattern-recognition)
5. [Phase 3: Advanced Problem Solving (Weeks 9-12)](#phase-3-advanced-problem-solving)
6. [Phase 4: Interview Simulation (Weeks 13-16)](#phase-4-interview-simulation)
7. [Daily Practice Routine](#daily-practice-routine)
8. [Visualization Techniques](#visualization-techniques)
9. [Common Patterns Cheat Sheet](#common-patterns-cheat-sheet)
10. [Resources & Tools](#resources--tools)

---

## 🎯 Understanding Your Challenge

### Why Embedded Developers Struggle with Coding Questions

```
┌─────────────────────────────────────────────────────────────────┐
│                    EMBEDDED DEVELOPER MINDSET                    │
├─────────────────────────────────────────────────────────────────┤
│  ✓ Hardware-centric thinking                                    │
│  ✓ Register manipulation                                        │
│  ✓ Real-time constraints                                        │
│  ✓ Memory-conscious programming                                 │
│  ✓ Protocol implementation (I2C, SPI, UART)                     │
│                                                                  │
│  BUT...                                                          │
│                                                                  │
│  ✗ Less exposure to abstract data structures                    │
│  ✗ Fewer algorithmic challenges in daily work                   │
│  ✗ Focus on "how to do" vs "optimal way to do"                  │
└─────────────────────────────────────────────────────────────────┘
```

### The Good News 🎉

Your embedded background gives you **unique advantages**:

- **Memory awareness** - You already think about space complexity
- **Efficiency mindset** - Embedded code must be optimal
- **Debugging skills** - You can trace through code mentally
- **Bit manipulation** - A topic many struggle with, you excel at!

---

## 🧠 The Problem-Solving Framework (UMPIRE)

**Before writing ANY code, follow this framework:**

```
╔═══════════════════════════════════════════════════════════════════════╗
║                         U.M.P.I.R.E. METHOD                           ║
╠═══════════════════════════════════════════════════════════════════════╣
║                                                                        ║
║  U - UNDERSTAND the problem                                           ║
║      ├── Read the problem 2-3 times                                   ║
║      ├── Identify inputs, outputs, constraints                        ║
║      ├── Ask clarifying questions                                     ║
║      └── Create examples (including edge cases)                       ║
║                                                                        ║
║  M - MATCH to known patterns                                          ║
║      ├── Does this remind me of any problem I've solved?              ║
║      ├── Which data structure fits best?                              ║
║      └── What algorithmic pattern applies?                            ║
║                                                                        ║
║  P - PLAN your approach                                               ║
║      ├── Write pseudocode first                                       ║
║      ├── Draw diagrams                                                ║
║      ├── Walk through with examples                                   ║
║      └── Identify time & space complexity                             ║
║                                                                        ║
║  I - IMPLEMENT the solution                                           ║
║      ├── Write clean, readable code                                   ║
║      ├── Use meaningful variable names                                ║
║      └── Add comments for complex logic                               ║
║                                                                        ║
║  R - REVIEW your code                                                 ║
║      ├── Trace through with examples                                  ║
║      ├── Check edge cases                                             ║
║      └── Look for bugs                                                ║
║                                                                        ║
║  E - EVALUATE and optimize                                            ║
║      ├── Can we improve time complexity?                              ║
║      ├── Can we reduce space usage?                                   ║
║      └── Discuss trade-offs                                           ║
║                                                                        ║
╚═══════════════════════════════════════════════════════════════════════╝
```

### Example: Applying UMPIRE

**Problem:** Find the duplicate number in an array of n+1 integers where each integer is between 1 and n.

```
┌──────────────────────────────────────────────────────────────────────┐
│ U - UNDERSTAND                                                        │
├──────────────────────────────────────────────────────────────────────┤
│ Input: [1, 3, 4, 2, 2]                                               │
│ Output: 2 (the duplicate)                                            │
│ Constraints: Can't modify array, O(1) extra space                    │
│ Edge cases: What if duplicate at start? At end? Multiple duplicates? │
├──────────────────────────────────────────────────────────────────────┤
│ M - MATCH                                                             │
├──────────────────────────────────────────────────────────────────────┤
│ Patterns to consider:                                                 │
│ - Sorting? ❌ (would modify array)                                   │
│ - Hash Set? ❌ (O(n) space)                                          │
│ - Floyd's Cycle Detection? ✓ (O(1) space, treats array as linked    │
│   list)                                                               │
├──────────────────────────────────────────────────────────────────────┤
│ P - PLAN                                                              │
├──────────────────────────────────────────────────────────────────────┤
│ 1. Use two pointers: slow and fast                                   │
│ 2. Move slow by 1, fast by 2 until they meet                         │
│ 3. Reset one pointer to start                                        │
│ 4. Move both by 1 until they meet again                              │
│ 5. Meeting point is the duplicate                                    │
└──────────────────────────────────────────────────────────────────────┘
```

---

## 📅 Phase 1: Foundation Building (Weeks 1-4)

### Week 1-2: Data Structures Fundamentals

```
┌─────────────────────────────────────────────────────────────────────┐
│                    DATA STRUCTURES PRIORITY                          │
├─────────────────────────────────────────────────────────────────────┤
│                                                                      │
│  ★★★★★ MUST MASTER (Use daily in interviews)                       │
│  ├── Arrays                                                          │
│  ├── Strings                                                         │
│  ├── Hash Maps / Hash Sets                                           │
│  ├── Linked Lists                                                    │
│  └── Two Pointers technique                                          │
│                                                                      │
│  ★★★★☆ VERY IMPORTANT                                               │
│  ├── Stacks                                                          │
│  ├── Queues                                                          │
│  ├── Binary Trees                                                    │
│  └── Binary Search Trees                                             │
│                                                                      │
│  ★★★☆☆ IMPORTANT                                                    │
│  ├── Heaps / Priority Queues                                         │
│  ├── Graphs                                                          │
│  └── Tries                                                           │
│                                                                      │
│  ★★☆☆☆ GOOD TO KNOW                                                 │
│  ├── Union-Find                                                      │
│  ├── Segment Trees                                                   │
│  └── Advanced Graph structures                                       │
│                                                                      │
└─────────────────────────────────────────────────────────────────────┘
```

### Week 1 Tasks

| Day | Topic                    | Practice Problems   | Time  |
| --- | ------------------------ | ------------------- | ----- |
| 1   | Arrays basics            | 3 easy problems     | 2 hrs |
| 2   | Arrays - Two Sum pattern | 3 easy problems     | 2 hrs |
| 3   | Strings basics           | 3 easy problems     | 2 hrs |
| 4   | Hash Maps                | 3 easy problems     | 2 hrs |
| 5   | Hash Sets                | 3 easy problems     | 2 hrs |
| 6   | Review + 1 medium        | Review all concepts | 3 hrs |
| 7   | Rest & Revision          | Light review        | 1 hr  |

### Week 2 Tasks

| Day | Topic                     | Practice Problems   | Time  |
| --- | ------------------------- | ------------------- | ----- |
| 1   | Linked Lists - basics     | 3 easy problems     | 2 hrs |
| 2   | Linked Lists - operations | 3 easy problems     | 2 hrs |
| 3   | Stacks                    | 3 easy problems     | 2 hrs |
| 4   | Queues                    | 3 easy problems     | 2 hrs |
| 5   | Two Pointers              | 3 easy problems     | 2 hrs |
| 6   | Review + 2 medium         | Review all concepts | 3 hrs |
| 7   | Rest & Revision           | Light review        | 1 hr  |

### Week 3-4: Algorithm Fundamentals

```
┌─────────────────────────────────────────────────────────────────────┐
│                    ALGORITHM PRIORITY                                │
├─────────────────────────────────────────────────────────────────────┤
│                                                                      │
│  ★★★★★ MUST MASTER                                                  │
│  ├── Binary Search                                                   │
│  ├── Sorting (understand concepts, not implementation)               │
│  ├── Recursion basics                                                │
│  └── Sliding Window                                                  │
│                                                                      │
│  ★★★★☆ VERY IMPORTANT                                               │
│  ├── BFS (Breadth-First Search)                                      │
│  ├── DFS (Depth-First Search)                                        │
│  ├── Backtracking                                                    │
│  └── Dynamic Programming (basics)                                    │
│                                                                      │
│  ★★★☆☆ IMPORTANT (Especially for FAANG)                            │
│  ├── Bit Manipulation (You're strong here!)                          │
│  ├── Greedy Algorithms                                               │
│  ├── Graph algorithms (Dijkstra, Topological Sort)                   │
│  └── Advanced DP                                                     │
│                                                                      │
└─────────────────────────────────────────────────────────────────────┘
```

---

## 📅 Phase 2: Pattern Recognition (Weeks 5-8)

### The 15 Essential Coding Patterns

```
╔═══════════════════════════════════════════════════════════════════════╗
║                     15 PATTERNS TO MASTER                             ║
╠═══════════════════════════════════════════════════════════════════════╣
║                                                                        ║
║  PATTERN 1: Sliding Window                                            ║
║  ─────────────────────────────                                         ║
║  Use when: Contiguous subarray/substring problems                     ║
║  Example: Maximum sum subarray of size k                              ║
║                                                                        ║
║  [1, 3, 2, 6, -1, 4, 1, 8, 2], k=5                                    ║
║   └──────────┘  → window slides →  └──────────┘                       ║
║                                                                        ║
╠═══════════════════════════════════════════════════════════════════════╣
║                                                                        ║
║  PATTERN 2: Two Pointers                                              ║
║  ───────────────────────                                               ║
║  Use when: Sorted arrays, finding pairs, palindromes                  ║
║  Example: Find pair with target sum in sorted array                   ║
║                                                                        ║
║  [1, 2, 3, 4, 5, 6, 7, 8, 9]                                          ║
║   ↑                       ↑                                           ║
║  left                   right                                         ║
║                                                                        ║
╠═══════════════════════════════════════════════════════════════════════╣
║                                                                        ║
║  PATTERN 3: Fast & Slow Pointers                                      ║
║  ───────────────────────────────                                       ║
║  Use when: Cycle detection, middle of linked list                     ║
║  Example: Detect cycle in linked list                                 ║
║                                                                        ║
║  slow →                                                                ║
║  fast →→                                                               ║
║                                                                        ║
╠═══════════════════════════════════════════════════════════════════════╣
║                                                                        ║
║  PATTERN 4: Merge Intervals                                           ║
║  ──────────────────────────                                            ║
║  Use when: Overlapping intervals, scheduling                          ║
║  Example: Merge overlapping intervals                                 ║
║                                                                        ║
║  [1,3] [2,6] [8,10] → [1,6] [8,10]                                    ║
║                                                                        ║
╠═══════════════════════════════════════════════════════════════════════╣
║                                                                        ║
║  PATTERN 5: Cyclic Sort                                               ║
║  ──────────────────────                                                ║
║  Use when: Array with numbers in range 1 to n                         ║
║  Example: Find missing number                                         ║
║                                                                        ║
╠═══════════════════════════════════════════════════════════════════════╣
║                                                                        ║
║  PATTERN 6: In-place Linked List Reversal                             ║
║  ────────────────────────────────────────                              ║
║  Use when: Reverse parts of linked list without extra space          ║
║                                                                        ║
║  1 → 2 → 3 → 4 → 5  becomes  5 → 4 → 3 → 2 → 1                        ║
║                                                                        ║
╠═══════════════════════════════════════════════════════════════════════╣
║                                                                        ║
║  PATTERN 7: Tree BFS                                                  ║
║  ────────────────────                                                  ║
║  Use when: Level-order traversal, level-by-level processing          ║
║                                                                        ║
║  PATTERN 8: Tree DFS                                                  ║
║  ────────────────────                                                  ║
║  Use when: Path finding, tree traversals                              ║
║                                                                        ║
║  PATTERN 9: Two Heaps                                                 ║
║  ────────────────────                                                  ║
║  Use when: Find median in stream, scheduling                          ║
║                                                                        ║
║  PATTERN 10: Subsets                                                  ║
║  ───────────────────                                                   ║
║  Use when: Permutations, combinations, power set                      ║
║                                                                        ║
║  PATTERN 11: Modified Binary Search                                   ║
║  ──────────────────────────────────                                    ║
║  Use when: Sorted or partially sorted arrays                          ║
║                                                                        ║
║  PATTERN 12: Top K Elements                                           ║
║  ──────────────────────────                                            ║
║  Use when: Find k largest/smallest elements                           ║
║                                                                        ║
║  PATTERN 13: K-way Merge                                              ║
║  ───────────────────────                                               ║
║  Use when: Merge multiple sorted lists                                ║
║                                                                        ║
║  PATTERN 14: Topological Sort                                         ║
║  ────────────────────────────                                          ║
║  Use when: Dependency resolution, scheduling tasks                    ║
║                                                                        ║
║  PATTERN 15: Dynamic Programming                                      ║
║  ───────────────────────────────                                       ║
║  Use when: Optimal substructure + overlapping subproblems             ║
║                                                                        ║
╚═══════════════════════════════════════════════════════════════════════╝
```

### Weekly Pattern Focus

| Week | Patterns to Master             | Problems per Pattern |
| ---- | ------------------------------ | -------------------- |
| 5    | Sliding Window, Two Pointers   | 5-7 each             |
| 6    | Binary Search, Merge Intervals | 5-7 each             |
| 7    | Tree BFS, Tree DFS             | 5-7 each             |
| 8    | Backtracking, Subsets          | 5-7 each             |

---

## 📅 Phase 3: Advanced Problem Solving (Weeks 9-12)

### Focus Areas

```
┌─────────────────────────────────────────────────────────────────────┐
│                    ADVANCED TOPICS                                   │
├─────────────────────────────────────────────────────────────────────┤
│                                                                      │
│  Week 9: Dynamic Programming                                         │
│  ├── Fibonacci-type problems                                         │
│  ├── Grid-based DP                                                   │
│  ├── String DP (LCS, Edit Distance)                                  │
│  └── Knapsack problems                                               │
│                                                                      │
│  Week 10: Graphs                                                     │
│  ├── BFS/DFS on graphs                                               │
│  ├── Shortest path (Dijkstra)                                        │
│  ├── Topological sort                                                │
│  └── Connected components                                            │
│                                                                      │
│  Week 11: Advanced Patterns                                          │
│  ├── Monotonic Stack                                                 │
│  ├── Trie problems                                                   │
│  ├── Union-Find                                                      │
│  └── Heap-based problems                                             │
│                                                                      │
│  Week 12: Company-Specific Prep                                      │
│  ├── Google: Focus on complexity analysis                            │
│  ├── Qualcomm: Bit manipulation, memory                              │
│  ├── Samsung: Implementation, simulation                             │
│  └── Mixed practice                                                  │
│                                                                      │
└─────────────────────────────────────────────────────────────────────┘
```

### DP Problem-Solving Framework

```
╔═══════════════════════════════════════════════════════════════════════╗
║                    DP THINKING PROCESS                                ║
╠═══════════════════════════════════════════════════════════════════════╣
║                                                                        ║
║  Step 1: Can I break the problem into smaller subproblems?            ║
║          YES → Potential DP problem                                   ║
║                                                                        ║
║  Step 2: Do subproblems overlap? (Same subproblem solved multiple     ║
║          times)                                                        ║
║          YES → DP will help                                           ║
║                                                                        ║
║  Step 3: Define the state                                             ║
║          What information do I need to solve the subproblem?          ║
║          dp[i] = ?                                                    ║
║                                                                        ║
║  Step 4: Define the transition                                        ║
║          How do I get dp[i] from previous states?                     ║
║          dp[i] = f(dp[i-1], dp[i-2], ...)                             ║
║                                                                        ║
║  Step 5: Define base cases                                            ║
║          What are the smallest subproblems I can solve directly?      ║
║                                                                        ║
║  Step 6: Choose direction                                             ║
║          Top-down (recursion + memoization) OR                        ║
║          Bottom-up (iterative)                                        ║
║                                                                        ║
╚═══════════════════════════════════════════════════════════════════════╝
```

---

## 📅 Phase 4: Interview Simulation (Weeks 13-16)

### Mock Interview Schedule

```
┌─────────────────────────────────────────────────────────────────────┐
│                    INTERVIEW SIMULATION                              │
├─────────────────────────────────────────────────────────────────────┤
│                                                                      │
│  Week 13: Self-Mock Interviews                                       │
│  ├── 3 problems per day (Easy/Medium/Medium)                         │
│  ├── 45 minutes per problem max                                      │
│  ├── Explain your approach out loud                                  │
│  └── Record yourself if possible                                     │
│                                                                      │
│  Week 14: Peer Mock Interviews                                       │
│  ├── Find interview partners online                                  │
│  ├── Platforms: Pramp, Interviewing.io                               │
│  ├── 2-3 mock interviews per week                                    │
│  └── Practice explaining while coding                                │
│                                                                      │
│  Week 15: Company-Specific Preparation                               │
│  ├── Research company interview patterns                             │
│  ├── Focus on most frequent topics                                   │
│  ├── Review system design basics                                     │
│  └── Prepare behavioral questions                                    │
│                                                                      │
│  Week 16: Final Review                                               │
│  ├── Review all solved problems                                      │
│  ├── Focus on weak areas                                             │
│  ├── Light practice only                                             │
│  └── Rest before interviews                                          │
│                                                                      │
└─────────────────────────────────────────────────────────────────────┘
```

---

## 📆 Daily Practice Routine

### The Ideal Day (2-3 hours)

```
╔═══════════════════════════════════════════════════════════════════════╗
║                    DAILY PRACTICE SCHEDULE                            ║
╠═══════════════════════════════════════════════════════════════════════╣
║                                                                        ║
║  ⏰ 15 min - Quick Review                                             ║
║  └── Review yesterday's problems                                      ║
║  └── Read solutions you struggled with                                ║
║                                                                        ║
║  ⏰ 45 min - Problem 1 (New concept/pattern)                          ║
║  └── Read & understand                          (5 min)               ║
║  └── Plan approach on paper                     (10 min)              ║
║  └── Code solution                              (20 min)              ║
║  └── Test & debug                               (10 min)              ║
║                                                                        ║
║  ⏰ 45 min - Problem 2 (Practice pattern)                             ║
║  └── Same structure as Problem 1                                      ║
║                                                                        ║
║  ⏰ 30 min - Problem 3 (Challenge/Medium)                             ║
║  └── Attempt without hints                                            ║
║  └── If stuck after 15 min, read hints                                ║
║  └── Study optimal solution                                           ║
║                                                                        ║
║  ⏰ 15 min - Reflection                                               ║
║  └── What patterns did I learn?                                       ║
║  └── What mistakes did I make?                                        ║
║  └── What will I practice tomorrow?                                   ║
║                                                                        ║
╚═══════════════════════════════════════════════════════════════════════╝
```

### Weekend Review (4-5 hours)

```
Saturday:
├── 2 hours: Solve 3-4 medium problems
├── 1 hour: Review week's problems
└── 1 hour: Study topics you struggled with

Sunday:
├── 2 hours: 1 contest or timed practice
├── 1 hour: Read solutions and explanations
└── 1 hour: Plan next week's focus areas
```

---

## 🎨 Visualization Techniques

### 1. Draw Everything

```
BEFORE YOU CODE, DRAW:

Arrays:        [1] [3] [5] [7] [9]
                ↑           ↑
               left       right

Linked Lists:  [1] → [2] → [3] → [4] → NULL
                ↑     ↑
              prev  curr

Trees:              [5]
                   /   \
                 [3]   [7]
                /  \   /  \
              [2] [4] [6] [8]

Hash Maps:     key → value
               "a" → 1
               "b" → 2

Stacks:        |   |
               | 3 |
               | 2 |
               | 1 |
               └───┘
```

### 2. Trace Through Examples

```
Problem: Two Sum
Input: [2, 7, 11, 15], target = 9

Step 1: i=0, nums[i]=2, need=7
        HashMap: {}
        7 not in map → add {2: 0}

Step 2: i=1, nums[i]=7, need=2
        HashMap: {2: 0}
        2 IS in map! → return [0, 1] ✓
```

### 3. State Tracking Table

```
For DP problems, create a table:

Problem: Climbing Stairs (n steps, 1 or 2 steps at a time)

| n | ways | Calculation     |
|---|------|-----------------|
| 1 | 1    | Base case       |
| 2 | 2    | Base case       |
| 3 | 3    | dp[2] + dp[1]   |
| 4 | 5    | dp[3] + dp[2]   |
| 5 | 8    | dp[4] + dp[3]   |
```

---

## 📋 Common Patterns Cheat Sheet

### Quick Reference Card

```
╔═══════════════════════════════════════════════════════════════════════╗
║                         PATTERN QUICK REFERENCE                        ║
╠═══════════════════════════════════════════════════════════════════════╣
║                                                                        ║
║  "Find pair with sum X"           → Two Pointers or Hash Map          ║
║  "Subarray with condition"        → Sliding Window                    ║
║  "K largest/smallest"             → Heap                              ║
║  "Cycle in linked list"           → Fast & Slow Pointers              ║
║  "Level by level"                 → BFS                               ║
║  "All paths/combinations"         → Backtracking/DFS                  ║
║  "Optimal with overlaps"          → Dynamic Programming               ║
║  "Sorted + search"                → Binary Search                     ║
║  "Prefix matching"                → Trie                              ║
║  "Connected components"           → Union-Find or DFS                 ║
║  "Intervals overlap"              → Sort by start, merge              ║
║  "Next greater element"           → Monotonic Stack                   ║
║  "Median in stream"               → Two Heaps                         ║
║  "Top K frequent"                 → Hash Map + Heap                   ║
║  "Dependencies/ordering"          → Topological Sort                  ║
║                                                                        ║
╚═══════════════════════════════════════════════════════════════════════╝
```

### Complexity Quick Reference

```
Time Complexity Goals:

O(1)        - Hash map lookup, array access
O(log n)    - Binary search, balanced tree operations
O(n)        - Single pass through data
O(n log n)  - Efficient sorting (merge sort, quick sort)
O(n²)       - Nested loops (try to optimize!)
O(2ⁿ)       - Recursive subsets (often can be improved)
O(n!)       - Permutations (unavoidable for some problems)

Space Complexity:

O(1)        - In-place, constant extra space
O(n)        - Linear extra space (hash map, recursion stack)
O(n²)       - 2D DP table
```

---

## 📚 Resources & Tools

### Practice Platforms (Priority Order)

```
1. LeetCode (Primary)
   ├── Start with "Top Interview Questions" collection
   ├── Focus on Easy → Medium progression
   ├── Use "Company" tag for targeted practice
   └── Join weekly contests

2. NeetCode (Structured Learning)
   ├── Curated 150 problems
   ├── Video explanations
   └── Organized by pattern

3. AlgoExpert (Alternative)
   ├── Good video explanations
   └── Focused problem set

4. HackerRank (Initial Practice)
   ├── Good for beginners
   └── Embedded challenges available
```

### Study Resources

```
Books:
├── "Cracking the Coding Interview" - Gayle McDowell
├── "Grokking Algorithms" - Aditya Bhargava (Visual learner friendly)
└── "Elements of Programming Interviews" - Advanced

YouTube Channels:
├── NeetCode - Pattern explanations
├── Abdul Bari - Algorithm theory
├── Tushar Roy - DP problems
└── Back To Back SWE - Detailed explanations

Courses:
├── Grokking the Coding Interview (Educative)
└── AlgoMonster (Pattern-based)
```

### Tools

```
For Practice:
├── LeetCode IDE
├── Visual Studio Code
└── Online IDEs (Replit, CodeSandbox)

For Visualization:
├── VisuAlgo.net - Algorithm visualization
├── Python Tutor - Code execution visualization
└── Draw.io - Diagrams
```

---

## 🎯 Embedded-Specific Interview Topics

### Topics Where You Have an Advantage

```
╔═══════════════════════════════════════════════════════════════════════╗
║                    YOUR EMBEDDED ADVANTAGES                           ║
╠═══════════════════════════════════════════════════════════════════════╣
║                                                                        ║
║  ✓ Bit Manipulation                                                   ║
║    └── Practice: Set/Clear bits, count bits, power of 2               ║
║    └── Companies love this for embedded roles!                        ║
║                                                                        ║
║  ✓ Memory Management                                                  ║
║    └── Stack vs Heap                                                  ║
║    └── Memory alignment                                               ║
║    └── Cache-friendly code                                            ║
║                                                                        ║
║  ✓ Low-Level Optimization                                             ║
║    └── Loop unrolling concepts                                        ║
║    └── Branch prediction awareness                                    ║
║    └── Inline functions                                               ║
║                                                                        ║
║  ✓ State Machine Design                                               ║
║    └── Common in embedded interviews                                  ║
║    └── Design patterns for FSM                                        ║
║                                                                        ║
║  ✓ Concurrency Basics                                                 ║
║    └── Mutex, semaphores                                              ║
║    └── Race conditions                                                ║
║    └── Interrupt handling                                             ║
║                                                                        ║
╚═══════════════════════════════════════════════════════════════════════╝
```

### Must-Know Bit Manipulation

```c
// Common operations you should know by heart:

// Check if bit is set
bool isBitSet = (num >> pos) & 1;

// Set a bit
num |= (1 << pos);

// Clear a bit
num &= ~(1 << pos);

// Toggle a bit
num ^= (1 << pos);

// Check if power of 2
bool isPowerOf2 = (n > 0) && ((n & (n-1)) == 0);

// Count set bits (Brian Kernighan's algorithm)
int count = 0;
while (n) {
    n = n & (n-1);
    count++;
}

// Get lowest set bit
int lowestBit = n & (-n);

// Clear lowest set bit
n = n & (n-1);
```

---

## 📈 Progress Tracking

### Weekly Self-Assessment

```
╔═══════════════════════════════════════════════════════════════════════╗
║                    WEEKLY PROGRESS TRACKER                            ║
╠═══════════════════════════════════════════════════════════════════════╣
║                                                                        ║
║  Week: ___________                                                     ║
║                                                                        ║
║  Problems Solved:                                                      ║
║  ├── Easy:   ___ / 10                                                 ║
║  ├── Medium: ___ / 5                                                  ║
║  └── Hard:   ___ / 1                                                  ║
║                                                                        ║
║  Patterns Practiced:                                                   ║
║  □ Sliding Window    □ Two Pointers    □ Binary Search               ║
║  □ BFS/DFS           □ Backtracking    □ Dynamic Programming         ║
║  □ Graph             □ Heap            □ Stack/Queue                 ║
║                                                                        ║
║  Self-Rating (1-5):                                                   ║
║  ├── Problem Understanding:  ___                                      ║
║  ├── Solution Planning:      ___                                      ║
║  ├── Code Implementation:    ___                                      ║
║  ├── Bug-free First Try:     ___                                      ║
║  └── Time Management:        ___                                      ║
║                                                                        ║
║  Areas to Improve:                                                     ║
║  _________________________________________________________________    ║
║  _________________________________________________________________    ║
║                                                                        ║
╚═══════════════════════════════════════════════════════════════════════╝
```

---

## 🏆 Success Mindset

### Key Principles

```
╔═══════════════════════════════════════════════════════════════════════╗
║                    MINDSET FOR SUCCESS                                ║
╠═══════════════════════════════════════════════════════════════════════╣
║                                                                        ║
║  1. STRUGGLE IS LEARNING                                              ║
║     Spending 30 minutes stuck on a problem teaches you more           ║
║     than reading 10 solutions.                                        ║
║                                                                        ║
║  2. PATTERNS OVER PROBLEMS                                            ║
║     Don't memorize solutions. Learn the underlying patterns.          ║
║     One pattern can solve hundreds of problems.                       ║
║                                                                        ║
║  3. QUALITY OVER QUANTITY                                             ║
║     Deeply understanding 200 problems > Rushing through 500.          ║
║     Review and revisit problems.                                      ║
║                                                                        ║
║  4. THINK BEFORE CODE                                                 ║
║     10 minutes of planning can save 30 minutes of debugging.          ║
║     Always use UMPIRE method.                                         ║
║                                                                        ║
║  5. EMBRACE FAILURE                                                   ║
║     Every wrong solution is a learning opportunity.                   ║
║     Keep a "mistakes" journal.                                        ║
║                                                                        ║
║  6. CONSISTENCY BEATS INTENSITY                                       ║
║     2 hours daily > 14 hours on weekends.                            ║
║     Build the habit.                                                  ║
║                                                                        ║
║  7. COMMUNICATE CLEARLY                                               ║
║     In interviews, explaining your thought process is as              ║
║     important as the solution itself.                                 ║
║                                                                        ║
╚═══════════════════════════════════════════════════════════════════════╝
```

---

## 🚀 Getting Started Today

### Your First Week Action Plan

```
DAY 1 (Today):
□ Set up LeetCode account
□ Solve 1 Easy array problem
□ Read about Two Sum pattern

DAY 2:
□ Solve 2 Easy array problems
□ Learn Hash Map basics

DAY 3:
□ Solve 2 Easy string problems
□ Practice explaining solutions out loud

DAY 4:
□ Solve 2 Easy Two Pointer problems
□ Start tracking your progress

DAY 5:
□ Solve 2 Easy hash map problems
□ Review all problems from the week

DAY 6:
□ Attempt 1 Medium problem
□ Don't worry if you can't solve it - read the solution

DAY 7:
□ Rest and light review
□ Plan next week's focus
```

---

**Remember**: You already have the foundation. As an embedded developer, you understand:

- How memory works
- How to optimize code
- How to debug systematically
- How computers actually work at a low level

Now you just need to **map this knowledge** to algorithm problems. The patterns are your bridge!

**Good luck on your interview preparation! 🎯**

---

_Created: January 22, 2026_
_Target Companies: Google, Qualcomm, Samsung, and other top product companies_
