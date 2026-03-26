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
