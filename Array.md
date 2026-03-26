# 📘 DAY 1 — Array Basics

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

## 💻 Code (JavaScript)

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

### 1. Loop

* Used a **for loop** to iterate through the array

### 2. Comparison

* Compared each element with the current maximum

### 3. Logic Building

* Start with first element as `max`
* Update `max` when a bigger value is found

---

## ✅ Summary

* Arrays store multiple values in one variable
* Loop helps traverse elements
* Comparison helps identify required values
* This pattern is very common in DSA problems 🚀

---

## 🧪 Practice Task

Try solving this on your own:

👉 Find the **minimum number** in an array

## 💻 Code (JavaScript)

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

Reverse the elements of an array **in-place**.

---

## 💻 Code (JavaScript)

```javascript
//---using for loop-----
function reverseArray(arr) {
  for (let i = 0; i < arr.length / 2; i++) {
    let temp = arr[i];
    arr[i] = arr[arr.length - 1 - i];
    arr[arr.length - 1 - i] = temp;
  }

  return arr;
}

//-------------------------
function reverseArray(arr) {
  let left = 0;
  let right = arr.length - 1;

  while (left < right) {
    let temp = arr[left];
    arr[left] = arr[right];
    arr[right] = temp;

    left++;
    right--;
  }

  //-----without temp ------
  left = 0;
  right = arr.length - 1;

  while (left < right) {
    [arr[left], arr[right]] = [arr[right], arr[left]];
    left++;
    right--;
  }

  return arr;
}

console.log(reverseArray([1,2,3,4])); // [4,3,2,1]
```

---

## 🎯 Key Learnings

### 1. Two Pointer Technique

* Used `left` and `right` pointers to swap elements

### 2. In-place Modification

* No extra space used (efficient memory usage)

### 3. Swapping Logic

* Used a temporary variable to swap values

---

## 🧪 Practice Task

👉 Reverse an array **without modifying original array**

## 💻 Code (JavaScript)

```javascript
//-----using inbuilt method ---------
// using Spread Operator
let arr = [1,2,3,4];

let reversed = [...arr].reverse();

console.log(reversed); // [4,3,2,1]
console.log(arr); // [1,2,3,4]

// Using slice()
let arr2 = [1,2,3,4];

let reversed2 = arr2.slice().reverse();

console.log(reversed2); // [4,3,2,1]
console.log(arr2); // [1,2,3,4]

//----------------------------------
function reverseArray(arr) {
  let result = [];

  for (let i = arr.length - 1; i >= 0; i--) {
    result.push(arr[i]);
  }

  return result;
}

let original = [1, 2, 3, 4];
let reversed3 = reverseArray(original);

console.log(reversed3); // [4,3,2,1]
console.log(original); // [1,2,3,4] ✅ unchanged
```

---

💡 This is a very important pattern for interviews 🚀

---

# 📘 DAY 2 — Array Practice (Basics + Logic Building)

## 🔥 Problem 1: Find Element

### 🧠 Question:

Find the **index** of a target element in an array.

---

### 💻 Code (JavaScript)

```javascript
function findElement(arr, target) {
  for (let i = 0; i < arr.length; i++) {
    if (arr[i] === target) {
      return i; // index
    }
  }
  return -1;
}

console.log(findElement([1,2,3,4,5], 3)); // 2
```

---

### ⚡ Complexity:

* Time: **O(n)**
* Space: **O(1)**

---

## 🔥 Problem 2: Count Occurrences

### 🧠 Question:

Count how many times a target appears in an array.

---

### 💻 Code (JavaScript)

```javascript
function countOccurrences(arr, target) {
  let count = 0;

  for (let num of arr) {
    if (num === target) {
      count++;
    }
  }

  return count;
}

console.log(countOccurrences([1,2,2,3,2], 2)); // 3
```

---

### ⚡ Complexity:

* Time: **O(n)**
* Space: **O(1)**

---

## 🔥 Problem 3: Check Sorted Array

### 🧠 Question:

Check if an array is sorted in **ascending order**.

---

### 💻 Code (JavaScript)

