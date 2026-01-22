# 🎯 Part 6: Searching & Sorting (Questions 66-75)

## Question 66: Binary Search

### Visualization

```
Sorted Array: [1, 3, 5, 7, 9, 11, 13], Target: 7

┌────────────────────────────────────────────────┐
│ Step 1:                                        │
│ [1, 3, 5, 7, 9, 11, 13]                       │
│  ↑        ↑          ↑                         │
│ low=0   mid=3      high=6                      │
│ arr[3]=7, 7==7? YES! Found at index 3         │
└────────────────────────────────────────────────┘

Another example, Target: 11
┌────────────────────────────────────────────────┐
│ Step 1: mid=3, arr[3]=7, 11>7 → search right  │
│ [1, 3, 5, 7, 9, 11, 13]                       │
│              ↑    ↑    ↑                       │
│           low=4 mid=5 high=6                   │
│                                                │
│ arr[5]=11, 11==11? Found at index 5!          │
└────────────────────────────────────────────────┘

Key: Eliminate half of search space each step
Time: O(log n) - Very fast!
```

### C Code

```c
int binarySearch(int arr[], int n, int target) {
    int low = 0, high = n - 1;

    while (low <= high) {
        int mid = low + (high - low) / 2;  // Avoid overflow

        if (arr[mid] == target) {
            return mid;
        } else if (arr[mid] < target) {
            low = mid + 1;   // Search right half
        } else {
            high = mid - 1;  // Search left half
        }
    }
    return -1;  // Not found
}
```

---

## Question 67: Bubble Sort

### Visualization

```
Array: [5, 3, 8, 4, 2]

Bubble largest element to end each pass:
┌────────────────────────────────────────────────┐
│ Pass 1: Compare adjacent, swap if needed       │
│ [5,3,8,4,2] → [3,5,8,4,2] (swap 5,3)          │
│ [3,5,8,4,2] → [3,5,8,4,2] (5<8, no swap)      │
│ [3,5,8,4,2] → [3,5,4,8,2] (swap 8,4)          │
│ [3,5,4,8,2] → [3,5,4,2,8] (swap 8,2)          │
│                          8 is now at end!      │
├────────────────────────────────────────────────┤
│ Pass 2: [3,5,4,2,8]                            │
│ → [3,5,4,2,8] → [3,4,5,2,8] → [3,4,2,5,8]    │
├────────────────────────────────────────────────┤
│ Continue until sorted: [2,3,4,5,8]            │
└────────────────────────────────────────────────┘
```

### C Code

```c
void bubbleSort(int arr[], int n) {
    for (int i = 0; i < n - 1; i++) {
        int swapped = 0;
        for (int j = 0; j < n - i - 1; j++) {
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
```

---

## Question 68: Selection Sort

### Visualization

```
Array: [64, 25, 12, 22, 11]

Find minimum, place at beginning:
┌────────────────────────────────────────────────┐
│ Pass 1: Find min in [64,25,12,22,11]          │
│         min=11 at index 4                      │
│         Swap with index 0                      │
│         [11, 25, 12, 22, 64]                  │
├────────────────────────────────────────────────┤
│ Pass 2: Find min in [25,12,22,64]             │
│         min=12 at index 2                      │
│         [11, 12, 25, 22, 64]                  │
├────────────────────────────────────────────────┤
│ Continue: [11, 12, 22, 25, 64]                │
└────────────────────────────────────────────────┘
```

---

## Question 69: Insertion Sort

### Visualization

```
Array: [5, 2, 4, 6, 1]

Insert each element in sorted position:
┌────────────────────────────────────────────────┐
│ [5] | 2, 4, 6, 1    (5 is sorted)             │
│ Insert 2: [2, 5] | 4, 6, 1                    │
│ Insert 4: [2, 4, 5] | 6, 1                    │
│ Insert 6: [2, 4, 5, 6] | 1                    │
│ Insert 1: [1, 2, 4, 5, 6]                     │
└────────────────────────────────────────────────┘

Like sorting playing cards in your hand!
```

