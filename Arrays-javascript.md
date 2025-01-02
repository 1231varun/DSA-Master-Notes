# Arrays - The Ultimate DSA Guide Notes

## Overview of Arrays

### What are Arrays?
An **array** is a collection of items stored at contiguous memory locations. It is the simplest data structure that allows the storage and manipulation of a fixed-size collection of elements of the same type.

### Key Features:
1. **Fixed Size**: The size of the array is defined at the time of declaration.
2. **Random Access**: Elements can be accessed directly via their index.
3. **Homogeneous Elements**: All elements in an array are of the same type.
4. **Efficient Memory Allocation**: Elements are stored in adjacent memory locations, ensuring efficient storage and retrieval.

### Functions and Operations:

#### Common Operations
| Operation          | Description                                |
|--------------------|--------------------------------------------|
| Traversal          | Accessing each element sequentially.      |
| Insertion          | Adding an element at a specified index.   |
| Deletion           | Removing an element from a specified index.|
| Search             | Finding an element (linear/binary search).|
| Update             | Changing the value of an element.         |

#### Prototypes (JavaScript Examples):
```javascript
// Declaration
let arr = [1, 2, 3, 4, 5];

// Accessing Elements
console.log(arr[2]); // Output: 3

// Updating Elements
arr[2] = 10;
console.log(arr); // Output: [1, 2, 10, 4, 5]

// Adding Elements
arr.push(6); // Adding to the end
console.log(arr); // Output: [1, 2, 10, 4, 5, 6]

// Removing Elements
arr.splice(arr.indexOf(10), 1); // Remove by value
console.log(arr); // Output: [1, 2, 4, 5, 6]

// Traversal
arr.forEach(num => console.log(num));

// Searching for an Element
if (arr.includes(4)) {
    console.log("4 is in the array");
}
```

---

## Detailed Array Algorithms and Techniques

### Prefix Sum Technique
The **Prefix Sum** technique is used for efficient range queries. It involves precomputing cumulative sums for subarray sum calculations.

#### Example: Sum of Elements in a Range
```javascript
function prefixSum(arr) {
    let prefix = Array(arr.length + 1).fill(0);
    for (let i = 0; i < arr.length; i++) {
        prefix[i + 1] = prefix[i] + arr[i];
    }
    return prefix;
}

// Query sum from index l to r
let arr = [1, 2, 3, 4, 5];
let prefix = prefixSum(arr);
let l = 1, r = 3;
console.log(prefix[r + 1] - prefix[l]); // Output: 9 (2 + 3 + 4)
```

---

### Kadane's Algorithm
Kadane's Algorithm is used to find the **maximum sum subarray** in an array.

#### Time Complexity:
- O(n)

#### Code Example:
```javascript
function maxSubarraySum(arr) {
    let maxEndingHere = arr[0], maxSoFar = arr[0];
    for (let i = 1; i < arr.length; i++) {
        maxEndingHere = Math.max(arr[i], maxEndingHere + arr[i]);
        maxSoFar = Math.max(maxSoFar, maxEndingHere);
    }
    return maxSoFar;
}

// Example Usage
let arr = [-2, 1, -3, 4, -1, 2, 1, -5, 4];
console.log(maxSubarraySum(arr)); // Output: 6 (subarray: [4, -1, 2, 1])
```

---

### Two Pointers Technique
The Two Pointers technique is used for problems involving sorted arrays, subarrays, or pairs of numbers that meet certain conditions.

#### Example: Find Two Numbers that Sum to Target
```javascript
function twoSum(arr, target) {
    arr.sort((a, b) => a - b); // Ensure the array is sorted
    let left = 0, right = arr.length - 1;

    while (left < right) {
        let currentSum = arr[left] + arr[right];
        if (currentSum === target) {
            return [arr[left], arr[right]];
        } else if (currentSum < target) {
            left++;
        } else {
            right--;
        }
    }
    return null;
}

// Example Usage
let arr = [10, 2, 3, 7, 5];
let target = 12;
console.log(twoSum(arr, target)); // Output: [5, 7]
```

---

## Advanced Array Techniques

### Sliding Window Technique
The Sliding Window technique is used to solve problems involving subarrays, such as finding the maximum or minimum sum of a subarray of fixed size.

#### Example: Maximum Sum of Subarray of Size K
```javascript
function maxSumSubarray(arr, k) {
    if (arr.length < k) return -1;

    let maxSum = 0, windowSum = 0;
    for (let i = 0; i < k; i++) {
        windowSum += arr[i];
    }
    maxSum = windowSum;

    for (let i = k; i < arr.length; i++) {
        windowSum += arr[i] - arr[i - k];
        maxSum = Math.max(maxSum, windowSum);
    }

    return maxSum;
}

// Example Usage
let arr = [2, 1, 5, 1, 3, 2];
let k = 3;
console.log(maxSumSubarray(arr, k)); // Output: 9
```

#### Example: Longest Substring with K Unique Characters
```javascript
function longestSubstringKUnique(s, k) {
    let charCount = new Map();
    let maxLength = 0, start = 0;

    for (let end = 0; end < s.length; end++) {
        charCount.set(s[end], (charCount.get(s[end]) || 0) + 1);

        while (charCount.size > k) {
            charCount.set(s[start], charCount.get(s[start]) - 1);
            if (charCount.get(s[start]) === 0) {
                charCount.delete(s[start]);
            }
            start++;
        }

        maxLength = Math.max(maxLength, end - start + 1);
    }

    return maxLength;
}

// Example Usage
let s = "eceba";
let k = 2;
console.log(longestSubstringKUnique(s, k)); // Output: 3 (substring: "ece")
```

---

### Sorting Algorithms

#### QuickSort
QuickSort is a **divide-and-conquer** algorithm that partitions an array into two halves and recursively sorts them.

#### Time Complexity:
- **Best/Average Case**: O(nlog n)
- **Worst Case**: O(n^2) (occurs when the pivot is poorly chosen)

#### Code Example:
```javascript
function quicksort(arr) {
    if (arr.length <= 1) return arr;
    let pivot = arr[Math.floor(arr.length / 2)];
    let left = arr.filter(x => x < pivot);
    let middle = arr.filter(x => x === pivot);
    let right = arr.filter(x => x > pivot);
    return [...quicksort(left), ...middle, ...quicksort(right)];
}

// Example Usage
let arr = [3, 6, 8, 10, 1, 2, 1];
console.log(quicksort(arr)); // Output: [1, 1, 2, 3, 6, 8, 10]
```

---

### Searching Algorithms

#### Binary Search
Binary Search is an efficient algorithm for finding an item in a sorted array by repeatedly dividing the search interval in half.

#### Time Complexity:
- **Best Case**: O(1)
- **Worst/Average Case**: O(log n)

#### Code Example:
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

// Example Usage
let arr = [1, 2, 3, 4, 5, 6, 7, 8, 9];
console.log(binarySearch(arr, 5)); // Output: 4
```

---

## Summary
This guide provides an in-depth explanation of arrays, advanced algorithms, and associated techniques in JavaScript. Use the code examples to practice and solidify your understanding. Happy coding!
