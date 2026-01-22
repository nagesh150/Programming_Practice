# 🎯 Part 1: Array Problems (Questions 1-15)

## Question 1: Find Maximum Element in Array

### Problem

Find the largest number in an array.

### Visualization

```
Array: [3, 7, 2, 9, 5, 1]

Step-by-step:
┌───────────────────────────────────────┐
│ Start: max = arr[0] = 3               │
├───────────────────────────────────────┤
│ [3]  7   2   9   5   1                │
│  ↑                                    │
│ max=3                                 │
├───────────────────────────────────────┤
│  3  [7]  2   9   5   1                │
│      ↑                                │
│ 7 > 3? YES → max=7                    │
├───────────────────────────────────────┤
│  3   7  [2]  9   5   1                │
│          ↑                            │
│ 2 > 7? NO → max=7                     │
├───────────────────────────────────────┤
│  3   7   2  [9]  5   1                │
│              ↑                        │
│ 9 > 7? YES → max=9                    │
├───────────────────────────────────────┤
│  3   7   2   9  [5]  1                │
│                  ↑                    │
│ 5 > 9? NO → max=9                     │
├───────────────────────────────────────┤
│  3   7   2   9   5  [1]               │
│                      ↑                │
│ 1 > 9? NO → max=9                     │
├───────────────────────────────────────┤
│ ANSWER: 9                             │
└───────────────────────────────────────┘
```

### C Code

```c
#include <stdio.h>

int findMax(int arr[], int n) {
    int max = arr[0];  // Assume first element is max

    for (int i = 1; i < n; i++) {
        if (arr[i] > max) {
            max = arr[i];  // Update max if current is larger
        }
    }
    return max;
}

int main() {
    int arr[] = {3, 7, 2, 9, 5, 1};
    int n = sizeof(arr) / sizeof(arr[0]);

    printf("Maximum: %d\n", findMax(arr, n));
    return 0;
}
```

### Key Points

- Time Complexity: O(n) - visit each element once
- Space Complexity: O(1) - only one variable needed

---

## Question 2: Find Second Largest Element

### Problem

Find the second largest number in an array.

### Visualization

```
Array: [12, 35, 1, 10, 34, 1]

Logic: Track TWO values - first and second

┌────────────────────────────────────────────────────┐
│ Initialize: first = -∞, second = -∞               │
├────────────────────────────────────────────────────┤
│ arr[0] = 12                                        │
│ 12 > first(-∞)? YES                               │
│ → second = first = -∞                             │
│ → first = 12                                       │
│ State: first=12, second=-∞                        │
├────────────────────────────────────────────────────┤
│ arr[1] = 35                                        │
│ 35 > first(12)? YES                               │
│ → second = first = 12                             │
│ → first = 35                                       │
│ State: first=35, second=12                        │
├────────────────────────────────────────────────────┤
│ arr[2] = 1                                         │
│ 1 > first(35)? NO                                 │
│ 1 > second(12)? NO                                │
│ State: first=35, second=12                        │
├────────────────────────────────────────────────────┤
│ arr[3] = 10                                        │
│ 10 > first(35)? NO                                │
│ 10 > second(12)? NO                               │
│ State: first=35, second=12                        │
├────────────────────────────────────────────────────┤
│ arr[4] = 34                                        │
│ 34 > first(35)? NO                                │
│ 34 > second(12)? YES → second=34                  │
│ State: first=35, second=34                        │
├────────────────────────────────────────────────────┤
│ ANSWER: second = 34                                │
└────────────────────────────────────────────────────┘
```

### C Code

```c
#include <stdio.h>
#include <limits.h>

int findSecondLargest(int arr[], int n) {
    int first = INT_MIN;
    int second = INT_MIN;

    for (int i = 0; i < n; i++) {
        if (arr[i] > first) {
            second = first;  // Old first becomes second
            first = arr[i];  // Current becomes first
        }
        else if (arr[i] > second && arr[i] != first) {
            second = arr[i];
        }
    }
    return second;
}

int main() {
    int arr[] = {12, 35, 1, 10, 34, 1};
    int n = sizeof(arr) / sizeof(arr[0]);

    printf("Second Largest: %d\n", findSecondLargest(arr, n));
    return 0;
}
```