### C Code

```c
void insertionSort(int arr[], int n) {
    for (int i = 1; i < n; i++) {
        int key = arr[i];
        int j = i - 1;

        // Shift elements greater than key
        while (j >= 0 && arr[j] > key) {
            arr[j + 1] = arr[j];
            j--;
        }
        arr[j + 1] = key;
    }
}
```

---

## Question 70: Merge Sort

### Visualization

```
Array: [38, 27, 43, 3, 9, 82, 10]

Divide and Conquer:
┌────────────────────────────────────────────────┐
│     [38, 27, 43, 3, 9, 82, 10]                │
│           /              \                     │
│    [38,27,43,3]    [9,82,10]                  │
│      /      \        /    \                    │
│   [38,27] [43,3]  [9,82] [10]                 │
│    /  \    /  \    /  \                       │
│  [38][27][43][3] [9][82][10]                  │
│    \  /    \  /    \  /                       │
│   [27,38] [3,43]  [9,82] [10]                 │
│      \      /        \    /                    │
│    [3,27,38,43]    [9,10,82]                  │
│           \              /                     │
│     [3, 9, 10, 27, 38, 43, 82]               │
└────────────────────────────────────────────────┘

Time: O(n log n) - Always!
Space: O(n) - Needs extra array
```

---

## Question 71: Quick Sort

### Visualization

```
Array: [10, 7, 8, 9, 1, 5], Pivot = 5

Partition: Move elements < pivot to left
┌────────────────────────────────────────────────┐
│ [10, 7, 8, 9, 1, 5]  pivot=5                  │
│                                                │
│ After partition:                               │
│ [1] [5] [8, 9, 7, 10]                         │
│  ↑   ↑       ↑                                │
│ <5  pivot   >5                                │
│                                                │
│ Recursively sort left and right parts         │
│ Final: [1, 5, 7, 8, 9, 10]                    │
└────────────────────────────────────────────────┘

Average: O(n log n)
Worst: O(n²) - when already sorted
```

---

## Question 72: Search in Rotated Sorted Array

### Visualization

```
Original: [1, 2, 3, 4, 5, 6, 7]
Rotated:  [4, 5, 6, 7, 1, 2, 3], Target: 1

Binary search with twist:
┌────────────────────────────────────────────────┐
│ [4, 5, 6, 7, 1, 2, 3]                         │
│  ↑        ↑        ↑                           │
│ low=0   mid=3    high=6                        │
│                                                │
│ arr[mid]=7, target=1                           │
│ Left half [4,5,6,7] is sorted (4<7)           │
│ Is 1 in [4,7]? NO → search right              │
│                                                │
│ [4, 5, 6, 7, 1, 2, 3]                         │
│              ↑  ↑  ↑                           │
│           low=4 mid high                       │
│                                                │
│ Found at index 4!                              │
└────────────────────────────────────────────────┘
```

---

## Questions 73-75 Quick Reference

| #   | Problem                     | Key Technique              |
| --- | --------------------------- | -------------------------- |
| 73  | Find peak element           | Binary search variant      |
| 74  | Search in 2D matrix         | Treat as 1D or staircase   |
| 75  | Median of two sorted arrays | Binary search, O(log(m+n)) |

## Sorting Comparison

```
┌──────────────┬─────────────┬─────────────┬──────────┐
│ Algorithm    │ Best        │ Worst       │ Space    │
├──────────────┼─────────────┼─────────────┼──────────┤
│ Bubble       │ O(n)        │ O(n²)       │ O(1)     │
│ Selection    │ O(n²)       │ O(n²)       │ O(1)     │
│ Insertion    │ O(n)        │ O(n²)       │ O(1)     │
│ Merge        │ O(n log n)  │ O(n log n)  │ O(n)     │
│ Quick        │ O(n log n)  │ O(n²)       │ O(log n) │
│ Heap         │ O(n log n)  │ O(n log n)  │ O(1)     │
└──────────────┴─────────────┴─────────────┴──────────┘
```
