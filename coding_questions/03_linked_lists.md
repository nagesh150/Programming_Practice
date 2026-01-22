# 🎯 Part 3: Linked List Problems (Questions 31-45)

## Question 31: Reverse a Linked List

### Visualization

```
Original: 1 → 2 → 3 → 4 → NULL

Step-by-step reversal:
┌────────────────────────────────────────────────┐
│ prev=NULL, curr=1                              │
│                                                │
│ NULL ← 1    2 → 3 → 4 → NULL                  │
│        ↑    ↑                                  │
│      prev  curr                                │
│                                                │
│ NULL ← 1 ← 2    3 → 4 → NULL                  │
│             ↑    ↑                             │
│           prev  curr                           │
│                                                │
│ NULL ← 1 ← 2 ← 3    4 → NULL                  │
│                  ↑    ↑                        │
│                prev  curr                      │
│                                                │
│ NULL ← 1 ← 2 ← 3 ← 4   NULL                   │
│                     ↑    ↑                     │
│                   prev  curr                   │
│                                                │
│ Result: 4 → 3 → 2 → 1 → NULL                  │
└────────────────────────────────────────────────┘
```

### C Code

```c
struct Node {
    int data;
    struct Node* next;
};

struct Node* reverseList(struct Node* head) {
    struct Node* prev = NULL;
    struct Node* curr = head;
    struct Node* next = NULL;

    while (curr != NULL) {
        next = curr->next;    // Save next
        curr->next = prev;    // Reverse link
        prev = curr;          // Move prev forward
        curr = next;          // Move curr forward
    }
    return prev;  // New head
}
```

### Memory Trick

```
Think of it as: "Save, Reverse, Move, Move"
1. Save next node
2. Reverse current's pointer
3. Move prev to current
4. Move current to next
```

---

## Question 32: Detect Cycle in Linked List

### Visualization (Floyd's Algorithm)

```
List with cycle:
1 → 2 → 3 → 4 → 5
        ↑       ↓
        └───────┘

Two Pointers: Slow (1 step), Fast (2 steps)
┌────────────────────────────────────────────────┐
│ Start: slow=1, fast=1                          │
│                                                │
│ Step 1: slow=2, fast=3                         │
│ Step 2: slow=3, fast=5                         │
│ Step 3: slow=4, fast=4  ← MEET! Cycle exists  │
└────────────────────────────────────────────────┘

No cycle: fast reaches NULL
```

### C Code

```c
bool hasCycle(struct Node* head) {
    struct Node* slow = head;
    struct Node* fast = head;

    while (fast != NULL && fast->next != NULL) {
        slow = slow->next;         // Move 1 step
        fast = fast->next->next;   // Move 2 steps

        if (slow == fast) {
            return true;  // Cycle detected!
        }
    }
    return false;  // No cycle
}
```

---

## Question 33: Find Middle of Linked List

### Visualization

```
List: 1 → 2 → 3 → 4 → 5

Fast moves 2x speed of slow:
┌────────────────────────────────────────────────┐
│ 1   2   3   4   5                              │
│ ↑                                              │
│ S,F (both start here)                          │
│                                                │
│ 1   2   3   4   5                              │
│     ↑       ↑                                  │
│     S       F                                  │
│                                                │
│ 1   2   3   4   5   NULL                       │
│         ↑           ↑                          │
│         S           F (reached end)            │
│                                                │
│ Middle = 3 ✓                                  │
└────────────────────────────────────────────────┘
```

### C Code

```c
struct Node* findMiddle(struct Node* head) {
    struct Node* slow = head;
    struct Node* fast = head;

    while (fast != NULL && fast->next != NULL) {
        slow = slow->next;
        fast = fast->next->next;
    }
    return slow;  // Middle node
}
```

---

## Question 34: Merge Two Sorted Linked Lists

### Visualization

```
L1: 1 → 3 → 5
L2: 2 → 4 → 6

Compare heads, pick smaller:
┌────────────────────────────────────────────────┐
│ 1 < 2 → take 1    Result: 1                   │
│ 3 > 2 → take 2    Result: 1→2                 │
│ 3 < 4 → take 3    Result: 1→2→3               │
│ 5 > 4 → take 4    Result: 1→2→3→4             │
│ 5 < 6 → take 5    Result: 1→2→3→4→5           │
│ take 6            Result: 1→2→3→4→5→6         │
└────────────────────────────────────────────────┘
```

### C Code

```c
struct Node* mergeLists(struct Node* l1, struct Node* l2) {
    struct Node dummy = {0, NULL};
    struct Node* tail = &dummy;

    while (l1 && l2) {
        if (l1->data <= l2->data) {
            tail->next = l1;
            l1 = l1->next;
        } else {
            tail->next = l2;
            l2 = l2->next;
        }
        tail = tail->next;
    }

    tail->next = l1 ? l1 : l2;  // Append remaining
    return dummy.next;
}
```

---

## Question 35: Remove N-th Node from End

### Visualization

```
Remove 2nd from end: 1 → 2 → 3 → 4 → 5

Two pointer technique:
┌────────────────────────────────────────────────┐
│ Move fast n=2 steps ahead first:               │
│                                                │
│ 1 → 2 → 3 → 4 → 5                             │
│ ↑       ↑                                      │
│ slow   fast                                    │
│                                                │
│ Then move both until fast reaches end:         │
│                                                │
│ 1 → 2 → 3 → 4 → 5 → NULL                      │
│         ↑           ↑                          │
│        slow        fast                        │
│                                                │
│ slow.next is the node to remove (4)           │
│ Result: 1 → 2 → 3 → 5                         │
└────────────────────────────────────────────────┘
```

---

## Question 36: Check if Linked List is Palindrome

### Visualization

```
List: 1 → 2 → 2 → 1

Steps:
1. Find middle: 1 → 2 | 2 → 1
2. Reverse second half: 1 → 2 | 1 → 2
3. Compare both halves
   1==1 ✓, 2==2 ✓ → PALINDROME!
```

---

## Questions 37-45 Quick Reference

| #   | Problem                            | Key Technique                |
| --- | ---------------------------------- | ---------------------------- |
| 37  | Add two numbers                    | Digit by digit + carry       |
| 38  | Intersection of lists              | Length difference method     |
| 39  | Delete node (given only that node) | Copy next's data             |
| 40  | Remove duplicates (sorted)         | Compare adjacent             |
| 41  | Rotate list by k                   | Find new head                |
| 42  | Clone list with random pointer     | HashMap or interweaving      |
| 43  | Flatten multilevel list            | DFS/recursion                |
| 44  | Sort linked list                   | Merge sort                   |
| 45  | Swap nodes in pairs                | Careful pointer manipulation |