---

## Question 3: Reverse an Array

### Problem

Reverse the elements of an array in-place.

### Visualization

```
Array: [1, 2, 3, 4, 5]

Two Pointer Approach:
┌─────────────────────────────────────────────────────┐
│ Initial:                                            │
│ [1]  [2]  [3]  [4]  [5]                            │
│  ↑                   ↑                              │
│ left=0            right=4                           │
├─────────────────────────────────────────────────────┤
│ Step 1: Swap arr[0] and arr[4]                      │
│ [5]  [2]  [3]  [4]  [1]                            │
│       ↑         ↑                                   │
│    left=1   right=3                                 │
├─────────────────────────────────────────────────────┤
│ Step 2: Swap arr[1] and arr[3]                      │
│ [5]  [4]  [3]  [2]  [1]                            │
│            ↑                                        │
│       left=2, right=2                               │
├─────────────────────────────────────────────────────┤
│ Step 3: left >= right, STOP!                        │
│                                                     │
│ Result: [5, 4, 3, 2, 1]                            │
└─────────────────────────────────────────────────────┘

Visual Swap:
    left                right
      ↓                   ↓
    [ 1 ]───────────────[ 5 ]
            SWAP!
    [ 5 ]───────────────[ 1 ]
```

### C Code

```c
#include <stdio.h>

void reverseArray(int arr[], int n) {
    int left = 0;
    int right = n - 1;

    while (left < right) {
        // Swap elements
        int temp = arr[left];
        arr[left] = arr[right];
        arr[right] = temp;

        left++;
        right--;
    }
}

void printArray(int arr[], int n) {
    for (int i = 0; i < n; i++) {
        printf("%d ", arr[i]);
    }
    printf("\n");
}

int main() {
    int arr[] = {1, 2, 3, 4, 5};
    int n = sizeof(arr) / sizeof(arr[0]);

    printf("Original: ");
    printArray(arr, n);

    reverseArray(arr, n);

    printf("Reversed: ");
    printArray(arr, n);

    return 0;
}
```

---

## Question 4: Two Sum - Find Pair with Given Sum

### Problem

Find two numbers in array that add up to target.

### Visualization

```
Array: [2, 7, 11, 15], Target: 9

Method 1: Brute Force (Easy to understand)
┌─────────────────────────────────────────────────────┐
│ Check ALL pairs:                                    │
│                                                     │
│ i=0: arr[0]=2                                       │
│   j=1: 2+7=9 ✓ FOUND!                              │
│                                                     │
│ Answer: indices [0, 1]                              │
└─────────────────────────────────────────────────────┘

Method 2: Hash Map (Optimal)
┌─────────────────────────────────────────────────────┐
│ For each number, check if (target - number) exists │
│                                                     │
│ i=0: arr[0]=2                                       │
│   need = 9 - 2 = 7                                  │
│   Is 7 in map? NO (map is empty)                   │
│   Store: map[2] = 0                                │
│   Map: {2: 0}                                       │
│                                                     │
│ i=1: arr[1]=7                                       │
│   need = 9 - 7 = 2                                  │
│   Is 2 in map? YES! at index 0                     │
│   FOUND! Return [0, 1]                             │
└─────────────────────────────────────────────────────┘
```

### C Code (Brute Force - Easier to understand)

```c
#include <stdio.h>

void twoSum(int arr[], int n, int target) {
    for (int i = 0; i < n - 1; i++) {
        for (int j = i + 1; j < n; j++) {
            if (arr[i] + arr[j] == target) {
                printf("Pair found at indices: %d and %d\n", i, j);
                printf("Values: %d + %d = %d\n", arr[i], arr[j], target);
                return;
            }
        }
    }
    printf("No pair found\n");
}

int main() {
    int arr[] = {2, 7, 11, 15};
    int n = sizeof(arr) / sizeof(arr[0]);
    int target = 9;

    twoSum(arr, n, target);
    return 0;
}
```

