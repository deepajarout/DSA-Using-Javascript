# 🔍 Binary Search (Interview Notes)

## 📌 Definition

Binary Search is an efficient algorithm to search an element in a **sorted array** by repeatedly dividing the search space into half.

---

## ⚙️ Key Idea

* Find **middle element**
* Compare with target:

  * Equal → return index
  * Target > mid → search right half
  * Target < mid → search left half

---

## 💻 Code (JavaScript)

```js
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

---

## ⏱ Complexity

* Time: **O(log n)**
* Space: **O(1)**

---

## ⚠️ Important Points

* Array must be **sorted**
* Faster than linear search (**O(n)**)

---

# 📘 Binary Search Patterns (Interview Notes)

---

# 🔥 Problem 2: First Occurrence

## 🧠 Problem

Find the **first index** of a target element in a sorted array.

### Example:

```js
[4, 8, 9, 10, 10, 12, 18], target = 10 → 3
```

---

## ❗ Why Normal Binary Search Fails?

```js
if (arr[mid] === target) return mid;
```

👉 This returns **any occurrence**, not guaranteed first.

Example:

```js
[4, 8, 10, 10, 10, 12, 18]
```

* May return index **3**
* But correct answer is **2**

---

## ✅ Correct Approach (Key Idea)

👉 When found:

* **Store index**
* Move **LEFT** to check earlier occurrence

---

## 💻 Code

```js
function firstOccurrence(arr, target) {
  let left = 0;
  let right = arr.length - 1;
  let result = -1;

  while (left <= right) {
    let mid = Math.floor((left + right) / 2);

    if (arr[mid] === target) {
      result = mid;     // store answer
      right = mid - 1;  // move LEFT
    } else if (arr[mid] < target) {
      left = mid + 1;
    } else {
      right = mid - 1;
    }
  }

  return result;
}
```

---

## 🔍 Why We Store `result`?

👉 Because:

* We **continue searching**
* Pointers move and may **skip correct index**

Without storing:

* You might **lose the answer**

---

## 🎯 Key Rule

| Situation                  | Action      |
| -------------------------- | ----------- |
| Found target               | Store index |
| Searching first occurrence | Move LEFT   |

---

## ⏱️ Complexity

* Time: **O(log n)**
* Space: **O(1)**

---

---

# 🔥 Problem 3: Count 1s in Sorted Array

## 🧠 Problem

Count number of `1`s in a sorted binary array.

### Example:

```js
[0, 0, 0, 1, 1, 1] → 3
```

---

## 🧠 Key Idea

👉 Since array is sorted:

* First find **first occurrence of 1**
* Then:

```js
count = arr.length - firstIndex
```

---

## 💻 Code

```js
function countOnes(arr) {
  let left = 0;
  let right = arr.length - 1;
  let firstOneIndex = -1;

  while (left <= right) {
    let mid = Math.floor((left + right) / 2);

    if (arr[mid] === 1) {
      firstOneIndex = mid;
      right = mid - 1;  // move LEFT
    } else {
      left = mid + 1;   // skip 0s
    }
  }

  if (firstOneIndex === -1) return 0;

  return arr.length - firstOneIndex;
}
```

---

## ✅ Example

```js
countOnes([0,0,0,1,1,1]) → 3
```

---

## 🔍 Dry Run

```js
[0, 0, 0, 1, 1, 1]
         ↑
     first 1 at index 3
```

```js
count = 6 - 3 = 3
```

---

## ❗ Edge Cases

```js
countOnes([0,0,0]) → 0
countOnes([1,1,1]) → 3
countOnes([]) → 0
```

---

## ⏱️ Complexity

* Time: **O(log n)**
* Space: **O(1)**

---

---

# 🚀 Binary Search Pattern Summary

## 🔥 Golden Rules

| Problem          | Trick                   |
| ---------------- | ----------------------- |
| First Occurrence | Store + move LEFT       |
| Last Occurrence  | Store + move RIGHT      |
| Count 1s         | Find first 1 → subtract |

---

## 🧠 Interview One-Liner

> “Whenever duplicates are involved, we don’t return immediately — we store the result and continue searching in the required direction.”

---

## 💡 Final Tip

👉 Binary Search is not just about finding element
👉 It’s about **controlling direction after finding**

---
# 📘 Binary Search — Last Occurrence

---

## 📌 Problem

Find the **last occurrence** of a given `target` in a **sorted array**.

---

## 🧠 Approach

- Use **Binary Search**
- Initialize:
  - `left = 0`
  - `right = n - 1`
  - `result = -1`
- While `left <= right`:
  - Find `mid`
  - If `arr[mid] === target`:
    - Store index in `result`
    - Move **right** (`left = mid + 1`) to find later occurrence
  - If `arr[mid] < target`:
    - Move right
  - Else:
    - Move left

---

## 💻 Code (JavaScript)

```js
function lastOccurrence(arr, target) {
  let left = 0, right = arr.length - 1;
  let result = -1;

  while (left <= right) {
    let mid = left + Math.floor((right - left) / 2);

    if (arr[mid] === target) {
      result = mid;
      left = mid + 1; // move right
    } else if (arr[mid] < target) {
      left = mid + 1;
    } else {
      right = mid - 1;
    }
  }

  return result;
}



