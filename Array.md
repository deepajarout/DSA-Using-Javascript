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
 //using  Spread Opeartpr
let arr = [1,2,3,4];

let reversed = [...arr].reverse();

console.log(reversed); // [4,3,2,1]
console.log(arr); // [1,2,3,4]

//Using slice()
 let arr = [1,2,3,4];

let reversed = arr.slice().reverse();

console.log(reversed); // [4,3,2,1]
console.log(arr); // [1,2,3,4]

//----------------------------------
function reverseArray(arr) {
  let result = [];

  for (let i = arr.length - 1; i >= 0; i--) {
    result.push(arr[i]);
  }

  return result;
}

let original = [1, 2, 3, 4];
let reversed = reverseArray(original);

console.log(reversed); // [4,3,2,1]
console.log(original); // [1,2,3,4] ✅ unchanged```

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

### ⚡ Complexity:

* Time: **O(n)** ✅
* Space: **O(1)** ✅

---

### ❗ Key Insight:

* XOR helps eliminate duplicates efficiently
* No extra space needed (better than hashmap)

---

## 🧠 Key Learnings (DAY 2)

* Array traversal using loops
* Conditional logic inside loops
* Optimizing without sorting
* Using **bit manipulation (XOR)** for advanced problems

---

## 🚀 Next (DAY 3 Preview)



---