---

## Question 5: Move Zeros to End

### Problem

Move all zeros to the end while maintaining order of non-zero elements.

### Visualization

```
Array: [0, 1, 0, 3, 12]

Two Pointer Approach:
┌─────────────────────────────────────────────────────┐
│ 'insertPos' = position to place next non-zero      │
│                                                     │
│ Initial: insertPos = 0                              │
│ [0]  [1]  [0]  [3]  [12]                           │
│  ↑                                                  │
│  i=0, arr[0]=0, skip (it's zero)                   │
├─────────────────────────────────────────────────────┤
│ i=1, arr[1]=1 (non-zero!)                          │
│ Place 1 at insertPos=0                             │
│ [1]  [1]  [0]  [3]  [12]                           │
│       ↑                                             │
│ insertPos = 1                                       │
├─────────────────────────────────────────────────────┤
│ i=2, arr[2]=0, skip                                │
├─────────────────────────────────────────────────────┤
│ i=3, arr[3]=3 (non-zero!)                          │
│ Place 3 at insertPos=1                             │
│ [1]  [3]  [0]  [3]  [12]                           │
│            ↑                                        │
│ insertPos = 2                                       │
├─────────────────────────────────────────────────────┤
│ i=4, arr[4]=12 (non-zero!)                         │
│ Place 12 at insertPos=2                            │
│ [1]  [3]  [12]  [3]  [12]                          │
│                 ↑                                   │
│ insertPos = 3                                       │
├─────────────────────────────────────────────────────┤
│ Fill remaining with zeros:                          │
│ [1]  [3]  [12]  [0]  [0]                           │
│                                                     │
│ DONE!                                               │
└─────────────────────────────────────────────────────┘
```

### C Code

```c
#include <stdio.h>

void moveZeros(int arr[], int n) {
    int insertPos = 0;

    // Move all non-zero elements to front
    for (int i = 0; i < n; i++) {
        if (arr[i] != 0) {
            arr[insertPos] = arr[i];
            insertPos++;
        }
    }

    // Fill remaining positions with zeros
    while (insertPos < n) {
        arr[insertPos] = 0;
        insertPos++;
    }
}

int main() {
    int arr[] = {0, 1, 0, 3, 12};
    int n = sizeof(arr) / sizeof(arr[0]);

    moveZeros(arr, n);

    printf("Result: ");
    for (int i = 0; i < n; i++) {
        printf("%d ", arr[i]);
    }
    return 0;
}
```

---

## Question 6: Find Duplicate in Array

### Problem

Find the duplicate number (only one duplicate exists).

### Visualization

```
Array: [1, 3, 4, 2, 2]

Method: Counting (Simple approach)
┌─────────────────────────────────────────────────────┐
│ Count occurrences of each number:                   │
│                                                     │
│ Number │ Count                                      │
│ ───────┼───────                                     │
│   1    │  1                                         │
│   2    │  2  ← DUPLICATE!                          │
│   3    │  1                                         │
│   4    │  1                                         │
│                                                     │
│ Answer: 2                                           │
└─────────────────────────────────────────────────────┘
```

### C Code

```c
#include <stdio.h>
#include <stdlib.h>

int findDuplicate(int arr[], int n) {
    // Create count array
    int *count = (int *)calloc(n, sizeof(int));

    for (int i = 0; i < n; i++) {
        count[arr[i]]++;
        if (count[arr[i]] > 1) {
            free(count);
            return arr[i];
        }
    }

    free(count);
    return -1;
}

int main() {
    int arr[] = {1, 3, 4, 2, 2};
    int n = sizeof(arr) / sizeof(arr[0]);

    printf("Duplicate: %d\n", findDuplicate(arr, n));
    return 0;
}
```

---

## Question 7: Rotate Array by K positions

### Problem

Rotate array to the right by k steps.

### Visualization

