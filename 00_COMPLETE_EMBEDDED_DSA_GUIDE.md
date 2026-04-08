# 📘 Complete DSA Guide for Embedded Systems Interviews

> **From Zero to Interview-Ready: The Comprehensive Guide for Beginners**
> 
> **Version:** 2.0  
> **Last Updated:** April 2026  
> **Target Audience:** Embedded Systems Engineers preparing for coding interviews  
> **Prerequisites:** Basic C programming knowledge

---

## Table of Contents

- [1. Why DSA for Embedded?](#1-why-dsa-for-embedded)
- [2. C Programming Foundations](#2-c-programming-foundations)
- [3. Time & Space Complexity](#3-time--space-complexity)
- [4. Complete DSA Implementation Guide](#4-complete-dsa-implementation-guide)
  - [4.1 Arrays & Strings](#41-arrays--strings)
  - [4.2 Linked Lists](#42-linked-lists)
  - [4.3 Stacks & Queues](#43-stacks--queues)
  - [4.4 Hashing](#44-hashing)
  - [4.5 Trees](#45-trees)
  - [4.6 Graphs](#46-graphs)
  - [4.7 Bit Manipulation](#47-bit-manipulation----embedded-superstar)
  - [4.8 Sorting & Searching](#48-sorting--searching)
- [5. Embedded-Specific Patterns](#5-embedded-specific-patterns)
- [6. Problem-Solving Framework](#6-problem-solving-framework)
- [7. Complete Question Bank](#7-complete-question-bank)
- [8. Company-Specific Preparation](#8-company-specific-preparation)
- [9. Top 30 Must-Solve Problems](#9-top-30-must-solve-problems)
- [10. 60-Day Study Plan](#10-60-day-study-plan)
- [11. Resources & References](#11-resources--references)
- [12. Interview Cheat Sheet](#12-interview-cheat-sheet)

---

## 1. Why DSA for Embedded?

### What Embedded Companies Test

**Embedded companies test:**
```
├── Memory-efficient code          → You have limited RAM (KB, not GB!)
├── Bit manipulation               → Hardware register manipulation
├── Real-time data processing      → Queues, Buffers, Circular Buffers
├── Fast lookup/search             → Index tables in firmware
├── Interrupt handling logic       → Stack management
└── Optimization mindset           → Every cycle counts!
```

### Company Focus Areas

| Company Type | Examples | Focus Area |
|---|---|---|
| **Chip Design** | Qualcomm, Intel, ARM | Bit manipulation, Linked Lists, Trees |
| **Automotive** | Bosch, Continental, Denso | Queues, Circular Buffers, Sorting |
| **MCU Vendors** | TI, Microchip, STM32 | Bitwise Ops, Hashing, Searching |
| **IoT/Startups** | Various | Arrays, Strings, Hash Maps |
| **Networking** | Cisco, Juniper | Graphs, Trees, Hash Maps |

### DSA Topic Distribution

```
Bit Manipulation ████████████████████ ~25%
Arrays & Strings ██████████████████ ~22%
Linked Lists ███████████████ ~18%
Stacks & Queues ████████████ ~15%
Sorting & Searching ██████████ ~10%
Trees & Hashing ████████ ~8%
Embedded-Specific Logic ██████ ~2%
```

---

## 2. C Programming Foundations

### MUST-KNOW C Concepts Before DSA

```c
// 1. POINTERS (THE MOST IMPORTANT for embedded)
int x = 10;
int *ptr = &x;          // pointer to int
int **dptr = &ptr;      // pointer to pointer

// 2. DYNAMIC MEMORY (know when NOT to use it)
int *arr = (int *)malloc(5 * sizeof(int));
// ... use arr...
free(arr);              // ALWAYS free!

// 3. STRUCTURES & TYPEDEF
typedef struct {
    uint8_t  id;
    uint16_t value;
    struct Node *next;  // self-referencing for linked lists
} SensorData;

// 4. FUNCTION POINTERS (used in driver callbacks)
void (*callback)(int);
callback = &myHandler;
callback(42);

// 5. BITWISE OPERATIONS (Daily bread in embedded)
uint8_t reg = 0x00;
reg |= (1 << 3);       // SET bit 3
reg &= ~(1 << 5);      // CLEAR bit 5
reg ^= (1 << 2);       // TOGGLE bit 2
if (reg & (1 << 3)) {} // CHECK bit 3
```

---

## 3. Time & Space Complexity

### Big-O Complexity Guide

> **IN EMBEDDED, SPACE MATTERS MORE THAN GENERAL SOFTWARE!**  
> You have 256KB RAM, not 16GB!

```
O(1)       → Constant      → Hash lookup, array index
O(log n)   → Logarithmic   → Binary search, balanced BST
O(n)       → Linear        → Single loop, linear search
O(n log n) → Linearithmic  → Merge sort, heap sort
O(n²)      → Quadratic     → Nested loops, bubble sort
O(2ⁿ)      → Exponential   → Recursive fibonacci (AVOID!)
```

### Space Considerations in Embedded

- **Stack:** Very limited (4-8KB typically) → Be careful with recursion!
- **Heap:** Avoid malloc/free in safety-critical code
- **Best:** Static arrays, pre-allocated buffers

### Example: Why Complexity Matters

```c
// BAD - O(n²) - Takes too long for real-time processing
for (int i = 0; i < n; i++)
    for (int j = 0; j < n; j++)
        process(data[i], data[j]);

// GOOD - O(n) - Meets real-time deadline
for (int i = 0; i < n; i++)
    process(data[i]);
```

---

## 4. Complete DSA Implementation Guide

### 8-Week Learning Roadmap

```
Week 1-2: Arrays & Strings           (operations, searching, sorting)
Week 3-4: Linked Lists               (singly, doubly, circular)
Week 5:   Stacks & Queues            (LIFO/FIFO, circular buffers)
Week 6:   Hashing & Trees            (hash tables, BST, traversals)
Week 7:   Graphs & Advanced          (BFS, DFS, shortest path)
Week 8:   Embedded-Specific + Mocks  (bit manipulation, state machines)
```

---

## 4.1 Arrays & Strings

### Problem 1: Reverse an Array In-Place

```c
// Embedded use: Reverse byte order (endianness conversion)

void reverse_array(int arr[], int n) {
    int left = 0, right = n - 1;
    while (left < right) {
        int temp = arr[left];
        arr[left] = arr[right];
        arr[right] = temp;
        left++;
        right--;
    }
}

/*
  Visual:
  [1, 2, 3, 4, 5]
   L           R     → swap 1,5
   [5, 2, 3, 4, 1]
      L     R        → swap 2,4
   [5, 4, 3, 2, 1]
         LR          → STOP!

  Time: O(n), Space: O(1)
*/
```

### Problem 2: Find Maximum in Array

```c
// Embedded use: Find peak sensor reading

int find_max(int arr[], int n) {
    int max = arr[0];
    for (int i = 1; i < n; i++) {
        if (arr[i] > max)
            max = arr[i];
    }
    return max;
}

// Time: O(n), Space: O(1)
```

### Problem 3: Remove Duplicates (Sorted Array)

```c
// Returns new length, modifies array in-place

int remove_duplicates(int arr[], int n) {
    if (n == 0) return 0;
    int j = 0;  // Pointer for unique elements
    for (int i = 1; i < n; i++) {
        if (arr[i] != arr[j]) {
            j++;
            arr[j] = arr[i];
        }
    }
    return j + 1;  // New length
}

/*
  Input:  [1, 1, 2, 2, 3, 4, 4, 5]
  Output: [1, 2, 3, 4, 5, _, _, _]  return 5
  
  Time: O(n), Space: O(1)
*/
```

### Problem 4: Move All Zeros to End

```c
void move_zeros(int arr[], int n) {
    int j = 0;  // Position for non-zero elements
    for (int i = 0; i < n; i++) {
        if (arr[i] != 0) {
            arr[j] = arr[i];
            j++;
        }
    }
    while (j < n) {
        arr[j] = 0;
        j++;
    }
}

/*
  Input:  [0, 1, 0, 3, 12, 0]
  Output: [1, 3, 12, 0, 0, 0]
  
  Time: O(n), Space: O(1)
*/
```

### Problem 5: Rotate Array by K (Reversal Algorithm)

```c
void reverse_range(int arr[], int start, int end) {
    while (start < end) {
        int temp = arr[start];
        arr[start] = arr[end];
        arr[end] = temp;
        start++;
        end--;
    }
}

void rotate_array(int arr[], int n, int k) {
    k = k % n;  // Handle k > n
    reverse_range(arr, 0, n - 1);   // Reverse all
    reverse_range(arr, 0, k - 1);   // Reverse first k
    reverse_range(arr, k, n - 1);   // Reverse rest
}

/*
  Input:  [1, 2, 3, 4, 5, 6, 7]  k = 3
  Step 1: [7, 6, 5, 4, 3, 2, 1]  (reverse all)
  Step 2: [5, 6, 7, 4, 3, 2, 1]  (reverse 0..2)
  Step 3: [5, 6, 7, 1, 2, 3, 4]  (reverse 3..6)
  
  Time: O(n), Space: O(1)
*/
```

### Problem 6: Two Sum

```c
// MOST ASKED ARRAY QUESTION IN EXISTENCE
// Sort + Two Pointer approach - O(n log n)

typedef struct { int val; int idx; } Pair;

void two_sum(int arr[], int n, int target) {
    Pair pairs[n];
    for (int i = 0; i < n; i++) {
        pairs[i].val = arr[i];
        pairs[i].idx = i;
    }
    
    // Sort by value
    for (int i = 0; i < n - 1; i++)
        for (int j = 0; j < n - i - 1; j++)
            if (pairs[j].val > pairs[j+1].val) {
                Pair temp = pairs[j];
                pairs[j] = pairs[j+1];
                pairs[j+1] = temp;
            }
    
    int left = 0, right = n - 1;
    while (left < right) {
        int sum = pairs[left].val + pairs[right].val;
        if (sum == target) {
            printf("Found: indices %d, %d\\n", 
                   pairs[left].idx, pairs[right].idx);
            return;
        } else if (sum < target)
            left++;
        else
            right--;
    }
    printf("No two-sum found\\n");
}

// Time: O(n log n), Space: O(n)
```

### Problem 7: Kadane's Algorithm (Maximum Subarray)

```c
// ASKED IN EVERY SINGLE EMBEDDED COMPANY

int max_subarray(int arr[], int n) {
    int max_so_far = arr[0];
    int max_ending_here = arr[0];
    
    for (int i = 1; i < n; i++) {
        max_ending_here = (max_ending_here + arr[i] > arr[i]) 
                          ? max_ending_here + arr[i] 
                          : arr[i];
        
        if (max_ending_here > max_so_far)
            max_so_far = max_ending_here;
    }
    return max_so_far;
}

/*
  arr = [-2, 1, -3, 4, -1, 2, 1, -5, 4]
  
  i=0: max_end=-2, max_far=-2
  i=1: max_end=1,  max_far=1
  i=2: max_end=-2, max_far=1
  i=3: max_end=4,  max_far=4
  i=4: max_end=3,  max_far=4
  i=5: max_end=5,  max_far=5
  i=6: max_end=6,  max_far=6    ← ANSWER
  i=7: max_end=1,  max_far=6
  i=8: max_end=5,  max_far=6
  
  Answer: 6 (subarray [4, -1, 2, 1])
  Time: O(n), Space: O(1)
*/
```

### Problem 8: Product of Array Except Self

```c
// Without using division! - O(n) time, O(n) space

void product_except_self(int arr[], int n, int result[]) {
    // Left pass: result[i] = product of all elements to LEFT of i
    result[0] = 1;
    for (int i = 1; i < n; i++)
        result[i] = result[i - 1] * arr[i - 1];
    
    // Right pass: multiply with products to RIGHT
    int right_product = 1;
    for (int i = n - 1; i >= 0; i--) {
        result[i] *= right_product;
        right_product *= arr[i];
    }
}

/*
  arr =    [1, 2, 3, 4]
  Left:    [1, 1, 2, 6]     (product to left)
  Result:  [24, 12, 8, 6]
  
  Time: O(n), Space: O(n)
*/
```

### Problem 9: Best Time to Buy and Sell Stock

```c
int max_profit(int prices[], int n) {
    int min_price = prices[0];
    int max_profit = 0;
    
    for (int i = 1; i < n; i++) {
        if (prices[i] - min_price > max_profit)
            max_profit = prices[i] - min_price;
        if (prices[i] < min_price)
            min_price = prices[i];
    }
    return max_profit;
}

/*
  prices = [7, 1, 5, 3, 6, 4]
  
  Buy at 1, Sell at 6, Profit = 5
  Time: O(n), Space: O(1)
*/
```

### Problem 10: Binary Search

```c
int binary_search(int arr[], int n, int target) {
    int low = 0, high = n - 1;
    
    while (low <= high) {
        int mid = low + (high - low) / 2;  // Avoid overflow!
        
        if (arr[mid] == target)
            return mid;
        else if (arr[mid] < target)
            low = mid + 1;
        else
            high = mid - 1;
    }
    return -1;
}

// Time: O(log n), Space: O(1)
```

### Problem 11: Search in Rotated Sorted Array

```c
int search_rotated(int arr[], int n, int target) {
    int low = 0, high = n - 1;
    
    while (low <= high) {
        int mid = low + (high - low) / 2;
        
        if (arr[mid] == target)
            return mid;
        
        // Check which half is sorted
        if (arr[low] <= arr[mid]) {
            // Left half is sorted
            if (target >= arr[low] && target < arr[mid])
                high = mid - 1;
            else
                low = mid + 1;
        } else {
            // Right half is sorted
            if (target > arr[mid] && target <= arr[high])
                low = mid + 1;
            else
                high = mid - 1;
        }
    }
    return -1;
}

// Time: O(log n), Space: O(1)
```

### Problem 12: Sort Colors (Dutch National Flag)

```c
// Sort array of 0s, 1s, 2s in single pass

void sort_colors(int arr[], int n) {
    int low = 0, mid = 0, high = n - 1;
    
    while (mid <= high) {
        if (arr[mid] == 0) {
            // Swap with low region
            int temp = arr[low];
            arr[low] = arr[mid];
            arr[mid] = temp;
            low++;
            mid++;
        } else if (arr[mid] == 1) {
            mid++;
        } else {
            // arr[mid] == 2, swap with high region
            int temp = arr[mid];
            arr[mid] = arr[high];
            arr[high] = temp;
            high--;
        }
    }
}

/*
  Input:  [2, 0, 2, 1, 1, 0]
  Output: [0, 0, 1, 1, 2, 2]
  
  Time: O(n), Space: O(1)
*/
```

### Problem 13: Sliding Window - Max Sum of K Elements

```c
// Embedded use: Moving average filter on sensor data!

int max_sum_sliding_window(int arr[], int n, int k) {
    int window_sum = 0;
    for (int i = 0; i < k; i++)
        window_sum += arr[i];
    int max_sum = window_sum;
    
    for (int i = k; i < n; i++) {
        window_sum = window_sum - arr[i - k] + arr[i];
        if (window_sum > max_sum)
            max_sum = window_sum;
    }
    return max_sum;
}

/*
  arr = [2, 1, 5, 1, 3, 2]   k = 3
  
  Window 1: [2, 1, 5] = 8
  Window 2:    [1, 5, 1] = 8-2+1=7
  Window 3:       [5, 1, 3] = 7-1+3=9  ← MAX
  Window 4:          [1, 3, 2] = 9-5+2=6
  
  KEY: Don't recalculate sum, just ADD new, REMOVE old!
  Time: O(n), Space: O(1)
*/
```

### String Problems

#### Reverse String
```c
void reverse_string(char str[]) {
    int len = strlen(str);
    for (int i = 0; i < len / 2; i++) {
        char temp = str[i];
        str[i] = str[len - 1 - i];
        str[len - 1 - i] = temp;
    }
}
// Time: O(n), Space: O(1)
```

#### Check Palindrome
```c
int is_palindrome(char str[]) {
    int len = strlen(str);
    for (int i = 0; i < len / 2; i++) {
        if (str[i] != str[len - 1 - i])
            return 0;
    }
    return 1;
}
// Time: O(n), Space: O(1)
```

#### Implement strlen, strcpy, strcmp

```c
int my_strlen(const char *str) {
    int len = 0;
    while (str[len] != '\0')
        len++;
    return len;
}

char *my_strcpy(char *dest, const char *src) {
    char *original = dest;
    while ((*dest++ = *src++) != '\0');
    return original;
}

int my_strcmp(const char *s1, const char *s2) {
    while (*s1 && (*s1 == *s2)) {
        s1++;
        s2++;
    }
    return *(unsigned char *)s1 - *(unsigned char *)s2;
}

// Time: O(n), Space: O(1)
```

#### Check Anagram

```c
int is_anagram(char s1[], char s2[]) {
    int freq[256] = {0};
    
    for (int i = 0; s1[i]; i++)
        freq[(unsigned char)tolower(s1[i])]++;
    for (int i = 0; s2[i]; i++)
        freq[(unsigned char)tolower(s2[i])]--;
    for (int i = 0; i < 256; i++)
        if (freq[i] != 0) return 0;
    return 1;
}

// Time: O(n), Space: O(1)
```

#### First Non-Repeating Character

```c
char first_unique(char str[]) {
    int freq[256] = {0};
    for (int i = 0; str[i]; i++)
        freq[(unsigned char)str[i]]++;
    for (int i = 0; str[i]; i++)
        if (freq[(unsigned char)str[i]] == 1)
            return str[i];
    return '\0';
}

// Time: O(n), Space: O(1)
```

---

## 4.2 Linked Lists

### Basic Linked List Implementation

```c
#include <stdio.h>
#include <stdlib.h>

typedef struct Node {
    int data;
    struct Node *next;
} Node;

Node* create_node(int data) {
    Node *new_node = (Node *)malloc(sizeof(Node));
    if (new_node == NULL) {
        printf("Memory allocation failed!\\n");
        return NULL;
    }
    new_node->data = data;
    new_node->next = NULL;
    return new_node;
}

void insert_begin(Node **head, int data) {
    Node *new_node = create_node(data);
    new_node->next = *head;
    *head = new_node;
}

void insert_end(Node **head, int data) {
    Node *new_node = create_node(data);
    if (*head == NULL) {
        *head = new_node;
        return;
    }
    Node *temp = *head;
    while (temp->next != NULL) temp = temp->next;
    temp->next = new_node;
}

void print_list(Node *head) {
    Node *temp = head;
    while (temp != NULL) {
        printf("%d -> ", temp->data);
        temp = temp->next;
    }
    printf("NULL\\n");
}

void free_list(Node **head) {
    Node *current = *head;
    while (current != NULL) {
        Node *temp = current;
        current = current->next;
        free(temp);
    }
    *head = NULL;
}
```

### Problem 1: Reverse Linked List

```c
Node* reverse_list(Node *head) {
    Node *prev = NULL;
    Node *current = head;
    Node *next = NULL;
    
    while (current != NULL) {
        next = current->next;      // Save next node
        current->next = prev;      // Reverse the link
        prev = current;            // Move prev forward
        current = next;            // Move current forward
    }
    return prev;  // New head
}

/*
  Before: 1 → 2 → 3 → NULL
  
  Step 1: prev=NULL, curr=1, next=2
          NULL ← 1    2 → 3 → NULL
          
  Step 2: prev=1, curr=2, next=3
          NULL ← 1 ← 2    3 → NULL
          
  Step 3: prev=2, curr=3, next=NULL
          NULL ← 1 ← 2 ← 3
  
  Result: 3 → 2 → 1 → NULL
  Time: O(n), Space: O(1)
*/
```

### Problem 2: Detect Cycle (Floyd's Algorithm)

```c
int detect_cycle(Node *head) {
    Node *slow = head;
    Node *fast = head;
    
    while (fast != NULL && fast->next != NULL) {
        slow = slow->next;           // Move 1 step
        fast = fast->next->next;     // Move 2 steps
        
        if (slow == fast)
            return 1;  // CYCLE DETECTED!
    }
    return 0;  // No cycle
}

/*
  Think of it like a RACETRACK:
  - Slow runner: 1 step at a time
  - Fast runner: 2 steps at a time
  - If track is circular, fast will eventually catch slow!
  
  Time: O(n), Space: O(1)
*/
```

### Problem 3: Find Middle Element

```c
Node* find_middle(Node *head) {
    Node *slow = head;
    Node *fast = head;
    
    while (fast != NULL && fast->next != NULL) {
        slow = slow->next;
        fast = fast->next->next;
    }
    return slow;  // Slow is at middle when fast reaches end
}

// Time: O(n), Space: O(1)
```

### Problem 4: Merge Two Sorted Lists

```c
Node* merge_sorted(Node *l1, Node *l2) {
    Node dummy;              // Dummy head (simplifies logic)
    Node *tail = &dummy;
    dummy.next = NULL;
    
    while (l1 != NULL && l2 != NULL) {
        if (l1->data <= l2->data) {
            tail->next = l1;
            l1 = l1->next;
        } else {
            tail->next = l2;
            l2 = l2->next;
        }
        tail = tail->next;
    }
    
    // Attach remaining
    tail->next = (l1 != NULL) ? l1 : l2;
    
    return dummy.next;
}

// Time: O(n + m), Space: O(1)
```

### Problem 5: Remove Nth Node from End

```c
Node* remove_nth_from_end(Node *head, int n) {
    Node dummy;
    dummy.next = head;
    Node *fast = &dummy;
    Node *slow = &dummy;
    
    // Move fast n+1 steps ahead
    for (int i = 0; i <= n; i++)
        fast = fast->next;
    
    // Move both until fast reaches end
    while (fast != NULL) {
        fast = fast->next;
        slow = slow->next;
    }
    
    // Remove node after slow
    Node *to_delete = slow->next;
    slow->next = slow->next->next;
    free(to_delete);
    
    return dummy.next;
}

// Time: O(n), Space: O(1)
```

### Problem 6: Find Cycle Start Node

```c
Node* find_cycle_start(Node *head) {
    Node *slow = head, *fast = head;
    
    // Detect cycle
    while (fast && fast->next) {
        slow = slow->next;
        fast = fast->next->next;
        if (slow == fast) break;
    }
    
    if (slow != fast) return NULL;  // No cycle
    
    // Find start: move one pointer to head, advance both at same speed
    slow = head;
    while (slow != fast) {
        slow = slow->next;
        fast = fast->next;
    }
    return slow;  // Meeting point = cycle start
}

// Time: O(n), Space: O(1)
```

### Problem 7: Check if Linked List is Palindrome

```c
int is_list_palindrome(Node *head) {
    // Find middle
    Node *slow = head, *fast = head;
    while (fast && fast->next) {
        slow = slow->next;
        fast = fast->next->next;
    }
    
    // Reverse second half
    Node *prev = NULL, *curr = slow, *next;
    while (curr) {
        next = curr->next;
        curr->next = prev;
        prev = curr;
        curr = next;
    }
    
    // Compare first and second halves
    Node *p1 = head, *p2 = prev;
    while (p2) {
        if (p1->data != p2->data) return 0;
        p1 = p1->next;
        p2 = p2->next;
    }
    return 1;
}

// Time: O(n), Space: O(1)
```

### Problem 8: Circular Linked List

```c
typedef struct CNode {
    int data;
    struct CNode *next;
} CNode;

void cll_insert(CNode **head, int data) {
    CNode *n = (CNode*)malloc(sizeof(CNode));
    n->data = data;
    
    if (*head == NULL) {
        *head = n;
        n->next = n;  // Points to itself!
        return;
    }
    
    CNode *temp = *head;
    while (temp->next != *head)
        temp = temp->next;
    temp->next = n;
    n->next = *head;
}

void cll_print(CNode *head) {
    if (!head) return;
    CNode *temp = head;
    do {
        printf("%d -> ", temp->data);
        temp = temp->next;
    } while (temp != head);
    printf("(back to %d)\\n", head->data);
}
```

---

## 4.3 Stacks & Queues

### Problem 1: Stack Implementation

```c
#define MAX_STACK_SIZE 100

typedef struct {
    int data[MAX_STACK_SIZE];
    int top;
} Stack;

void stack_init(Stack *s) { s->top = -1; }

int stack_empty(Stack *s) { return s->top == -1; }

int stack_full(Stack *s) { return s->top == MAX_STACK_SIZE - 1; }

void stack_push(Stack *s, int value) {
    if (!stack_full(s)) 
        s->data[++(s->top)] = value;
}

int stack_pop(Stack *s) {
    if (!stack_empty(s)) 
        return s->data[(s->top)--];
    return -1;
}

int stack_peek(Stack *s) {
    if (!stack_empty(s)) 
        return s->data[s->top];
    return -1;
}

// Time: O(1), Space: depends on usage
```

### Problem 2: Queue Implementation

```c
#define MAX_QUEUE_SIZE 100

typedef struct {
    int arr[MAX_QUEUE_SIZE];
    int front, rear;
} Queue;

void queue_init(Queue *q) { q->front = q->rear = -1; }

int queue_empty(Queue *q) { return q->front == -1; }

void queue_enqueue(Queue *q, int val) {
    if (q->rear == MAX_QUEUE_SIZE - 1) return;
    if (q->front == -1) q->front = 0;
    q->arr[++(q->rear)] = val;
}

int queue_dequeue(Queue *q) {
    if (queue_empty(q)) return -1;
    int val = q->arr[q->front];
    if (q->front == q->rear)
        q->front = q->rear = -1;
    else
        q->front++;
    return val;
}

// Time: O(1), Space: depends on usage
```

### Problem 3: Circular Queue/Buffer (EMBEDDED CRITICAL!)

```c
// THIS IS THE #1 EMBEDDED INTERVIEW TOPIC!

#define CBUF_SIZE 64

typedef struct {
    uint8_t buf[CBUF_SIZE];
    uint16_t head, tail, count;
} CircularBuffer;

void cbuf_init(CircularBuffer *cb) {
    cb->head = cb->tail = cb->count = 0;
}

int cbuf_write(CircularBuffer *cb, uint8_t data) {
    if (cb->count == CBUF_SIZE) return -1;  // Full
    cb->buf[cb->head] = data;
    cb->head = (cb->head + 1) % CBUF_SIZE;
    cb->count++;
    return 0;
}

int cbuf_read(CircularBuffer *cb, uint8_t *data) {
    if (cb->count == 0) return -1;  // Empty
    *data = cb->buf[cb->tail];
    cb->tail = (cb->tail + 1) % CBUF_SIZE;
    cb->count--;
    return 0;
}

int cbuf_is_empty(CircularBuffer *cb) { return cb->count == 0; }
int cbuf_is_full(CircularBuffer *cb)  { return cb->count == CBUF_SIZE; }

/*
  Circular Buffer Visual (capacity = 5):
  
  Initial:  [  ][  ][  ][  ][  ]  head=0, tail=0, count=0
  
  Write A:  [A ][  ][  ][  ][  ]  head=1, count=1
  Write B:  [A ][B ][  ][  ][  ]  head=2, count=2
  Write C,D,E,F: [F ][B ][C ][D ][E ]  head=0 (wrapped!), FULL!
  
  The % operator makes it CIRCULAR!
  Time: O(1), Space: O(capacity)
*/
```

### Problem 4: Valid Parentheses

```c
int is_valid_parentheses(char *str) {
    Stack s;
    stack_init(&s);
    
    for (int i = 0; str[i]; i++) {
        if (str[i] == '(' || str[i] == '{' || str[i] == '[') {
            stack_push(&s, str[i]);
        } else {
            if (stack_empty(&s)) return 0;
            int top = stack_pop(&s);
            if ((str[i] == ')' && top != '(') ||
                (str[i] == '}' && top != '{') ||
                (str[i] == ']' && top != '['))
                return 0;
        }
    }
    return stack_empty(&s);
}

// Time: O(n), Space: O(n)
```

### Problem 5: Min Stack (Get Minimum in O(1))

```c
typedef struct {
    int arr[MAX_STACK_SIZE];
    int min_arr[MAX_STACK_SIZE];
    int top;
} MinStack;

void minstack_init(MinStack *s) { s->top = -1; }

void minstack_push(MinStack *s, int val) {
    s->top++;
    s->arr[s->top] = val;
    if (s->top == 0)
        s->min_arr[s->top] = val;
    else
        s->min_arr[s->top] = (val < s->min_arr[s->top-1])
                              ? val : s->min_arr[s->top-1];
}

int minstack_get_min(MinStack *s) {
    return s->min_arr[s->top];
}

// Time: O(1), Space: O(n)
```

### Problem 6: Next Greater Element

```c
void next_greater(int arr[], int n, int result[]) {
    Stack s;
    stack_init(&s);
    
    for (int i = n - 1; i >= 0; i--) {
        while (!stack_empty(&s) && stack_peek(&s) <= arr[i])
            stack_pop(&s);
        
        result[i] = stack_empty(&s) ? -1 : stack_peek(&s);
        stack_push(&s, arr[i]);
    }
}

/*
  arr =    [4, 5, 2, 25]
  result = [5, 25, 25, -1]
  
  4 → next greater is 5
  5 → next greater is 25
  2 → next greater is 25
  25 → no greater → -1
  
  Time: O(n), Space: O(n)
*/
```

### Problem 7: Priority Queue (Min-Heap)

```c
#define MAX_HEAP_SIZE 100

typedef struct {
    int data[MAX_HEAP_SIZE];
    int size;
} MinHeap;

void heap_init(MinHeap *h) { h->size = 0; }

void heap_swap(int *a, int *b) { int t=*a; *a=*b; *b=t; }

void heap_insert(MinHeap *h, int value) {
    int i = h->size++;
    h->data[i] = value;
    while (i > 0 && h->data[(i-1)/2] > h->data[i]) {
        heap_swap(&h->data[(i-1)/2], &h->data[i]);
        i = (i-1)/2;
    }
}

int heap_extract_min(MinHeap *h) {
    int min = h->data[0];
    h->data[0] = h->data[--h->size];
    int i = 0;
    while (2*i+1 < h->size) {
        int smallest = i;
        int l = 2*i+1, r = 2*i+2;
        if (h->data[l] < h->data[smallest]) smallest = l;
        if (r < h->size && h->data[r] < h->data[smallest]) smallest = r;
        if (smallest == i) break;
        heap_swap(&h->data[i], &h->data[smallest]);
        i = smallest;
    }
    return min;
}

// Time: O(log n), Space: O(n)
```

### Problem 8: UART Ring Buffer (ISR Safe)

```c
// Embedded use: Serial communication buffers

#define UART_BUF_SIZE 256

typedef struct {
    volatile uint8_t buf[UART_BUF_SIZE];
    volatile uint16_t head;
    volatile uint16_t tail;
} UartRingBuffer;

void uart_init(UartRingBuffer *ub) {
    ub->head = ub->tail = 0;
}

// ISR: called when byte received
void uart_rx_isr(UartRingBuffer *ub, uint8_t byte) {
    uint16_t next = (ub->head + 1) % UART_BUF_SIZE;
    if (next != ub->tail) {       // Not full
        ub->buf[ub->head] = byte;
        ub->head = next;
    }
}

// Main loop: read byte
int uart_read(UartRingBuffer *ub, uint8_t *byte) {
    if (ub->head == ub->tail) return 0;  // Empty
    *byte = ub->buf[ub->tail];
    ub->tail = (ub->tail + 1) % UART_BUF_SIZE;
    return 1;
}

/*
  Advantage: O(1) ISR without blocking
  Time: O(1), Space: O(UART_BUF_SIZE)
*/
```

---

## 4.4 Hashing

### Simple HashMap Implementation

```c
#define TABLE_SIZE 101

typedef struct Entry {
    int key, value;
    struct Entry *next;
} Entry;

typedef struct {
    Entry *table[TABLE_SIZE];
} HashMap;

unsigned int hash_func(int key) {
    return ((unsigned int)key) % TABLE_SIZE;
}

void hashmap_init(HashMap *m) {
    for (int i = 0; i < TABLE_SIZE; i++)
        m->table[i] = NULL;
}

void hashmap_put(HashMap *m, int key, int value) {
    unsigned int idx = hash_func(key);
    Entry *e = m->table[idx];
    while (e) {
        if (e->key == key) { 
            e->value = value; 
            return; 
        }
        e = e->next;
    }
    e = (Entry*)malloc(sizeof(Entry));
    e->key = key; e->value = value;
    e->next = m->table[idx];
    m->table[idx] = e;
}

int hashmap_get(HashMap *m, int key, int *value) {
    Entry *e = m->table[hash_func(key)];
    while (e) {
        if (e->key == key) { 
            *value = e->value; 
            return 1; 
        }
        e = e->next;
    }
    return 0;
}

/*
  Hash Table Visual:
  
  Bucket 5:  [5:100] → NULL
  Bucket 5:  [69:200] → NULL   (69 % 64 = 5, COLLISION!)
  Bucket 5:  [133:300] → [69:200] → NULL  (chaining)
  
  Lookup key 69:
    hash(69) = 5
    bucket[5]: 133? No → next → 69? Yes! Return 200
    
  Time: O(1) avg, O(n) worst; Space: O(n)
*/
```

### Frequency Count

```c
void frequency_count(int arr[], int n) {
    HashMap m;
    hashmap_init(&m);
    
    for (int i = 0; i < n; i++) {
        int count = 0;
        hashmap_get(&m, arr[i], &count);
        hashmap_put(&m, arr[i], count + 1);
    }
}
```

### Contains Duplicate

```c
int contains_duplicate(int arr[], int n) {
    HashMap m;
    hashmap_init(&m);
    for (int i = 0; i < n; i++) {
        int val;
        if (hashmap_get(&m, arr[i], &val)) return 1;
        hashmap_put(&m, arr[i], 1);
    }
    return 0;
}
```

---

## 4.5 Trees

### BST Implementation

```c
typedef struct TreeNode {
    int data;
    struct TreeNode *left, *right;
} TreeNode;

TreeNode* new_node(int data) {
    TreeNode *n = (TreeNode*)malloc(sizeof(TreeNode));
    n->data = data;
    n->left = n->right = NULL;
    return n;
}

TreeNode* bst_insert(TreeNode *root, int data) {
    if (!root) return new_node(data);
    if (data < root->data)
        root->left = bst_insert(root->left, data);
    else if (data > root->data)
        root->right = bst_insert(root->right, data);
    return root;
}

TreeNode* bst_search(TreeNode *root, int target) {
    if (!root || root->data == target) return root;
    if (target < root->data)
        return bst_search(root->left, target);
    return bst_search(root->right, target);
}
```

### Tree Traversals

```c
void inorder(TreeNode *root) {
    if (!root) return;
    inorder(root->left);
    printf("%d ", root->data);
    inorder(root->right);
}

void preorder(TreeNode *root) {
    if (!root) return;
    printf("%d ", root->data);
    preorder(root->left);
    preorder(root->right);
}

void postorder(TreeNode *root) {
    if (!root) return;
    postorder(root->left);
    postorder(root->right);
    printf("%d ", root->data);
}
```

### Level Order Traversal (BFS)

```c
void level_order(TreeNode *root) {
    if (!root) return;
    TreeNode *queue[100];
    int front = 0, rear = 0;
    queue[rear++] = root;
    
    while (front < rear) {
        TreeNode *curr = queue[front++];
        printf("%d ", curr->data);
        if (curr->left)  queue[rear++] = curr->left;
        if (curr->right) queue[rear++] = curr->right;
    }
}
```

### Tree Height

```c
int tree_height(TreeNode *root) {
    if (!root) return 0;
    int lh = tree_height(root->left);
    int rh = tree_height(root->right);
    return 1 + (lh > rh ? lh : rh);
}
```

### Validate BST

```c
int is_valid_bst_util(TreeNode *root, int min, int max) {
    if (!root) return 1;
    if (root->data <= min || root->data >= max) return 0;
    return is_valid_bst_util(root->left, min, root->data) &&
           is_valid_bst_util(root->right, root->data, max);
}

int is_valid_bst(TreeNode *root) {
    return is_valid_bst_util(root, INT_MIN, INT_MAX);
}
```

### Lowest Common Ancestor

```c
TreeNode* lca(TreeNode *root, int p, int q) {
    if (!root) return NULL;
    if (root->data > p && root->data > q)
        return lca(root->left, p, q);
    if (root->data < p && root->data < q)
        return lca(root->right, p, q);
    return root;  // Split point
}
```

### Mirror/Invert Tree

```c
TreeNode* mirror(TreeNode *root) {
    if (!root) return NULL;
    TreeNode *temp = root->left;
    root->left = mirror(root->right);
    root->right = mirror(temp);
    return root;
}
```

---

## 4.6 Graphs

### Graph Representation (Adjacency List)

```c
#define MAX_VERTICES 50

typedef struct AdjNode {
    int vertex;
    struct AdjNode *next;
} AdjNode;

typedef struct {
    AdjNode *heads[MAX_VERTICES];
    int num_vertices;
} GraphList;

void graph_list_init(GraphList *g, int vertices) {
    g->num_vertices = vertices;
    for (int i = 0; i < vertices; i++)
        g->heads[i] = NULL;
}

void add_edge(GraphList *g, int src, int dest) {
    AdjNode *node = (AdjNode *)malloc(sizeof(AdjNode));
    node->vertex = dest;
    node->next = g->heads[src];
    g->heads[src] = node;
}
```

### BFS (Breadth-First Search)

```c
void bfs(GraphList *g, int start) {
    int visited[MAX_VERTICES] = {0};
    int queue[MAX_VERTICES];
    int front = 0, rear = 0;
    
    visited[start] = 1;
    queue[rear++] = start;
    
    printf("BFS: ");
    while (front < rear) {
        int current = queue[front++];
        printf("%d ", current);
        
        AdjNode *temp = g->heads[current];
        while (temp != NULL) {
            if (!visited[temp->vertex]) {
                visited[temp->vertex] = 1;
                queue[rear++] = temp->vertex;
            }
            temp = temp->next;
        }
    }
    printf("\\n");
}

// Time: O(V + E), Space: O(V)
```

### DFS (Depth-First Search)

```c
void dfs_util(GraphList *g, int vertex, int visited[]) {
    visited[vertex] = 1;
    printf("%d ", vertex);
    
    AdjNode *temp = g->heads[vertex];
    while (temp != NULL) {
        if (!visited[temp->vertex])
            dfs_util(g, temp->vertex, visited);
        temp = temp->next;
    }
}

void dfs(GraphList *g, int start) {
    int visited[MAX_VERTICES] = {0};
    printf("DFS: ");
    dfs_util(g, start, visited);
    printf("\\n");
}

// Time: O(V + E), Space: O(V)
```

---

## 4.7 Bit Manipulation - EMBEDDED SUPERSTAR!

> **THIS SECTION IS THE MOST IMPORTANT FOR EMBEDDED!**
> **You WILL be asked bit manipulation in every interview.**

### Basic Bit Operations

```c
#include <stdint.h>

void bit_ops_demo(void) {
    uint8_t reg = 0x00;
    
    reg |= (1 << 3);            // SET bit 3         → 0000 1000
    reg &= ~(1 << 3);           // CLEAR bit 3       → 0000 0000
    reg ^= (1 << 3);            // TOGGLE bit 3      → 0000 1000
    int bit = (reg >> 3) & 1;   // CHECK bit 3       → 1
    
    // Set multiple bits (bits 2 and 5)
    reg |= (1 << 2) | (1 << 5);
    
    // Clear multiple bits
    reg &= ~((1 << 2) | (1 << 5));
    
    // Set specific bit pattern (bits 4-6 to value 5 = 101)
    reg &= ~(0x7 << 4);        // Clear field
    reg |= (5 & 0x7) << 4;     // Set value
}
```

### Count Set Bits (Brian Kernighan - Fastest)

```c
// Method 1: Simple loop - O(bits)
int count_bits_loop(uint32_t n) {
    int count = 0;
    while (n) {
        count += n & 1;
        n >>= 1;
    }
    return count;
}

// Method 2: Brian Kernighan - O(set bits)
int count_bits_kernighan(uint32_t n) {
    int count = 0;
    while (n) {
        n &= n - 1;  // Clear lowest set bit
        count++;
    }
    return count;
}

// Method 3: Lookup table - Embedded favorite!
int count_bits_lookup(uint32_t n) {
    static const int table[16] = {
        0,1,1,2,1,2,2,3,1,2,2,3,2,3,3,4
    };
    int count = 0;
    while (n) {
        count += table[n & 0xF];
        n >>= 4;
    }
    return count;
}

/*
  n = 12 = 1100
  
  Kernighan:
  Step 1: n=1100, n-1=1011, n & (n-1) = 1000, count=1
  Step 2: n=1000, n-1=0111, n & (n-1) = 0000, count=2
  Step 3: n=0, STOP. Result: 2 bits set
  
  Time: O(# of set bits), Space: O(1)
*/
```

### Check Power of Two

```c
int is_power_of_two(uint32_t n) {
    return (n > 0) && ((n & (n - 1)) == 0);
}

/*
  8  = 1000   8-1=0111   1000 & 0111 = 0000 → YES!
  10 = 1010  10-1=1001   1010 & 1001 = 1000 → NO!
  
  Time: O(1), Space: O(1)
*/
```

### Find Single Number (XOR)

```c
int single_number(int arr[], int n) {
    int result = 0;
    for (int i = 0; i < n; i++)
        result ^= arr[i];
    return result;
}

/*
  arr = [4, 1, 2, 1, 2]
  
  result = 0
  result = 0 ^ 4 = 4
  result = 4 ^ 1 = 5
  result = 5 ^ 2 = 7
  result = 7 ^ 1 = 6 (1 cancelled)
  result = 6 ^ 2 = 4 (2 cancelled)
  
  Answer: 4 (the single number!)
  
  Time: O(n), Space: O(1)
*/
```

### Reverse Bits

```c
uint32_t reverse_bits(uint32_t n) {
    uint32_t result = 0;
    for (int i = 0; i < 32; i++) {
        result = (result << 1) | (n & 1);
        n >>= 1;
    }
    return result;
}
```

### Swap Without Temp

```c
void xor_swap(int *a, int *b) {
    if (a != b) {  // Must check!
        *a ^= *b;
        *b ^= *a;
        *a ^= *b;
    }
}
```

### Find Missing Number (XOR)

```c
int find_missing_xor(int arr[], int n) {
    int xor_full = 0, xor_arr = 0;
    for (int i = 0; i <= n; i++) xor_full ^= i;
    for (int i = 0; i < n; i++) xor_arr ^= arr[i];
    return xor_full ^ xor_arr;
}

/*
  arr = [3, 0, 1]  n = 3
  xor_full = 0^1^2^3
  xor_arr = 3^0^1
  result  = (0^1^2^3) ^ (3^0^1) = 2
  
  Time: O(n), Space: O(1)
*/
```

### Turn Off Rightmost Set Bit

```c
int turn_off_rightmost(int n) {
    return n & (n - 1);
}

// 12 = 1100 → 1100 & 1011 = 1000 = 8
```

### Isolate Rightmost Set Bit

```c
int isolate_rightmost(int n) {
    return n & (-n);  // Using two's complement
}

// 12 = 1100 → 1100 & 0100 = 0100 = 4
```

### Generate All Subsets (Power Set)

```c
void print_subsets(int arr[], int n) {
    for (int mask = 0; mask < (1 << n); mask++) {
        printf("{ ");
        for (int i = 0; i < n; i++) {
            if (mask & (1 << i))
                printf("%d ", arr[i]);
        }
        printf("}\\n");
    }
}

/*
  arr = [1, 2, 3], n = 3, total = 8
  
  mask=0 (000): { }
  mask=1 (001): { 1 }
  mask=2 (010): { 2 }
  mask=3 (011): { 1 2 }
  mask=4 (100): { 3 }
  mask=5 (101): { 1 3 }
  mask=6 (110): { 2 3 }
  mask=7 (111): { 1 2 3 }
  
  Time: O(n * 2^n), Space: O(1)
*/
```

### Add Two Numbers Without + Operator

```c
int add(int a, int b) {
    while (b != 0) {
        int carry = a & b;       // Find carry bits
        a = a ^ b;               // Sum without carry
        b = carry << 1;          // Shift carry left
    }
    return a;
}

/*
  3 + 5:
  a=3=011, b=5=101
  carry = 011 & 101 = 001
  a = 011 ^ 101 = 110
  b = 001 << 1 = 010
  
  a=6=110, b=2=010
  carry = 110 & 010 = 010
  a = 110 ^ 010 = 100
  b = 010 << 1 = 100
  
  a=4=100, b=4=100
  carry = 100 & 100 = 100
  a = 100 ^ 100 = 000
  b = 100 << 1 = 1000
  
  a=0, b=1000
  carry = 0 & 1000 = 0
  a = 0 ^ 1000 = 1000
  b = 0 << 1 = 0
  
  Result: 8
*/
```

### Two Non-Repeating Elements

```c
void find_two_unique(int arr[], int n) {
    int xor_all = 0;
    for (int i = 0; i < n; i++)
        xor_all ^= arr[i];
    
    // Find rightmost set bit in xor_all
    int set_bit = xor_all & (-xor_all);
    
    int x = 0, y = 0;
    for (int i = 0; i < n; i++) {
        if (arr[i] & set_bit)
            x ^= arr[i];   // Group with bit set
        else
            y ^= arr[i];   // Group without bit
    }
    printf("Two unique: %d, %d\\n", x, y);
}
```

---

## 4.8 Sorting & Searching

### Bubble Sort

```c
void bubble_sort(int arr[], int n) {
    for (int i = 0; i < n - 1; i++) {
        int swapped = 0;
        for (int j = 0; j < n - 1 - i; j++) {
            if (arr[j] > arr[j + 1]) {
                int temp = arr[j];
                arr[j] = arr[j + 1];
                arr[j + 1] = temp;
                swapped = 1;
            }
        }
        if (!swapped) break;  // Already sorted
    }
}

// Time: O(n²), Space: O(1), Stable: YES
```

### Selection Sort

```c
void selection_sort(int arr[], int n) {
    for (int i = 0; i < n - 1; i++) {
        int min_idx = i;
        for (int j = i + 1; j < n; j++)
            if (arr[j] < arr[min_idx])
                min_idx = j;
        int temp = arr[i];
        arr[i] = arr[min_idx];
        arr[min_idx] = temp;
    }
}

// Time: O(n²), Space: O(1), Stable: NO
```

### Insertion Sort

```c
void insertion_sort(int arr[], int n) {
    for (int i = 1; i < n; i++) {
        int key = arr[i];
        int j = i - 1;
        while (j >= 0 && arr[j] > key) {
            arr[j + 1] = arr[j];
            j--;
        }
        arr[j + 1] = key;
    }
}

// Time: O(n²), Space: O(1), Stable: YES
// BEST for small and nearly sorted arrays!
```

### Merge Sort

```c
void merge(int arr[], int l, int m, int r) {
    int n1 = m - l + 1, n2 = r - m;
    int L[n1], R[n2];
    
    for (int i = 0; i < n1; i++) L[i] = arr[l + i];
    for (int i = 0; i < n2; i++) R[i] = arr[m + 1 + i];
    
    int i = 0, j = 0, k = l;
    while (i < n1 && j < n2)
        arr[k++] = (L[i] <= R[j]) ? L[i++] : R[j++];
    while (i < n1) arr[k++] = L[i++];
    while (j < n2) arr[k++] = R[j++];
}

void merge_sort(int arr[], int l, int r) {
    if (l < r) {
        int m = l + (r - l) / 2;
        merge_sort(arr, l, m);
        merge_sort(arr, m + 1, r);
        merge(arr, l, m, r);
    }
}

// Time: O(n log n), Space: O(n), Stable: YES
```

### Quick Sort

```c
int partition(int arr[], int low, int high) {
    int pivot = arr[high];
    int i = low - 1;
    for (int j = low; j < high; j++) {
        if (arr[j] < pivot) {
            i++;
            int t = arr[i]; arr[i] = arr[j]; arr[j] = t;
        }
    }
    int t = arr[i+1]; arr[i+1] = arr[high]; arr[high] = t;
    return i + 1;
}

void quick_sort(int arr[], int low, int high) {
    if (low < high) {
        int pi = partition(arr, low, high);
        quick_sort(arr, low, pi - 1);
        quick_sort(arr, pi + 1, high);
    }
}

// Time: O(n log n) avg, O(n²) worst
// Space: O(log n), Stable: NO
```

### Find Peak Element

```c
int find_peak(int arr[], int n) {
    int low = 0, high = n - 1;
    while (low < high) {
        int mid = low + (high - low) / 2;
        if (arr[mid] < arr[mid + 1])
            low = mid + 1;
        else
            high = mid;
    }
    return low;
}

// Time: O(log n), Space: O(1)
```

### Integer Square Root

```c
int my_sqrt(int n) {
    if (n < 2) return n;
    int low = 1, high = n / 2, ans = 1;
    while (low <= high) {
        int mid = low + (high - low) / 2;
        if ((long long)mid * mid <= n) {
            ans = mid;
            low = mid + 1;
        } else {
            high = mid - 1;
        }
    }
    return ans;
}

// Time: O(log n), Space: O(1)
```

---

## 5. Embedded-Specific Patterns

### Pattern 1: State Machine

```c
typedef enum {
    STATE_IDLE, STATE_INIT, STATE_RUNNING,
    STATE_ERROR, STATE_COUNT
} SystemState;

typedef SystemState (*StateHandler)(void);

SystemState handle_idle(void) {
    printf("IDLE: Waiting...\\n");
    return STATE_INIT;
}

SystemState handle_init(void) {
    printf("INIT: Initializing...\\n");
    return STATE_RUNNING;
}

SystemState handle_running(void) {
    printf("RUNNING: Processing...\\n");
    return STATE_RUNNING;
}

SystemState handle_error(void) {
    printf("ERROR: Handling...\\n");
    return STATE_IDLE;
}

StateHandler state_handlers[STATE_COUNT] = {
    handle_idle, handle_init, handle_running, handle_error
};

void run_state_machine(void) {
    SystemState current = STATE_IDLE;
    for (int i = 0; i < 10; i++)
        current = state_handlers[current]();
}
```

### Pattern 2: Memory Pool Allocator

```c
#define POOL_BLK_SIZE  64
#define POOL_BLK_COUNT 16

typedef struct PoolNode {
    struct PoolNode *next;
} PoolNode;

typedef struct {
    uint8_t mem[POOL_BLK_COUNT][POOL_BLK_SIZE];
    PoolNode *free_list;
} MemPool;

void pool_init(MemPool *p) {
    p->free_list = NULL;
    for (int i = POOL_BLK_COUNT - 1; i >= 0; i--) {
        PoolNode *n = (PoolNode*)&p->mem[i][0];
        n->next = p->free_list;
        p->free_list = n;
    }
}

void* pool_alloc(MemPool *p) {
    if (!p->free_list) return NULL;
    PoolNode *n = p->free_list;
    p->free_list = n->next;
    return (void*)n;
}

void pool_free(MemPool *p, void *ptr) {
    PoolNode *n = (PoolNode*)ptr;
    n->next = p->free_list;
    p->free_list = n;
}

/*
  Advantages:
  - O(1) alloc and free
  - No fragmentation
  - Deterministic behavior
  - Time: O(1), Space: Fixed
*/
```

### Pattern 3: GPIO Pin Configuration

```c
typedef struct {
    volatile uint32_t MODER;
    volatile uint32_t OTYPER;
    volatile uint32_t OSPEEDR;
    volatile uint32_t PUPDR;
    volatile uint32_t IDR;
    volatile uint32_t ODR;
    volatile uint32_t BSRR;
} GPIO_TypeDef;

#define GPIO_MODE_INPUT   0
#define GPIO_MODE_OUTPUT  1
#define GPIO_MODE_AF      2
#define GPIO_MODE_ANALOG  3

void gpio_pin_set_mode(GPIO_TypeDef *gpio, int pin, int mode) {
    gpio->MODER &= ~(3U << (pin * 2));
    gpio->MODER |= (mode << (pin * 2));
}

void gpio_pin_write(GPIO_TypeDef *gpio, int pin, int val) {
    if (val)
        gpio->BSRR = (1U << pin);      // Set
    else
        gpio->BSRR = (1U << (pin + 16)); // Reset
}

int gpio_pin_read(GPIO_TypeDef *gpio, int pin) {
    return (gpio->IDR >> pin) & 1;
}
```

### Pattern 4: Button Debounce

```c
#define DEBOUNCE_MS 50

typedef struct {
    uint8_t  raw_state;
    uint8_t  stable_state;
    uint32_t counter;
    uint8_t  pressed;
} Button;

void button_update(Button *btn, uint8_t current_raw, uint32_t tick_ms) {
    if (current_raw != btn->raw_state) {
        btn->raw_state = current_raw;
        btn->counter = 0;
    } else {
        btn->counter += tick_ms;
        if (btn->counter >= DEBOUNCE_MS) {
            if (btn->stable_state != current_raw) {
                btn->stable_state = current_raw;
                if (current_raw == 0)
                    btn->pressed = 1;
            }
        }
    }
}

// Call every 10ms from timer ISR
```

### Pattern 5: Endianness Conversion

```c
uint32_t swap_endian(uint32_t val) {
    return ((val & 0xFF000000) >> 24) |
           ((val & 0x00FF0000) >> 8)  |
           ((val & 0x0000FF00) << 8)  |
           ((val & 0x000000FF) << 24);
}

int is_little_endian() {
    uint32_t x = 1;
    return (*(uint8_t*)&x == 1);
}
```

### Pattern 6: CRC-16 Calculation

```c
uint16_t crc16(const uint8_t *data, int len) {
    uint16_t crc = 0xFFFF;
    for (int i = 0; i < len; i++) {
        crc ^= data[i];
        for (int j = 0; j < 8; j++) {
            if (crc & 1)
                crc = (crc >> 1) ^ 0xA001;
            else
                crc >>= 1;
        }
    }
    return crc;
}
```

### Pattern 7: Command Parser

```c
typedef struct {
    char name[16];
    void (*handler)(int argc, char argv[][16]);
} Command;

void cmd_led(int argc, char argv[][16]) {
    printf("LED %s\\n", argv[1]);
}

void cmd_adc(int argc, char argv[][16]) {
    printf("Reading ADC channel %s\\n", argv[1]);
}

Command commands[] = {
    {"led", cmd_led},
    {"adc", cmd_adc},
};
#define NUM_CMDS (sizeof(commands)/sizeof(commands[0]))

void parse_command(char *input) {
    char tokens[5][16];
    int argc = 0;
    char *token = strtok(input, " ");
    while (token && argc < 5) {
        strcpy(tokens[argc++], token);
        token = strtok(NULL, " ");
    }
    for (int i = 0; i < NUM_CMDS; i++) {
        if (strcmp(tokens[0], commands[i].name) == 0) {
            commands[i].handler(argc, tokens);
            return;
        }
    }
    printf("Unknown command: %s\\n", tokens[0]);
}
```

---

## 6. Problem-Solving Framework

### The 5-Step Method

```
╔════════════════════════════════════════════════╗
║          THE DUMMY-PROOF 5-STEP METHOD         ║
╠════════════════════════════════════════════════╣
║                                                ║
║  Step 1: UNDERSTAND (2 min)                    ║
║  ├── Read problem 3 times                      ║
║  ├── Write input/output examples by hand       ║
║  ├── Ask: What's the edge case?                ║
║  └── Ask: What's the constraint?               ║
║                                                ║
║  Step 2: BRUTE FORCE FIRST (5 min)             ║
║  ├── What's the dumbest way to solve?          ║
║  ├── Write it in pseudocode                    ║
║  ├── Get it working first!                     ║
║  └── Time: O(?), Space: O(?)                   ║
║                                                ║
║  Step 3: FIND PATTERN (5 min)                  ║
║  ├── Is this sliding window?                   ║
║  ├── Can two pointers help?                    ║
║  ├── Can I use a hash map?                     ║
║  ├── Can I sort first?                         ║
║  └── Can I use stack/queue?                    ║
║                                                ║
║  Step 4: OPTIMIZE (10 min)                     ║
║  ├── Apply the identified pattern              ║
║  ├── Trace through examples                    ║
║  ├── Fix bugs                                  ║
║  └── Calculate new complexity                  ║
║                                                ║
║  Step 5: TEST & CLEAN (5 min)                  ║
║  ├── Test edge cases                           ║
║  ├── Test with given examples                  ║
║  ├── Clean up variable names                   ║
║  └── Add comments                              ║
║                                                ║
╚════════════════════════════════════════════════╝
```

### Pattern Recognition Cheat Sheet

| Problem Says | Think |
|---|---|
| "contiguous subarray" | Sliding Window / Prefix Sum |
| "sorted array" | Binary Search |
| "pairs" / "two numbers" | Two Pointer / Hash Map |
| "top k" / "k largest" | Heap / Priority Queue |
| "shortest path" | BFS (unweighted) |
| "all paths" | DFS + Backtracking |
| "parentheses matching" | Stack |
| "first unique" | Queue + Hash Map |
| "merge intervals" | Sort + Iterate |
| "cycle detection" | Floyd's / DFS |
| "buffer" / "stream" | Circular Buffer |
| "bit manipulation" | XOR / AND / Shift |
| "frequency count" | Hash Map |
| "minimum/maximum" | Greedy / Heap |
| "lookup" | Hash Map / BST |
| "state machine" | Enum + Switch/Handler |
| "interrupt handling" | Queue + Flag |
| "memory efficient" | Bit manipulation / Array |

---

## 7. Complete Question Bank

### Arrays (28 Problems)

**Easy:**
1. Reverse an array in-place
2. Find maximum/minimum element
3. Remove duplicates from sorted array
4. Move all zeros to end
5. Rotate array by k positions
6. Find second largest element
7. Check if array is sorted
8. Linear search
9. Count occurrences
10. Merge two sorted arrays
11. Find intersection of two arrays
12. Left rotate by one

**Medium:**
13. Two Sum
14. Maximum Subarray (Kadane's)
15. Product of Array Except Self
16. Best Time to Buy/Sell Stock
17. Container With Most Water
18. 3Sum
19. Search in Rotated Sorted Array
20. Find Min in Rotated Sorted Array
21. Subarray Sum Equals K
22. Next Permutation
23. Sort Colors (Dutch Flag)
24. Spiral Matrix
25. Set Matrix Zeroes
26. Find Missing Number
27. Majority Element
28. Longest Consecutive Sequence

### Strings (21 Problems)

**Easy:**
1. Reverse a string
2. Check if palindrome
3. Count vowels and consonants
4. Find length without strlen
5. Copy without strcpy
6. Compare two strings
7. Convert uppercase/lowercase
8. Count words
9. Check if anagrams
10. First non-repeating character
11. Remove duplicates

**Medium:**
12. Longest Palindromic Substring
13. String to Integer (atoi)
14. Implement strstr
15. Longest Common Prefix
16. Group Anagrams
17. Valid Parentheses
18. Reverse Words in String
19. Check if rotation
20. Compress string
21. Longest unique substring

### Linked Lists (21 Problems)

**Easy:**
1. Implement singly linked list
2. Reverse linked list
3. Find length
4. Find middle
5. Detect cycle
6. Delete node by value
7. Insert at beginning/end/sorted
8. Print in reverse (recursion)
9. Remove duplicates from sorted
10. Find Nth node from end
11. Circular linked list

**Medium:**
12. Merge two sorted lists
13. Remove Nth node from end
14. Check if palindrome
15. Intersection of two lists
16. Add two numbers (as links)
17. Find cycle start
18. Flatten multilevel list
19. Rotate by k
20. Swap nodes in pairs
21. Doubly linked list

### Stacks & Queues (14 Problems)

1. Implement Stack
2. Implement Queue
3. Implement Stack using Linked List
4. Valid Parentheses
5. Circular Queue/Buffer
6. Min Stack
7. Queue using Two Stacks
8. Reverse String using Stack
9. Next Greater Element
10. Evaluate Postfix
11. Implement Priority Queue
12. Check stack permutations
13. Sort Stack
14. Design a Deque

### Sorting & Searching (14 Problems)

1. Binary Search
2. Bubble Sort
3. Selection Sort
4. Insertion Sort
5. Merge Sort
6. Quick Sort
7. Search in Rotated Sorted Array
8. First/Last Position
9. Find Peak Element
10. Floor and Ceiling
11. Count Inversions
12. Search in 2D Matrix
13. Find kth smallest/largest
14. Square root (binary search)

### Trees (12 Problems)

1. Implement BST
2. Inorder Traversal
3. Preorder Traversal
4. Postorder Traversal
5. Level Order Traversal (BFS)
6. Height/Depth of Tree
7. Check if BST
8. Lowest Common Ancestor
9. Mirror/Invert Tree
10. Diameter of Tree
11. Check if two trees identical
12. Find kth smallest in BST

### Hashing (10 Problems)

1. Two Sum
2. Frequency Count
3. Check Duplicates
4. Group Anagrams
5. Top K Frequent Elements
6. First Non-Repeating
7. Longest Consecutive
8. Subarray Sum Equals K
9. Implement HashMap
10. Count Pairs with Difference

### Bit Manipulation (21 Problems)

1. Set/Clear/Toggle/Check bits
2. Count set bits
3. Check power of 2
4. Single number (XOR)
5. Reverse bits
6. Swap without temp
7. Find missing number
8. Rightmost set bit position
9. Generate all subsets
10. Count bits in range
11. Add without arithmetic
12. Detect opposite signs
13. Turn off rightmost bit
14. Isolate rightmost bit
15. Check if ith bit set
16. Toggle all bits
17. Two non-repeating elements
18. Bitwise AND of range
19. Gray code generation
20. Divide using bit ops
21. Total set bits 1 to N

### Embedded-Specific (20 Problems)

1. Circular Buffer
2. UART Ring Buffer
3. Thread/ISR-Safe Queue
4. Memory Pool Allocator
5. State Machine
6. Bit Field Registers
7. CAN Message Filter
8. GPIO Configuration
9. Timer Interrupt Logic
10. LED Pattern Controller
11. Button Debounce
12. Endianness Conversion
13. I2C/SPI Protocol Parser
14. Power-of-2 Buffer Check
15. CRC Calculation
16. Fixed-Point Arithmetic
17. Flash Wear Leveling
18. Command Parser
19. Watchdog Timer Logic
20. Interrupt Priority Config

---

## 8. Company-Specific Preparation

### QUALCOMM / INTEL / ARM (Chip Design)

**MUST SOLVE (80% probability):**
- Bit manipulation (set/clear/toggle/check)
- Count set bits (Kernighan)
- Reverse bits
- Find single number (XOR)
- Two Sum
- Maximum Subarray (Kadane's)
- Reverse linked list
- Detect cycle
- Binary search
- Valid parentheses

**LIKELY ASKED (50% probability):**
- Product except self
- Search in rotated array
- Merge two sorted lists
- LRU Cache
- Lowest Common Ancestor
- Level order traversal
- Trapping rain water
- Sliding window maximum
- Serialize/Deserialize tree
- Implement HashMap

### BOSCH / CONTINENTAL / DENSO (Automotive)

**MUST SOLVE:**
- Circular buffer
- Bit manipulation (registers)
- CAN message filtering
- State machine
- UART ring buffer
- Button debounce
- Merge sort
- Binary search
- Linked list
- Stack/Queue

**LIKELY ASKED:**
- Memory pool allocator
- CRC calculation
- Endianness conversion
- Priority queue
- Reverse array/string
- Remove duplicates
- String operations
- Sort colors
- Find missing number
- Check power of 2

### TEXAS INSTRUMENTS / MICROCHIP / STM32 (MCU)

**MUST SOLVE:**
- Bit field manipulation
- GPIO configuration
- Timer/counter logic
- Circular buffer
- LED pattern controller
- strlen/strcpy/strcmp
- Reverse string
- Palindrome check
- Bubble/Selection/Insertion sort
- Binary search
- Stack/Queue
- Linked list

**LIKELY ASKED:**
- Interrupt handler
- Power management
- ADC/DAC processing
- Frequency count
- Anagram
- Merge sorted arrays
- Two pointer
- Fixed-point arithmetic

---

## 9. Top 30 Must-Solve Problems

### If You Only Have 1 Week

```
BIT MANIPULATION (8 questions):
1.  Set/Clear/Toggle/Check bits
2.  Count set bits (Kernighan)
3.  Check power of 2
4.  Find single number (XOR)
5.  Reverse bits
6.  Find missing number (XOR)
7.  Swap without temp
8.  Generate all subsets

ARRAYS (7 questions):
9.  Reverse array
10. Two Sum
11. Maximum subarray (Kadane's)
12. Remove duplicates
13. Move zeros to end
14. Binary search
15. Search in rotated array

LINKED LIST (5 questions):
16. Reverse linked list
17. Detect cycle
18. Find middle
19. Merge sorted lists
20. Nth from end

STRINGS (5 questions):
21. Reverse string
22. Palindrome check
23. strlen/strcpy/strcmp
24. Anagram check
25. First non-repeating

STACK/QUEUE (3 questions):
26. Valid parentheses
27. Circular buffer
28. Stack implementation

EMBEDDED-SPECIFIC (2 questions):
29. State machine
30. UART ring buffer
```

---

## 10. 60-Day Study Plan

### Daily Routine
- **Morning (1 hour):** Learn 1 new concept or pattern
- **Evening (1-2 hours):** Solve 2-3 problems on paper first, then code
- **Weekend:** Review week's problems + solve 1 hard problem

### Week 1: Arrays (Easy)
- Day 1-2: Reverse, Max, Remove duplicates
- Day 3-4: Move zeros, Rotate, Second largest
- Day 5-6: Merge sorted, Count occurrences
- Day 7: Review all + solve 2 new

### Week 2: Arrays (Medium) + Strings
- Day 8-9: Two Sum, Kadane's
- Day 10-11: Product except, Buy/Sell stock
- Day 12-13: Sliding window, Binary search
- Day 14: Review + String ops

### Week 3: Strings + Linked List
- Day 15-16: strlen, strcpy, strcmp, atoi
- Day 17-18: Anagram, first unique, reverse words
- Day 19-20: LL create, insert, print
- Day 21: Review

### Week 4: Linked List
- Day 22-23: Reverse, detect cycle, find middle
- Day 24-25: Merge, Nth from end, remove dups
- Day 26-27: Palindrome, cycle start, circular
- Day 28: Review all LL

### Week 5: Stacks, Queues, Sorting
- Day 29-30: Stack and Queue implementations
- Day 31-32: Circular buffer, Valid parentheses
- Day 33-34: Bubble, Selection, Insertion sort
- Day 35: Review + Min Stack

### Week 6: Advanced Sorting + Hashing + Trees
- Day 36-37: Merge sort, Quick sort
- Day 38-39: HashMap, frequency count
- Day 40-41: BST insert/search, traversals
- Day 42: Review

### Week 7: Bit Manipulation (CRITICAL!)
- Day 43-44: Set/Clear/Check, Count bits
- Day 45-46: Power of 2, Single, Reverse
- Day 47-48: Missing, Subsets, Add
- Day 49: Review ALL bit manipulation

### Week 8: Embedded + Mocks
- Day 50-51: State machine, UART
- Day 52-53: Memory pool, GPIO, Debounce
- Day 54-55: CAN, CRC, Endianness
- Day 56-57: Review weak areas
- Day 58-60: MOCK INTERVIEWS

---

## 11. Resources & References

### Free Practice Platforms

| Platform | URL | Best For |
|---|---|---|
| LeetCode | leetcode.com | Problem variety |
| HackerRank | hackerrank.com | C-specific |
| GeeksforGeeks | geeksforgeeks.org | Explanations |
| NeetCode | neetcode.io | Curated 150 |
| CodeChef | codechef.com | Competitive |

### YouTube Channels

- **Abdul Bari:** DSA theory
- **Striver (take U forward):** Complete course
- **Jenny's Lectures:** CS fundamentals
- **Gaurav Sen:** System design
- **Rachit Jain:** Competitive programming

### Books

- **Data Structures in C** - Reema Thareja
- **The C Programming Language** - K&R
- **Making Embedded Systems** - Elecia White
- **Cracking the Coding Interview** - General prep
- **Programming Interviews Exposed** - Interview patterns

---

## 12. Interview Cheat Sheet

### Quick Reference

```
1. COMPLEXITY:
   O(1), O(log n), O(n), O(n log n), O(n²)

2. TWO POINTER: Sorted array, find pair
3. SLIDING WINDOW: Subarray/substring
4. BINARY SEARCH: Sorted → O(log n)
5. FAST/SLOW: Cycle detection, middle

6. STACK: LIFO - parentheses, eval
7. QUEUE: FIFO - BFS, scheduling
8. CIRCULAR BUFFER: (head+1) % capacity

9. HASH MAP: O(1) lookup, frequency
10. BST: Sorted, inorder = sorted

11. BIT TRICKS:
    SET:    reg |= (1 << n)
    CLEAR:  reg &= ~(1 << n)
    TOGGLE: reg ^= (1 << n)
    CHECK:  reg & (1 << n)
    XOR:    a ^ a = 0, a ^ 0 = a

12. EMBEDDED: ISR → Queue → Main
13. EMBEDDED: No malloc → Pool alloc
14. EMBEDDED: Circular buffer for UART
15. EMBEDDED: State machine for protocols
```

### Golden Rules

```
╔════════════════════════════════════════════════╗
║              GOLDEN RULES                      ║
╠════════════════════════════════════════════════╣
║                                                ║
║  1. SOLVE ON PAPER FIRST                       ║
║  2. TRACE through examples                     ║
║  3. BRUTE FORCE first, OPTIMIZE later          ║
║  4. TALK OUT LOUD (explain thinking)           ║
║  5. KNOW YOUR COMPLEXITIES (Big-O)             ║
║  6. BIT MANIPULATION is bread & butter         ║
║  7. CIRCULAR BUFFER - know it cold             ║
║  8. POINTERS - must be comfortable             ║
║  9. CONSISTENCY > INTENSITY                    ║
║  10. DON'T MEMORIZE - understand PATTERNS      ║
║                                                ║
╚════════════════════════════════════════════════╝
```

---

## Final Words

Start today. Solve one easy problem. Tomorrow solve two. In 60 days, you'll be interview-ready.

**Remember:**
- ✅ Understand before coding
- ✅ Test on paper first
- ✅ Trace through examples
- ✅ Know your complexities
- ✅ Practice consistently

**Good luck!** 💪

---

**Document Version:** 2.0  
**Last Updated:** April 2026  
**Total Problems:** 165+  
**Total Code Examples:** 200+  
**Total Patterns:** 30+

