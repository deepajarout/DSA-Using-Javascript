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
