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
---
# 🌟 Longest Substring with At Most K Distinct Characters (Detailed Code)

---

## 📌 Problem Statement

Given a string `s` and an integer `k`, return the **length of the longest substring** that contains **at most `k` distinct characters**.

---

## 🧠 Approach: Sliding Window

We maintain a window `[left, right]` and ensure:
👉 At any time → **window contains ≤ k distinct characters**

---

## ✅ Fully Explained Code

```javascript
function longestKDistinct(s, k) {

  // Map to store frequency of characters in current window
  let map = new Map();

  // Left pointer (start of window)
  let left = 0;

  // Store maximum length found
  let maxLen = 0;

  // Right pointer expands the window
  for (let right = 0; right < s.length; right++) {

    let char = s[right]; // current character

    // Step 1: Add current character to map
    // If already exists → increase count
    // Else → initialize with 1
    map.set(char, (map.get(char) || 0) + 1);

    // Step 2: Check if window is invalid
    // Invalid condition → more than k distinct characters
    while (map.size > k) {

      // Character at left pointer
      let leftChar = s[left];

      // Reduce its frequency
      map.set(leftChar, map.get(leftChar) - 1);

      // If frequency becomes 0 → remove from map
      if (map.get(leftChar) === 0) {
        map.delete(leftChar);
      }

      // Move left pointer to shrink window
      left++;
    }

    // Step 3: Calculate current valid window size
    let windowSize = right - left + 1;

    // Step 4: Update maximum length
    maxLen = Math.max(maxLen, windowSize);
  }

  // Return final result
  return maxLen;
}
```
---

---

## 🧠 Intuition

We need to find the **longest substring** with **at most `k` distinct characters**.

- Expand the window to include more characters
- If the number of distinct characters exceeds `k`, shrink the window
- Track the maximum valid window size

---

## 🚀 Approach: Sliding Window + HashMap

We use:
- Two pointers: `left` and `right`
- A `Map` to store character frequency

---

## 🔄 Algorithm Steps

1. Initialize:
   - `left = 0`
   - `maxLength = 0`
   - `map = new Map()`

2. Iterate with `right` pointer:
   - Add character to map
   - If `map.size > k`:
     - Shrink window from left
     - Decrease frequency
     - Remove character if frequency becomes 0

3. Update `maxLength`

4. Return result

---

## 🪜 Dry Run

Input: `s = "eceba"`, `k = 2`

| Step | Window | Map | Action | Max |
|------|--------|-----|--------|-----|
| e    | e      | {e:1} | expand | 1 |
| c    | ec     | {e:1,c:1} | expand | 2 |
| e    | ece    | {e:2,c:1} | expand | 3 |
| b    | eceb   | {e:2,c:1,b:1} | shrink | 3 |
| a    | ba     | {b:1,a:1} | shrink | 3 |

---

## ✅ JavaScript Implementation

```javascript
function longestSubstringKDistinct(s, k) {
  let map = new Map();
  let left = 0;
  let maxLength = 0;

  for (let right = 0; right < s.length; right++) {
    let char = s[right];

    // Add character to map
    map.set(char, (map.get(char) || 0) + 1);

    // Shrink window if condition breaks
    while (map.size > k) {
      let leftChar = s[left];
      map.set(leftChar, map.get(leftChar) - 1);

      if (map.get(leftChar) === 0) {
        map.delete(leftChar);
      }

      left++;
    }

    // Update max length
    maxLength = Math.max(maxLength, right - left + 1);
  }

  return maxLength;
}
```