```
Array: [1, 2, 3, 4, 5, 6, 7], k = 3

Method: Three Reversals
┌─────────────────────────────────────────────────────┐
│ Step 1: Reverse entire array                        │
│ [1, 2, 3, 4, 5, 6, 7]                              │
│          ↓                                          │
│ [7, 6, 5, 4, 3, 2, 1]                              │
├─────────────────────────────────────────────────────┤
│ Step 2: Reverse first k elements (0 to k-1)        │
│ [7, 6, 5] [4, 3, 2, 1]                             │
│     ↓                                               │
│ [5, 6, 7] [4, 3, 2, 1]                             │
├─────────────────────────────────────────────────────┤
│ Step 3: Reverse remaining elements (k to n-1)      │
│ [5, 6, 7] [4, 3, 2, 1]                             │
│               ↓                                     │
│ [5, 6, 7] [1, 2, 3, 4]                             │
├─────────────────────────────────────────────────────┤
│ Result: [5, 6, 7, 1, 2, 3, 4] ✓                    │
└─────────────────────────────────────────────────────┘

WHY THIS WORKS:
Original:  [1, 2, 3, 4 | 5, 6, 7]
                        ← move right by 3
Expected:  [5, 6, 7 | 1, 2, 3, 4]
```

### C Code

```c
#include <stdio.h>

void reverse(int arr[], int start, int end) {
    while (start < end) {
        int temp = arr[start];
        arr[start] = arr[end];
        arr[end] = temp;
        start++;
        end--;
    }
}

void rotateArray(int arr[], int n, int k) {
    k = k % n;  // Handle k > n

    // Step 1: Reverse entire array
    reverse(arr, 0, n - 1);

    // Step 2: Reverse first k elements
    reverse(arr, 0, k - 1);

    // Step 3: Reverse remaining elements
    reverse(arr, k, n - 1);
}

int main() {
    int arr[] = {1, 2, 3, 4, 5, 6, 7};
    int n = sizeof(arr) / sizeof(arr[0]);
    int k = 3;

    rotateArray(arr, n, k);

    printf("Rotated: ");
    for (int i = 0; i < n; i++) {
        printf("%d ", arr[i]);
    }
    return 0;
}
```

---

## Question 8: Find Missing Number (1 to N)

### Problem

Array contains n-1 numbers from 1 to n. Find the missing one.

### Visualization

```
Array: [1, 2, 4, 5, 6], n = 6

Method: Sum Formula
┌─────────────────────────────────────────────────────┐
│ Sum of 1 to n = n * (n + 1) / 2                    │
│                                                     │
│ Expected sum of 1 to 6:                             │
│ = 6 * 7 / 2 = 21                                   │
│                                                     │
│ Actual sum of array:                                │
│ = 1 + 2 + 4 + 5 + 6 = 18                           │
│                                                     │
│ Missing number = 21 - 18 = 3 ✓                     │
└─────────────────────────────────────────────────────┘

Visual:
Expected: [1] [2] [3] [4] [5] [6]
Actual:   [1] [2] [?] [4] [5] [6]
                   ↑
               Missing!
```

### C Code

```c
#include <stdio.h>

int findMissing(int arr[], int n) {
    // Expected sum of 1 to n
    int expectedSum = n * (n + 1) / 2;

    // Actual sum of array
    int actualSum = 0;
    for (int i = 0; i < n - 1; i++) {
        actualSum += arr[i];
    }

    return expectedSum - actualSum;
}

int main() {
    int arr[] = {1, 2, 4, 5, 6};
    int n = 6;  // Numbers should be 1 to 6

    printf("Missing number: %d\n", findMissing(arr, n));
    return 0;
}
```

---

## Question 9: Check if Array is Sorted

### Problem

Determine if array is sorted in ascending order.

### Visualization