```javascript
function isSorted(arr) {
  for (let i = 1; i < arr.length; i++) {
    if (arr[i] < arr[i - 1]) {
      return false;
    }
  }
  return true;
}

console.log(isSorted([1,2,3,4])); // true
console.log(isSorted([1,3,2]));   // false
```

---

### ⚡ Complexity:

* Time: **O(n)**
* Space: **O(1)**

---

## 🧪 BONUS Problem: Second Largest Element ⭐⭐⭐

### 🧠 Question:

Find the **second largest element** in an array
👉 **Constraint:** Do NOT sort

---

### 💻 Code (JavaScript)

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

console.log(findSecondLargest([3, 7, 2, 9, 5])); // 7
```

---

### ⚡ Complexity:

* Time: **O(n)**
* Space: **O(1)**

---

## 🔥 LeetCode Problem: Single Number ⭐⭐⭐

### 🧠 Question:

Given a non-empty array of integers, every element appears **twice except one**.
Find that single one.

---

### 💡 Approach:

Use **XOR (^)** property:

* `a ^ a = 0`
* `a ^ 0 = a`

👉 All duplicates cancel out, leaving the unique number.

---

### 💻 Code (JavaScript)

```javascript
var singleNumber = function(nums) {
    var ans = 0;

    for(var i = 0; i < nums.length; i++){
        ans = ans ^ nums[i];
    }

    return ans;
};

console.log(singleNumber([4,1,2,1,2])); // 4
```

---


## 🚀 Next (DAY 3 )

---

## 🔥 Problem 1: Two Sum (Brute Force)

### 💡 Approach:

* Check every pair using nested loops
* Return indices when sum matches target

### 💻 Code:

```js
function twoSum(arr, target) {
  for (let i = 0; i < arr.length; i++) {
    for (let j = i + 1; j < arr.length; j++) {
      if (arr[i] + arr[j] === target) {
        return [i, j];
      }
    }
  }
}
```

### ⏱ Time Complexity:

* O(n²)

### 📦 Space Complexity:

* O(1)

---

## 🚀 Problem 1: Two Sum (Optimized - Hash Map)

### 💡 Approach:

* Store visited elements in a map
* Check if complement exists

### 💻 Code:

```js
function twoSum(arr, target) {
  let map = {};

  for (let i = 0; i < arr.length; i++) {
    let complement = target - arr[i];

    if (map[complement] !== undefined) {
      return [map[complement], i];
    }

    map[arr[i]] = i;
  }
}
```

### ⏱ Time Complexity:

* O(n)

### 📦 Space Complexity:

* O(n)

---

## 🔥 Problem 2: Move Zeros

### 💡 Approach:

* Use two pointers
* Swap non-zero elements forward

### 💻 Code:

```js
function moveZeros(arr) {
  let j = 0;

  for (let i = 0; i < arr.length; i++) {
    if (arr[i] !== 0) {
      if (i !== j) {
        [arr[i], arr[j]] = [arr[j], arr[i]];
      }
      j++;
    }
  }

  return arr;
}
```

### ⏱ Time Complexity:

* O(n)

### 📦 Space Complexity:

* O(1)

---

## 🔥 Problem 3: Remove Duplicates (Using Object)

### 💡 Approach:

* Use object as hashmap
* Store visited values

### 💻 Code:

```js
function removeDuplicates(arr) {
  let map = {};
  let result = [];

  for (let i = 0; i < arr.length; i++) {
    if (!map[arr[i]]) {
      map[arr[i]] = true;
      result.push(arr[i]);
    }
  }

  return result;
}
```

### ⏱ Time Complexity:

* O(n)

### 📦 Space Complexity:

* O(n)

---

## 🚀 Problem 3: Remove Duplicates (Using Set)

### 💡 Approach:

* Use Set to track unique values

### 💻 Code:

```js
function removeDuplicates(arr) {
  let seen = new Set();
  let result = [];

  for (let num of arr) {
    if (!seen.has(num)) {
      seen.add(num);
      result.push(num);
    }
  }

  return result;
}
```

### ⏱ Time Complexity:

* O(n)

### 📦 Space Complexity:

* O(n)

---
