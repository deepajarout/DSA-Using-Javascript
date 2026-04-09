# 📘 Sliding Window – Complete Guide (Interview + Code + Patterns)

---

# 📌 1. What is Sliding Window?

Sliding Window is an **optimized technique** used to solve problems involving:

- Arrays
- Strings
- Subarrays / Substrings (contiguous)

Instead of recalculating values again and again, we:
👉 Reuse previous computations  
👉 Move (slide) the window efficiently

---

# 🎯 2. When to Use Sliding Window?

Use this technique when:

- Problem involves **contiguous elements**
- You see words like:
  - "subarray"
  - "substring"
  - "window"
  - "longest"
  - "smallest"
- Need **better than O(n²)** solution

---

# 🧠 3. Types of Sliding Window

## ✅ 3.1 Fixed Size Window

- Window size = constant (`k`)
- Example:
  - Maximum sum of subarray of size k

---

## ✅ 3.2 Variable Size Window

- Window size changes dynamically
- Example:
  - Longest substring without repeating characters

---

# 🧩 4. Problem: Maximum Sum Subarray of Size K

---

## 📌 Problem Statement

Given an array of integers and a number `k`, find the **maximum sum of any contiguous subarray of size `k`**.

---

## 🧾 Example

Input:
arr = [2, 1, 7, 6, 9, 8, 2, 1, 3]
k = 4

Output:
30


---

# 🚫 5. Brute Force Approach

## 💡 Idea

- Generate all subarrays of size `k`
- Calculate sum for each
- Track max

---

## 🧮 Code

```javascript
function maxSubArrayBrute(arr, k) {
  let maxSum = -Infinity;

  for (let i = 0; i <= arr.length - k; i++) {
    let sum = 0;

    for (let j = i; j < i + k; j++) {
      sum += arr[j];
    }

    maxSum = Math.max(maxSum, sum);
  }

  return maxSum;
}
```

Complexity
Time: O(n * k)
Space: O(1)

