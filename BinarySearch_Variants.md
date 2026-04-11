# 🔍 Binary Search Patterns – Complete Guide

## 📌 Overview

Binary Search is a powerful algorithm used not only for searching elements in a sorted array but also for solving optimization and boundary problems.

This document covers:

* Classic Binary Search
* First/Last Occurrence (Boundary Search)
* Binary Search on Answer
* Pattern recognition tricks

---

# 🧠 1. Classic Binary Search

## 🎯 Use Case

Find a target element in a **sorted array**

## ✅ Code

```javascript
function binarySearch(arr, target) {
  let low = 0, high = arr.length - 1;

  while (low <= high) {
    let mid = Math.floor((low + high) / 2);

    if (arr[mid] === target) return mid;
    else if (arr[mid] < target) low = mid + 1;
    else high = mid - 1;
  }

  return -1;
}
```

## ⏱ Complexity

* Time: O(log n)
* Space: O(1)

---

# 🧠 2. First / Last Occurrence (Boundary Search)

## 🎯 Use Case

Find:

* First occurrence of element
* Last occurrence of element

## 🔥 Pattern

```
[1, 2, 2, 2, 3]
      ↑
   boundary
```

## ✅ First Occurrence

```javascript
function firstOccurrence(arr, target) {
  let low = 0, high = arr.length - 1;
  let ans = -1;

  while (low <= high) {
    let mid = Math.floor((low + high) / 2);

    if (arr[mid] === target) {
      ans = mid;
      high = mid - 1;
    } else if (arr[mid] < target) {
      low = mid + 1;
    } else {
      high = mid - 1;
    }
  }

  return ans;
}
```

---

# 🧠 3. Monotonic Pattern (00001111)

## 🎯 Use Case

Find transition point

## 🔥 Pattern

```
0 0 0 0 1 1 1 1
        ↑
     first 1
```

## ✅ Code

```javascript
function firstOne(arr) {
  let low = 0, high = arr.length - 1;
  let ans = -1;

  while (low <= high) {
    let mid = Math.floor((low + high) / 2);

    if (arr[mid] === 1) {
      ans = mid;
      high = mid - 1;
    } else {
      low = mid + 1;
    }
  }

  return ans;
}
```

---

# 🧠 4. Binary Search on Answer

## 🎯 Use Case

Find:

* Minimum possible value
* Maximum possible value

## 💡 Key Idea

Use a `check(mid)` function

## 🔥 Pattern

```
F F F F T T T T
        ↑
     answer
```

## ✅ Template

```javascript
function solve() {
  let left = MIN;
  let right = MAX;

  let check = (mid) => {
    // return true or false
  };

  while (left <= right) {
    let mid = Math.floor((left + right) / 2);

    if (check(mid)) {
      right = mid - 1;
    } else {
      left = mid + 1;
    }
  }

  return left;
}
```

---

# 🧠 5. Key Differences

| Feature   | Binary Search | Boundary Search | BS on Answer |
| --------- | ------------- | --------------- | ------------ |
| Goal      | Find element  | Find position   | Find value   |
| Data      | Sorted array  | Sorted array    | Range        |
| Condition | arr[mid]      | boundary logic  | check(mid)   |
| Pattern   | exact match   | duplicates      | monotonic    |

---

# 🧠 6. Pattern Recognition

## ✅ Use Classic Binary Search when:

* “Find target”
* “Search element”

---

## ✅ Use Boundary Search when:

* “First occurrence”
* “Last occurrence”
* Duplicates exist

---

## ✅ Use Binary Search on Answer when:

* “Minimum possible”
* “Maximum possible”
* “At least / at most”

---

# 🎯 Interview Strategy

## 🔥 Ask Yourself:

1. Am I searching an element?
   → Use Binary Search

2. Am I finding a boundary?
   → Use First/Last Occurrence

3. Am I minimizing/maximizing something?
   → Use Binary Search on Answer

---

# 🚨 Common Mistakes

* ❌ Using binary search on unsorted data
* ❌ Wrong condition in `check(mid)`
* ❌ Infinite loop due to wrong updates
* ❌ Confusing `left` vs `right` return

---

# 💯 Summary

* Binary Search is not just one algorithm — it's a **pattern**
* Recognizing the pattern is the key to solving problems
* Practice different variations to master it

---

# 🚀 Next Steps

* Practice 15+ problems for each pattern
* Focus on identifying monotonic behavior
* Master boundary conditions

---
