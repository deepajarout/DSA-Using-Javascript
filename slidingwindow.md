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
---

# 📘 Maximum Sum Subarray of Size K (Sliding Window)

---

## 📌 Function

```javascript
function maxSubArray(arr, k) {
  if (arr.length < k) return null;

  let windowSum = 0;
  let maxSum = 0;

  // Step 1: First window
  for (let i = 0; i < k; i++) {
    windowSum += arr[i];
  }

  maxSum = windowSum;

  // Step 2: Slide window
  for (let i = k; i < arr.length; i++) {
    windowSum += arr[i];
    windowSum -= arr[i - k];

    maxSum = Math.max(maxSum, windowSum);
  }

  return maxSum;
}
```
---
# 🧩 Longest Substring Without Repeating Characters (Medium)

## 📌 Problem Statement

Given a string `s`, find the **length of the longest substring** without repeating characters.

---

## 🧠 Approach: Sliding Window (Optimal)

### 💡 Idea

- Use a **sliding window (left → right)**
- Maintain a **Set / Map** to track characters
- If duplicate found → **shrink window**
- Track **maximum length**

---

## 🚀 Solution 1: Using Set

### 💻 Code

```javascript
function longestSubstring(s) {
  let set = new Set();
  let left = 0;
  let maxLength = 0;

  for (let right = 0; right < s.length; right++) {

    // Remove duplicates
    while (set.has(s[right])) {
      set.delete(s[left]);
      left++;
    }

    set.add(s[right]);
    maxLength = Math.max(maxLength, right - left + 1);
  }

  return maxLength;
}
```

# 🧩 Longest Substring Without Repeating Characters (Using Map)

## 📌 Problem Statement

Given a string `s`, find the **length of the longest substring without repeating characters**.

---

## 🧠 Approach: Sliding Window + HashMap

### 💡 Idea

- Use a **sliding window (left → right)**
- Use a **Map** to store:
  - Character → Last seen index
- If duplicate found:
  - Move `left` pointer directly to **last index + 1**
- Update max length

---

## 🚀 Optimized Solution (Map)

### 💻 Code

```javascript
function longestSubstring(s) {
  let map = new Map(); // char -> last index
  let left = 0;
  let maxLength = 0;

  for (let right = 0; right < s.length; right++) {

    // If character already seen
    if (map.has(s[right])) {
      // Move left pointer
      left = Math.max(map.get(s[right]) + 1, left);
    }

    // Update last seen index
    map.set(s[right], right);

    // Calculate max length
    maxLength = Math.max(maxLength, right - left + 1);
  }

  return maxLength;
}
```

