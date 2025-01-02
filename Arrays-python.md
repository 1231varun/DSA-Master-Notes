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

#### Prototypes (Python Examples):
```python
# Declaration
arr = [1, 2, 3, 4, 5]

# Accessing Elements
print(arr[2])  # Output: 3

# Updating Elements
arr[2] = 10
print(arr)  # Output: [1, 2, 10, 4, 5]

# Adding Elements
arr.append(6)  # Adding to the end
print(arr)  # Output: [1, 2, 10, 4, 5, 6]

# Removing Elements
arr.remove(10)  # Remove by value
print(arr)  # Output: [1, 2, 4, 5, 6]

# Traversal
for num in arr:
    print(num)

# Searching for an Element
if 4 in arr:
    print("4 is in the array")
```

---

## Detailed Array Algorithms and Techniques

### Prefix Sum Technique
The **Prefix Sum** technique is used for efficient range queries. It involves precomputing cumulative sums for subarray sum calculations.

#### Example: Sum of Elements in a Range
```python
def prefix_sum(arr):
    prefix = [0] * (len(arr) + 1)
    for i in range(len(arr)):
        prefix[i + 1] = prefix[i] + arr[i]
    return prefix

# Query sum from index l to r
arr = [1, 2, 3, 4, 5]
prefix = prefix_sum(arr)
l, r = 1, 3
print(prefix[r + 1] - prefix[l])  # Output: 9 (2 + 3 + 4)
```

---

### Kadane's Algorithm
Kadane's Algorithm is used to find the **maximum sum subarray** in an array.

#### Time Complexity:
- O(n)

#### Code Example:
```python
def max_subarray_sum(arr):
    max_ending_here = max_so_far = arr[0]
    for x in arr[1:]:
        max_ending_here = max(x, max_ending_here + x)
        max_so_far = max(max_so_far, max_ending_here)
    return max_so_far

# Example Usage
arr = [-2, 1, -3, 4, -1, 2, 1, -5, 4]
print(max_subarray_sum(arr))  # Output: 6 (subarray: [4, -1, 2, 1])
```

---

### Two Pointers Technique
The Two Pointers technique is used for problems involving sorted arrays, subarrays, or pairs of numbers that meet certain conditions.

#### Example: Find Two Numbers that Sum to Target
```python
def two_sum(arr, target):
    arr.sort()  # Ensure the array is sorted
    left, right = 0, len(arr) - 1

    while left < right:
        current_sum = arr[left] + arr[right]
        if current_sum == target:
            return (arr[left], arr[right])
        elif current_sum < target:
            left += 1
        else:
            right -= 1
    return None

# Example Usage
arr = [10, 2, 3, 7, 5]
target = 12
print(two_sum(arr, target))  # Output: (5, 7)
```

---

## Advanced Array Techniques

### Sliding Window Technique
The Sliding Window technique is used to solve problems involving subarrays, such as finding the maximum or minimum sum of a subarray of fixed size.

#### Example: Maximum Sum of Subarray of Size K
```python
def max_sum_subarray(arr, k):
    if len(arr) < k:
        return -1

    max_sum = sum(arr[:k])
    window_sum = max_sum

    for i in range(len(arr) - k):
        window_sum = window_sum - arr[i] + arr[i + k]
        max_sum = max(max_sum, window_sum)

    return max_sum

# Example Usage
arr = [2, 1, 5, 1, 3, 2]
k = 3
print(max_sum_subarray(arr, k))  # Output: 9
```

#### Example: Longest Substring with K Unique Characters
```python
def longest_substring_k_unique(s, k):
    char_count = {}
    max_length = start = 0

    for end in range(len(s)):
        char_count[s[end]] = char_count.get(s[end], 0) + 1

        while len(char_count) > k:
            char_count[s[start]] -= 1
            if char_count[s[start]] == 0:
                del char_count[s[start]]
            start += 1

        max_length = max(max_length, end - start + 1)

    return max_length

# Example Usage
s = "eceba"
k = 2
print(longest_substring_k_unique(s, k))  # Output: 3 (substring: "ece")
```

---

### Sorting Algorithms

#### QuickSort
QuickSort is a **divide-and-conquer** algorithm that partitions an array into two halves and recursively sorts them.

#### Time Complexity:
- **Best/Average Case**: O(nlog n)
- **Worst Case**: O(n^2) (occurs when the pivot is poorly chosen)

