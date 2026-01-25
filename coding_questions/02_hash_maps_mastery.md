# 🗺️ Mastering Hash Maps (Lookup Tables) in C: 20+ Questions from Easy to Medium

**Target Audience:** Embedded Developers who think in "Memory Addresses" and "Lookup Tables".
**Language:** C (Standard C99)

---

## 🧠 The Concept: Hash Map = Lookup Table (LUT)

In C, we don't have built-in "Dictionaries" like Python. We have two ways to do this:

1.  **Direct Addressing (Frequency Array):**
    - **Concept:** If keys are small (e.g., characters `a-z`, or numbers `1-1000`), we just use the key as the index of an array.
    - **Embedded View:** It's a Register Map. Offset `0x00` is 'a', Offset `0x01` is 'b'.
    - **Complexity:** O(1) Access.

2.  **True Hash Map (Struct + Linked List):**
    - **Concept:** When keys are huge (e.g., `1,000,000` or strings), we can't allocate an array that big. We calculate `index = key % SIZE` and store data there.
    - **Embedded View:** A "bucket" system for classifying data.

---

## 🎨 Visualization Key

```
Memory (Array): [ 0 ] [ 0 ] [ 0 ] [ 0 ]
Index:           0     1     2     3
Meaning:       Count of '0's, '1's, '2's...
```

---

## 🟢 Part 1: Easy (Frequency Arrays / Direct Lookup)

_Constraint: Keys are small integers or characters._

### 1. Count Character Frequency

**Problem:** Given string "embedded", count how many times each character appears.
**Visualization:**

```
Input: "beta"
Array `freq[26]` (Indices 0-25 represent a-z):

1. Read 'b' (index 1):
   [0] [1] [0] ...
    a   b   c

2. Read 'e' (index 4):
   [0] [1] [0] [0] [1] ...
    a   b   c   d   e

3. Read 't' ...
4. Read 'a' ...
```

**C Solution:**

```c
void countChars(char *str) {
    int freq[26] = {0}; // LUT for a-z
    for(int i = 0; str[i] != '\0'; i++) {
        freq[str[i] - 'a']++; // Map 'a'->0, 'b'->1
    }
}
```

### 2. First Unique Character to String

**Problem:** Find the first character that only appears once. "leetcode" -> 'l', "loveleetcode" -> 'v'.
**Visualization:**

```
1. Build Freq Map: "l"->1, "o"->2, "v"->1, "e"->4...
2. Re-read string LEFT to RIGHT:
   Check 'l': freq is 1? YES -> Return 'l'.
```

**C Solution:**

```c
int firstUniqChar(char *s) {
    int freq[26] = {0};
    // Pass 1: Fill LUT
    for(int i=0; s[i]; i++) freq[s[i]-'a']++;
    // Pass 2: Check LUT
    for(int i=0; s[i]; i++) {
        if(freq[s[i]-'a'] == 1) return i;
    }
    return -1;
}
```

### 3. Valid Anagram

**Problem:** s = "anagram", t = "nagaram". Return true if t is rearrangement of s.
**Embedded Logic:** If I increment for `s` and decrement for `t`, the buffer should allow be mostly ZEROS at the end.
**C Solution:**

```c
bool isAnagram(char *s, char *t) {
    if (strlen(s) != strlen(t)) return false;
    int table[26] = {0};
    for(int i=0; s[i]; i++) {
        table[s[i] - 'a']++; // +1 for s
        table[t[i] - 'a']--; // -1 for t
    }
    for(int i=0; i<26; i++) {
        if(table[i] != 0) return false;
    }
    return true;
}
```

### 4. Intersection of Two Arrays

**Problem:** nums1 = [1,2,2,1], nums2 = [2,2]. Result = [2].
**Logic:** Mark numbers present in `nums1`. Check `nums2` against mark.

### 5. Find the Missing Number (0 to n)

**Problem:** [3,0,1] (n=3). Missing is 2.
**Logic:**

1. Math Method: Sum(0..n) - Sum(arr).
2. HashMap Method: Mark `present[3]=1`, `present[0]=1`... then find `present[i]==0`.

### 6. Ransom Note

**Problem:** Can "ransomNote" be constructed from letters in "magazine"?
**Logic:** Count letters in magazine. Iterate note; decrement counts. If count < 0, False.

### 7. Majority Element (> n/2)

**Problem:** [3,2,3] -> 3.
**Logic:** Count freqs. Return if count > n/2. (Or Boyer-Moore Voting Algo for O(1) space).

### 8. Contains Duplicate

**Problem:** [1,2,3,1] -> True.
**Logic:** Mark `seen[num] = 1`. If `seen[num]` is already 1, return True.

### 9. Check if One String Swap Can Make Strings Equal

**Problem:** "bank", "kanb" -> True.
**Logic:** Freq maps must be identical. Diff positions count must be 0 or 2.

### 10. Find Common Characters

**Problem:** ["bella", "label", "roller"] -> ["e", "l", "l"]
**Logic:** Keep a "Min Freq" map. 'e' appears 1, 1, 1 time -> Min is 1. 'l' appears 2, 2, 2 -> Min is 2.

---

## 🟡 Part 2: Medium (Hash Maps / "Virtual" Hash Maps)