```
Array 1: [1, 2, 3, 4, 5] - SORTED ✓
Array 2: [1, 3, 2, 4, 5] - NOT SORTED ✗

Logic:
┌─────────────────────────────────────────────────────┐
│ For sorted array: arr[i] <= arr[i+1] for all i     │
│                                                     │
│ Array: [1, 3, 2, 4, 5]                             │
│                                                     │
│ Check: 1 <= 3? ✓                                   │
│ Check: 3 <= 2? ✗ NOT SORTED!                       │
│                                                     │
│        [1]  [3]  [2]  [4]  [5]                     │
│              ↓    ↓                                 │
│              3 >  2  = Problem!                     │
└─────────────────────────────────────────────────────┘
```

### C Code

```c
#include <stdio.h>
#include <stdbool.h>

bool isSorted(int arr[], int n) {
    for (int i = 0; i < n - 1; i++) {
        if (arr[i] > arr[i + 1]) {
            return false;
        }
    }
    return true;
}

int main() {
    int arr1[] = {1, 2, 3, 4, 5};
    int arr2[] = {1, 3, 2, 4, 5};

    printf("Array 1 sorted: %s\n", isSorted(arr1, 5) ? "Yes" : "No");
    printf("Array 2 sorted: %s\n", isSorted(arr2, 5) ? "Yes" : "No");

    return 0;
}
```

---

## Question 10: Merge Two Sorted Arrays

### Problem

Merge two sorted arrays into one sorted array.

### Visualization

```
arr1: [1, 3, 5, 7]
arr2: [2, 4, 6, 8]

Two Pointer Merge:
┌─────────────────────────────────────────────────────┐
│ arr1:  [1]  [3]  [5]  [7]                          │
│         ↑                                           │
│         i                                           │
│                                                     │
│ arr2:  [2]  [4]  [6]  [8]                          │
│         ↑                                           │
│         j                                           │
│                                                     │
│ Compare arr1[i]=1 vs arr2[j]=2                     │
│ 1 < 2, take 1                                       │
│ result: [1]                                         │
├─────────────────────────────────────────────────────┤
│ arr1:  [1]  [3]  [5]  [7]                          │
│              ↑                                      │
│              i                                      │
│                                                     │
│ arr2:  [2]  [4]  [6]  [8]                          │
│         ↑                                           │
│         j                                           │
│                                                     │
│ Compare arr1[i]=3 vs arr2[j]=2                     │
│ 2 < 3, take 2                                       │
│ result: [1, 2]                                      │
├─────────────────────────────────────────────────────┤
│ ... continue until done ...                         │
│                                                     │
│ Final: [1, 2, 3, 4, 5, 6, 7, 8]                    │
└─────────────────────────────────────────────────────┘
```

### C Code

```c
#include <stdio.h>

void mergeSortedArrays(int arr1[], int n1, int arr2[], int n2, int result[]) {
    int i = 0, j = 0, k = 0;

    // Compare and merge
    while (i < n1 && j < n2) {
        if (arr1[i] <= arr2[j]) {
            result[k] = arr1[i];
            i++;
        } else {
            result[k] = arr2[j];
            j++;
        }
        k++;
    }

    // Copy remaining elements from arr1
    while (i < n1) {
        result[k] = arr1[i];
        i++;
        k++;
    }

    // Copy remaining elements from arr2
    while (j < n2) {
        result[k] = arr2[j];
        j++;
        k++;
    }
}

int main() {
    int arr1[] = {1, 3, 5, 7};
    int arr2[] = {2, 4, 6, 8};
    int n1 = 4, n2 = 4;
    int result[8];

    mergeSortedArrays(arr1, n1, arr2, n2, result);

    printf("Merged: ");
    for (int i = 0; i < n1 + n2; i++) {
        printf("%d ", result[i]);
    }
    return 0;
}
```

---

## Question 11-15: Quick Reference

| #   | Problem                                 | Key Technique       |
| --- | --------------------------------------- | ------------------- |
| 11  | Find intersection of two arrays         | Hash Map or Sorting |
| 12  | Find Union of two arrays                | Hash Set            |
| 13  | Find majority element (>n/2 times)      | Boyer-Moore Voting  |
| 14  | Find leaders in array                   | Traverse from right |
| 15  | Maximum difference (arr[j]-arr[i], j>i) | Track minimum       |

---

_Continue to Part 2: String Problems_
