# 🎯 Part 4: Stack & Queue Problems (Questions 46-55)

## Question 46: Implement Stack using Array

### Visualization

```
Stack Operations (LIFO - Last In First Out)

PUSH 10, PUSH 20, PUSH 30:
┌─────┐
│ 30  │ ← top
├─────┤
│ 20  │
├─────┤
│ 10  │
└─────┘

POP: Returns 30, top moves down
┌─────┐
│ 20  │ ← top
├─────┤
│ 10  │
└─────┘
```

### C Code

```c
#define MAX 100

typedef struct {
    int arr[MAX];
    int top;
} Stack;

void init(Stack* s) { s->top = -1; }

int isEmpty(Stack* s) { return s->top == -1; }

int isFull(Stack* s) { return s->top == MAX - 1; }

void push(Stack* s, int val) {
    if (!isFull(s)) s->arr[++s->top] = val;
}

int pop(Stack* s) {
    if (!isEmpty(s)) return s->arr[s->top--];
    return -1;
}

int peek(Stack* s) {
    if (!isEmpty(s)) return s->arr[s->top];
    return -1;
}
```

---

## Question 47: Valid Parentheses

### Visualization

```
String: "({[]})"

Process each character:
┌────────────────────────────────────────────────┐
│ '(' → push     Stack: [( ]                    │
│ '{' → push     Stack: [( { ]                  │
│ '[' → push     Stack: [( { [ ]                │
│ ']' → matches '[', pop   Stack: [( { ]        │
│ '}' → matches '{', pop   Stack: [( ]          │
│ ')' → matches '(', pop   Stack: [ ]           │
│                                                │
│ Stack empty → VALID ✓                         │
└────────────────────────────────────────────────┘

Invalid example: "([)]"
'(' push, '[' push, ')' doesn't match '[' → INVALID
```

### C Code

```c
bool isValid(char* s) {
    char stack[10000];
    int top = -1;

    for (int i = 0; s[i]; i++) {
        char c = s[i];

        if (c == '(' || c == '{' || c == '[') {
            stack[++top] = c;
        } else {
            if (top == -1) return false;

            char t = stack[top--];
            if ((c == ')' && t != '(') ||
                (c == '}' && t != '{') ||
                (c == ']' && t != '[')) {
                return false;
            }
        }
    }
    return top == -1;
}
```

---

## Question 48: Next Greater Element

### Visualization

```
Array: [4, 5, 2, 10, 8]
Find next greater element for each

Using Monotonic Stack:
┌────────────────────────────────────────────────┐
│ Process right to left:                         │
│                                                │
│ i=4: 8  → Stack empty, NGE=-1, push 8         │
│ i=3: 10 → Stack[8]<10, pop, empty, NGE=-1     │
│         push 10                                │
│ i=2: 2  → Stack[10]>2, NGE=10, push 2         │
│ i=1: 5  → Stack[2]<5 pop, [10]>5, NGE=10      │
│         push 5                                 │
│ i=0: 4  → Stack[5]>4, NGE=5, push 4           │
│                                                │
│ Result: [5, 10, 10, -1, -1]                   │
└────────────────────────────────────────────────┘
```

---

## Question 49: Implement Queue using Stacks

### Visualization

```
Use 2 stacks: inStack, outStack

Enqueue 1,2,3:
inStack:  [1,2,3]  (3 on top)
outStack: []

Dequeue (need to return 1):
1. Move all from inStack to outStack
   inStack:  []
   outStack: [3,2,1]  (1 on top)
2. Pop outStack → returns 1

Key: outStack reverses order!
```

### C Code

```c
typedef struct {
    Stack inStack;
    Stack outStack;
} Queue;

void enqueue(Queue* q, int val) {
    push(&q->inStack, val);
}

int dequeue(Queue* q) {
    if (isEmpty(&q->outStack)) {
        // Move all elements from inStack to outStack
        while (!isEmpty(&q->inStack)) {
            push(&q->outStack, pop(&q->inStack));
        }
    }
    return pop(&q->outStack);
}
```

---

## Question 50: Min Stack (Get Min in O(1))

### Visualization

```
Maintain two stacks: main stack + min stack

Operations: push(3), push(5), push(2), push(1)
┌────────────────────────────────────────────────┐
│ Main Stack    Min Stack                        │
│ ┌───┐         ┌───┐                           │
│ │ 1 │         │ 1 │ ← current min             │
│ ├───┤         ├───┤                           │
│ │ 2 │         │ 2 │                           │
│ ├───┤         ├───┤                           │
│ │ 5 │         │ 3 │                           │
│ ├───┤         ├───┤                           │
│ │ 3 │         │ 3 │                           │
│ └───┘         └───┘                           │
│                                                │
│ getMin() → peek minStack → 1                  │
│ pop() → pop both → min becomes 2              │
└────────────────────────────────────────────────┘
```

---

## Question 51: Evaluate Postfix Expression

### Visualization

```
Expression: "23*54*+"  (which is (2*3)+(5*4))

┌────────────────────────────────────────────────┐
│ '2' → push 2        Stack: [2]                │
│ '3' → push 3        Stack: [2,3]              │
│ '*' → pop 3,2       2*3=6                     │
│       push 6        Stack: [6]                │
│ '5' → push 5        Stack: [6,5]              │
│ '4' → push 4        Stack: [6,5,4]            │
│ '*' → pop 4,5       5*4=20                    │
│       push 20       Stack: [6,20]             │
│ '+' → pop 20,6      6+20=26                   │
│       push 26       Stack: [26]               │
│                                                │
│ Result: 26 ✓                                  │
└────────────────────────────────────────────────┘
```

---

## Questions 52-55 Quick Reference

| #   | Problem                        | Key Technique                  |
| --- | ------------------------------ | ------------------------------ |
| 52  | Stock span problem             | Monotonic stack                |
| 53  | Largest rectangle in histogram | Stack + area calculation       |
| 54  | Sliding window maximum         | Deque (double-ended queue)     |
| 55  | Implement circular queue       | Array with front/rear pointers |