_Challenge: Negative numbers, large numbers, or index tracking._

### 🛠️ The "Mini-Hash" Boilerplate for C

For Medium problems in C where keys are large (impossible for arrays), use this simple "Separate Chaining" structure. Memorize this pattern!

```c
#include <stdlib.h>

#define HASH_SIZE 1000 // Bucket count

typedef struct Node {
    int key;
    int value; // or index
    struct Node* next; // Linked list for collisions
} Node;

Node* table[HASH_SIZE]; // The Hash Map

// Standard Hash Function: abs(key) % SIZE
int hash(int key) {
    int idx = key % HASH_SIZE;
    return (idx < 0) ? idx + HASH_SIZE : idx;
}

void insert(int key, int val) {
    int idx = hash(key);
    Node* n = (Node*)malloc(sizeof(Node));
    n->key = key; n->value = val; n->next = table[idx];
    table[idx] = n; // Push to front
}

int search(int key) { // Returns value or -1
    int idx = hash(key);
    Node* curr = table[idx];
    while(curr) {
        if(curr->key == key) return curr->value;
        curr = curr->next;
    }
    return -1000; // Error code
}
```

### 11. Two Sum (The Classic)

**Problem:** nums = [2,7,11,15], target = 9. Return indices [0, 1].
**Visualization:**

```
i=0, num=2. Need 7. Is 7 in map? No. Store {2: 0}.
i=1, num=7. Need 2. Is 2 in map? YES! (index 0).
Return {0, 1}.
```

_Requires the "Mini-Hash" above._

### 12. Group Anagrams

**Problem:** ["eat","tea","tan","ate","nat","bat"] -> [["bat"],["nat","tan"],["ate","eat","tea"]]
**Logic:** Sort each string to find its "Key". "eat"->"aet", "tea"->"aet".
Store original strings in a bucket labeled "aet".

### 13. Top K Frequent Elements

**Problem:** [1,1,1,2,2,3], k=2 -> [1,2]
**Logic:**

1. Freq Map: {1:3, 2:2, 3:1}.
2. Bucket Sort (Reverse Map): Index=Frequency.
   Arr[3] -> {1}
   Arr[2] -> {2}
   Result top 2: 1, 2.

### 14. Longest Consecutive Sequence

**Problem:** [100, 4, 200, 1, 3, 2] -> 4 (sequence 1,2,3,4)
**Logic:** Put all nums in Hash Set. For each num, check if `num-1` exists.
If NO (it's the start), count consecutive `num+1` in loop.

### 15. Subarray Sum Equals K

**Problem:** [1,1,1], k=2 -> 2.
**Logic:** Prefix Sum + Hash Map.
`CurrentSum - Target = OldSum`. If `OldSum` exists in map, we found a subarray.

### 16. Find All Duplicates in Array

**Problem:** [4,3,2,7,8,2,3,1] -> [2,3].
**Constraint:** O(n) time, O(1) space complexity!
**Logic:** Use the array ITSELF as the hash map.
Visit `arr[abs(x) - 1]`. If it's positive, make it negative (mark visited). If already negative, it's a duplicate!

### 17. Permutation in String

**Problem:** s1="ab", s2="eidbaooo" -> True (s2 contains permutation of s1).
**Logic:** Sliding Window + Hash Map.
Window size = len(s1). check if Window Freq Map == s1 Freq Map.

### 18. Contiguous Array

**Problem:** Binary array [0,1,0]. Find max length of subarray with equal 0s and 1s.
**Logic:** Treat 0 as -1.
Prefix Sum. If Sum=0, equal 0s/1s. If Sum previously seen, sub-array between has equal count.

### 19. Isomorphic Strings

**Problem:** "egg", "add" -> True. "foo", "bar" -> False.
**Logic:** Map 'e'->'a', 'g'->'d'. Check consistency.

### 20. Word Pattern

**Problem:** pattern="abba", s="dog cat cat dog" -> True.
**Logic:** Map 'a'->"dog", 'b'->"cat".

---

## 🏗️ 10 More to Practice (Advanced Regulars)

These follow the same patterns but combine mechanisms.

21. **Sort Characters By Frequency** (Map + Sort)
22. **Product of Array Except Self** (Prefix/Suffix "Maps")
23. **Replace Words** (Trie/Hash Set)
24. **Longest Absolute File Path** (Stack + Length Map)
25. **Brick Wall** (Map Edge Counts)
26. **Subdomain Visit Count** (String parsing + Map)
27. **Find and Replace Pattern** (Bi-directional mapping)
28. **Least Number of Unique Integers after K Removals**
29. **Check if Array Pairs are Divisible by k** (Remainder Map)
30. **Maximum Size Subarray Sum Equals k**

---

## 🎓 How to Practice This List "Smartly"

1.  **Don't write the full Hash Function each time.**
    - For char problems (#1-10), ALWAYS use `int freq[26] = {0};`.
    - For int problems, if range is small (e.g., `-1000` to `1000`), use `int map[2001]` and offset by `+1000`.
2.  **Focus on the Logic, not the Lib.**
    - In an embedded interview, if you say "I assume a standard hash map method `put(k,v)` exists...", they will usually say "Yes, go ahead."
    - Focus on **WHEN** to use it (Lookups, Counts, Caching).
