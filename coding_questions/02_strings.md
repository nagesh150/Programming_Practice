# 🎯 Part 2: String Problems (Questions 16-30)

## Question 16: Reverse a String

### Visualization

```
String: "HELLO" → "OLLEH"

  H   E   L   L   O
  ↑               ↑
left=0         right=4

Swap H↔O: O E L L H, move pointers
Swap E↔L: O L L E H, DONE!
```

### C Code

```c
void reverseString(char str[]) {
    int left = 0, right = strlen(str) - 1;
    while (left < right) {
        char temp = str[left];
        str[left++] = str[right];
        str[right--] = temp;
    }
}
```

---

## Question 17: Check Palindrome

### Visualization

```
"RADAR" - Check if same forwards & backwards

  R   A   D   A   R
  ↑               ↑
  R == R ✓ (continue)
      ↑       ↑
      A == A ✓ (continue)
          ↑
    left >= right → PALINDROME ✓
```

### C Code

```c
bool isPalindrome(char str[]) {
    int left = 0, right = strlen(str) - 1;
    while (left < right) {
        if (str[left++] != str[right--]) return false;
    }
    return true;
}
```

---

## Question 18: Count Character Frequency

### Visualization

```
"hello" → h:1, e:1, l:2, o:1

Use array[26] for a-z:
index = char - 'a'
'h'-'a' = 7 → count[7]++
```

### C Code

```c
void countFrequency(char str[]) {
    int count[26] = {0};
    for (int i = 0; str[i]; i++)
        count[str[i] - 'a']++;
    for (int i = 0; i < 26; i++)
        if (count[i]) printf("%c:%d ", 'a'+i, count[i]);
}
```

---

## Question 19: First Non-Repeating Character

### Visualization

```
"leetcode"
Count: l:1, e:3, t:1, c:1, o:1, d:1
First with count=1 → 'l' at index 0
```

---

## Question 20: Check Anagram

### Visualization

```
"listen" & "silent" - Same letters, different order

Count both, compare:
listen: e:1,i:1,l:1,n:1,s:1,t:1
silent: e:1,i:1,l:1,n:1,s:1,t:1
MATCH → Anagram ✓
```

---

## Questions 21-30 Quick Reference

| #   | Problem                  | Key Idea                       |
| --- | ------------------------ | ------------------------------ |
| 21  | Remove duplicates        | Boolean seen[] array           |
| 22  | Count words              | Count space→letter transitions |
| 23  | Longest unique substring | Sliding window                 |
| 24  | String compression       | Two pointers + count           |
| 25  | Check rotation           | s1+s1 contains s2?             |
| 26  | Longest common prefix    | Compare char by char           |
| 27  | Valid parentheses        | Stack                          |
| 28  | Reverse words            | Reverse all, then each word    |
| 29  | atoi implementation      | Parse digit by digit           |
| 30  | Pattern matching         | Sliding window                 |
