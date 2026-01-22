# 🎯 Part 5: Binary Trees (Questions 56-65)

## Question 56: Binary Tree Traversals

### Visualization

```
Tree:
        1
       / \
      2   3
     / \
    4   5

Three Types of Traversal:
┌────────────────────────────────────────────────┐
│ INORDER (Left, Root, Right):                   │
│ Visit: 4 → 2 → 5 → 1 → 3                      │
│                                                │
│ PREORDER (Root, Left, Right):                  │
│ Visit: 1 → 2 → 4 → 5 → 3                      │
│                                                │
│ POSTORDER (Left, Right, Root):                 │
│ Visit: 4 → 5 → 2 → 3 → 1                      │
│                                                │
│ LEVEL ORDER (BFS):                             │
│ Visit: 1 → 2 → 3 → 4 → 5                      │
└────────────────────────────────────────────────┘

Memory Trick:
- INorder   = Left IN between
- PREorder  = Root comes PRE (first)
- POSTorder = Root comes POST (last)
```

### C Code

```c
struct TreeNode {
    int val;
    struct TreeNode* left;
    struct TreeNode* right;
};

// Inorder: Left → Root → Right
void inorder(struct TreeNode* root) {
    if (root == NULL) return;
    inorder(root->left);
    printf("%d ", root->val);
    inorder(root->right);
}

// Preorder: Root → Left → Right
void preorder(struct TreeNode* root) {
    if (root == NULL) return;
    printf("%d ", root->val);
    preorder(root->left);
    preorder(root->right);
}

// Postorder: Left → Right → Root
void postorder(struct TreeNode* root) {
    if (root == NULL) return;
    postorder(root->left);
    postorder(root->right);
    printf("%d ", root->val);
}
```

---

## Question 57: Height/Depth of Binary Tree

### Visualization

```
        1         ← Level 0
       / \
      2   3       ← Level 1
     / \
    4   5         ← Level 2

Height = Maximum depth = 2

Recursive thinking:
┌────────────────────────────────────────────────┐
│ height(node) = 1 + max(height(left),          │
│                        height(right))          │
│                                                │
│ height(4) = 0 (leaf)                          │
│ height(5) = 0 (leaf)                          │
│ height(2) = 1 + max(0,0) = 1                  │
│ height(3) = 0 (leaf)                          │
│ height(1) = 1 + max(1,0) = 2                  │
└────────────────────────────────────────────────┘
```

### C Code

```c
int height(struct TreeNode* root) {
    if (root == NULL) return -1;  // or 0, based on definition

    int leftHeight = height(root->left);
    int rightHeight = height(root->right);

    return 1 + (leftHeight > rightHeight ? leftHeight : rightHeight);
}
```

---

## Question 58: Check if Tree is Balanced

### Visualization

```
Balanced (height diff ≤ 1):     Unbalanced:
        1                           1
       / \                         /
      2   3                       2
     / \                         /
    4   5                       3

Left height=2, Right height=1   Left height=2, Right=0
Diff=1 ≤ 1 ✓ BALANCED          Diff=2 > 1 ✗ NOT BALANCED
```

### C Code

```c
int checkBalance(struct TreeNode* root) {
    if (root == NULL) return 0;

    int leftH = checkBalance(root->left);
    if (leftH == -1) return -1;

    int rightH = checkBalance(root->right);
    if (rightH == -1) return -1;

    if (abs(leftH - rightH) > 1) return -1;

    return 1 + (leftH > rightH ? leftH : rightH);
}

bool isBalanced(struct TreeNode* root) {
    return checkBalance(root) != -1;
}
```

---

## Question 59: Lowest Common Ancestor (LCA)

### Visualization

```
        3
       / \
      5   1
     / \ / \
    6  2 0  8

LCA of 5 and 1? → 3 (first common parent)
LCA of 5 and 6? → 5 (5 is ancestor of 6)
LCA of 6 and 2? → 5

Logic:
┌────────────────────────────────────────────────┐
│ If current node == p or q → return current    │
│ Search left subtree                            │
│ Search right subtree                           │
│ If both found something → current is LCA      │
│ If only one found → return that one           │
└────────────────────────────────────────────────┘
```

### C Code

```c
struct TreeNode* lowestCommonAncestor(struct TreeNode* root,
                                       struct TreeNode* p,
                                       struct TreeNode* q) {
    if (root == NULL || root == p || root == q)
        return root;

    struct TreeNode* left = lowestCommonAncestor(root->left, p, q);
    struct TreeNode* right = lowestCommonAncestor(root->right, p, q);

    if (left && right) return root;  // Found in both sides
    return left ? left : right;       // Return non-null
}
```

---

## Question 60: Level Order Traversal (BFS)

### Visualization

```
        1
       / \
      2   3
     / \   \
    4   5   6

Level 0: [1]
Level 1: [2, 3]
Level 2: [4, 5, 6]

Using Queue:
┌────────────────────────────────────────────────┐
│ Queue: [1]                                     │
│ Process 1, add children → Queue: [2,3]        │
│ Process 2, add children → Queue: [3,4,5]      │
│ Process 3, add children → Queue: [4,5,6]      │
│ Process 4,5,6 (no children)                   │
└────────────────────────────────────────────────┘
```

---

## Question 61: Check if Trees are Identical

### Visualization

```
Tree 1:     Tree 2:
    1           1
   / \         / \
  2   3       2   3

Compare:
- Root values same? 1==1 ✓
- Left subtrees identical? 2==2 ✓
- Right subtrees identical? 3==3 ✓
→ IDENTICAL!
```

### C Code

```c
bool isSameTree(struct TreeNode* p, struct TreeNode* q) {
    if (p == NULL && q == NULL) return true;
    if (p == NULL || q == NULL) return false;

    return (p->val == q->val) &&
           isSameTree(p->left, q->left) &&
           isSameTree(p->right, q->right);
}
```

---

## Question 62: Invert/Mirror Binary Tree

### Visualization

```
Original:       Inverted:
    1               1
   / \             / \
  2   3    →     3   2
 / \               / \
4   5             5   4
```

### C Code

```c
struct TreeNode* invertTree(struct TreeNode* root) {
    if (root == NULL) return NULL;

    // Swap children
    struct TreeNode* temp = root->left;
    root->left = root->right;
    root->right = temp;

    // Recursively invert subtrees
    invertTree(root->left);
    invertTree(root->right);

    return root;
}
```

---

## Questions 63-65 Quick Reference

| #   | Problem                          | Key Technique      |
| --- | -------------------------------- | ------------------ |
| 63  | Path sum (root to leaf = target) | DFS + subtract     |
| 64  | Maximum path sum                 | DFS, track max     |
| 65  | Serialize/Deserialize tree       | Preorder + markers |