#### Code Example:
```python
def quicksort(arr):
    if len(arr) <= 1:
        return arr
    pivot = arr[len(arr) // 2]
    left = [x for x in arr if x < pivot]
    middle = [x for x in arr if x == pivot]
    right = [x for x in arr if x > pivot]
    return quicksort(left) + middle + quicksort(right)

# Example Usage
arr = [3, 6, 8, 10, 1, 2, 1]
print(quicksort(arr))  # Output: [1, 1, 2, 3, 6, 8, 10]
```

---

### MergeSort
MergeSort is a stable sorting algorithm that repeatedly divides the array into halves, sorts them, and merges them back.

#### Time Complexity:
- **Best/Average/Worst Case**: O(nlog n)

#### Code Example:
```python
def mergesort(arr):
    if len(arr) <= 1:
        return arr
    mid = len(arr) // 2
    left = mergesort(arr[:mid])
    right = mergesort(arr[mid:])

    return merge(left, right)

def merge(left, right):
    result = []
    i = j = 0
    while i < len(left) and j < len(right):
        if left[i] < right[j]:
            result.append(left[i])
            i += 1
        else:
            result.append(right[j])
            j += 1

    result.extend(left[i:])
    result.extend(right[j:])
    return result

# Example Usage
arr = [3, 6, 8, 10, 1, 2, 1]
print(mergesort(arr))  # Output: [1, 1, 2, 3, 6, 8, 10]
```

---

### Searching Algorithms

#### Binary Search
Binary Search is an efficient algorithm for finding an item in a sorted array by repeatedly dividing the search interval in half.

#### Time Complexity:
- **Best Case**: O(1)
- **Worst/Average Case**: O(log n)

#### Code Example:
```python
def binary_search(arr, target):
    low, high = 0, len(arr) - 1
    while low <= high:
        mid = (low + high) // 2
        if arr[mid] == target:
            return mid
        elif arr[mid] < target:
            low = mid + 1
        else:
            high = mid - 1
    return -1

# Example Usage
arr = [1, 2, 3, 4, 5, 6, 7, 8, 9]
print(binary_search(arr, 5))  # Output: 4
```

---

## Recommended LeetCode Problems (Arrays)

To solidify your understanding of arrays, try solving these problems on [LeetCode](https://leetcode.com/):

### Easy Level:
1. [Two Sum](https://leetcode.com/problems/two-sum/)
2. [Best Time to Buy and Sell Stock](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/)
3. [Maximum Subarray](https://leetcode.com/problems/maximum-subarray/)
4. [Contains Duplicate](https://leetcode.com/problems/contains-duplicate/)
5. [Move Zeroes](https://leetcode.com/problems/move-zeroes/)

### Medium Level:
1. [3Sum](https://leetcode.com/problems/3sum/)
2. [Product of Array Except Self](https://leetcode.com/problems/product-of-array-except-self/)
3. [Maximum Product Subarray](https://leetcode.com/problems/maximum-product-subarray/)
4. [Find Minimum in Rotated Sorted Array](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/)
5. [Subarray Sum Equals K](https://leetcode.com/problems/subarray-sum-equals-k/)

### Hard Level:
1. [Trapping Rain Water](https://leetcode.com/problems/trapping-rain-water/)
2. [First Missing Positive](https://leetcode.com/problems/first-missing-positive/)
3. [Longest Consecutive Sequence](https://leetcode.com/problems/longest-consecutive-sequence/)
4. [Merge Intervals](https://leetcode.com/problems/merge-intervals/)
5. [Median of Two Sorted Arrays](https://leetcode.com/problems/median-of-two-sorted-arrays/)

---

## Additional Algorithms to Know

### Dutch National Flag Algorithm
This algorithm is used to sort an array with three distinct types of elements efficiently (e.g., 0s, 1s, and 2s).

#### Code Example:
```python
def dutch_national_flag(arr):
    low, mid, high = 0, 0, len(arr) - 1
    while mid <= high:
        if arr[mid] == 0:
            arr[low], arr[mid] = arr[mid], arr[low]
            low += 1
            mid += 1
        elif arr[mid] == 1:
            mid += 1
        else:
            arr[mid], arr[high] = arr[high], arr[mid]
            high -= 1

# Example Usage
arr = [2, 0, 2, 1, 1, 0]
dutch_national_flag(arr)
print(arr)  # Output: [0, 0, 1, 1, 2, 2]
```

---

## Summary
This guide provides an in-depth explanation of arrays, advanced algorithms, LeetCode problem recommendations, and additional techniques. Use the code examples to practice and solidify your understanding. Happy coding!
