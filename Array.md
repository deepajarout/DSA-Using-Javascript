# 📘 DAY 1 — Array Basics

---

## 📌 What is an Array?

An **array** is a collection of elements stored in **continuous memory locations**.

### Example:

```js
[1, 2, 3, 4, 5]
```

---

## 🔥 Problem 1: Find Maximum Number

### 🧠 Question:

Find the **largest number** in an array.

---

### 💻 Code (JavaScript)

```javascript
function findMax(arr) {
  let max = arr[0];

  for (let i = 1; i < arr.length; i++) {
    if (arr[i] > max) {
      max = arr[i];
    }
  }

  return max;
}

console.log(findMax([3, 7, 2, 9, 5])); // 9
```

---

## 🎯 Key Learnings

* Used a **for loop** to iterate
* Compared each element with current max
* Updated max dynamically

---

## 🧪 Practice Task

👉 Find the **minimum number** in an array

```javascript
function findMin(arr) {
  let min = arr[0];

  for (let i = 1; i < arr.length; i++) {
    if (arr[i] < min) {
      min = arr[i];
    }
  }

  return min;
}

console.log(findMin([3, 7, 2, 9, 5])); // 2
```

---

## 🔥 Problem 2: Reverse Array

### 🧠 Question:

Reverse the array **in-place**

---

### 💻 Code (JavaScript)

### 👉 Using for loop

```javascript
function reverseArray(arr) {
  for (let i = 0; i < arr.length / 2; i++) {
    let temp = arr[i];
    arr[i] = arr[arr.length - 1 - i];
    arr[arr.length - 1 - i] = temp;
  }
  return arr;
}
```

---

### 👉 Using Two Pointer

```javascript
function reverseArray(arr) {
  let left = 0;
  let right = arr.length - 1;

  while (left < right) {
    [arr[left], arr[right]] = [arr[right], arr[left]];
    left++;
    right--;
  }

  return arr;
}
```

---

## 🧪 Reverse Without Modifying Original

```javascript
// Spread
let arr = [1,2,3,4];
let reversed = [...arr].reverse();

// Slice
let reversed2 = arr.slice().reverse();

// Manual
function reverseArray(arr) {
  let result = [];
  for (let i = arr.length - 1; i >= 0; i--) {
    result.push(arr[i]);
  }
  return result;
}
```

---

# 📘 DAY 2 — Array Practice

---

## 🔥 Problem 1: Find Element

```javascript
function findElement(arr, target) {
  for (let i = 0; i < arr.length; i++) {
    if (arr[i] === target) {
      return i;
    }
  }
  return -1;
}
```

---

## 🔥 Problem 2: Count Occurrences

```javascript
function countOccurrences(arr, target) {
  let count = 0;

  for (let num of arr) {
    if (num === target) count++;
  }

  return count;
}
```

---

## 🔥 Problem 3: Check Sorted Array

```javascript
function isSorted(arr) {
  for (let i = 1; i < arr.length; i++) {
    if (arr[i] < arr[i - 1]) return false;
  }
  return true;
}
```

---

## 🧪 BONUS: Second Largest

```javascript
function findSecondLargest(array) {
  var larg = -Infinity;
  var second = -Infinity;

  for (var i = 0; i < array.length; i++) {
    if (array[i] > larg) {
      second = larg;
      larg = array[i];
    } else if (array[i] > second && array[i] !== larg) {
      second = array[i];
    }
  }

  return second === -Infinity ? null : second;
}
```

---

## 🔥 LeetCode: Single Number

```javascript
var singleNumber = function(nums) {
  var ans = 0;

  for (var i = 0; i < nums.length; i++) {
    ans = ans ^ nums[i];
  }

  return ans;
};
```

---

## 🧠 Key Learnings (DAY 2)

* Looping patterns
* Condition-based logic
* Avoid sorting when not needed
* XOR trick (very important)

---

## 🚀 DAY 3 Preview

* Move zeros
* Two pointers
* Sliding window (intro)

---
