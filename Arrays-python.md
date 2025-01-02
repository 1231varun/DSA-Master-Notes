# Lists in Python - The Ultimate DSA Guide Notes

## Overview of Lists

### What are Lists?
A **list** in Python is a dynamic and versatile data structure that allows the storage and manipulation of an ordered collection of elements. Lists in Python can hold elements of **different data types**, making them highly flexible compared to traditional arrays in other languages.

### Key Features:
1. **Dynamic Size**: Lists can grow or shrink as needed.
2. **Random Access**: Elements can be accessed directly via their index.
3. **Heterogeneous Elements**: Lists can store elements of different types (e.g., integers, strings, objects).
4. **Built-in Operations**: Python provides powerful built-in methods for manipulating lists efficiently.
5. **Nested Structures**: Lists can contain other lists, enabling multi-dimensional arrays.

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
#### Creating Lists
```python
# Empty list
empty_list = []

# List with elements
nums = [1, 2, 3, 4, 5]

# List with mixed types
mixed = [1, "hello", 3.14, True]

# Nested list
nested = [[1, 2], [3, 4], [5, 6]]
```

#### Accessing Elements
```python
nums = [10, 20, 30, 40, 50]

# Access by index
print(nums[0])  # Output: 10
print(nums[-1])  # Output: 50 (last element)

# Slicing
print(nums[1:4])  # Output: [20, 30, 40]
```

#### Adding Elements
```python
nums = [1, 2, 3]

# Append an element
nums.append(4)
print(nums)  # Output: [1, 2, 3, 4]

# Insert at a specific index
nums.insert(1, 10)
print(nums)  # Output: [1, 10, 2, 3, 4]

# Extend the list with another list
nums.extend([5, 6, 7])
print(nums)  # Output: [1, 10, 2, 3, 4, 5, 6, 7]
```

#### Removing Elements
```python
nums = [1, 2, 3, 4, 5]

# Remove by value
nums.remove(3)
print(nums)  # Output: [1, 2, 4, 5]

# Remove by index
nums.pop(1)  # Removes element at index 1
print(nums)  # Output: [1, 4, 5]

# Clear the entire list
nums.clear()
print(nums)  # Output: []
```

#### Traversing a List
```python
nums = [10, 20, 30]
for num in nums:
    print(num)

# Enumerate for index and value
for index, value in enumerate(nums):
    print(f"Index: {index}, Value: {value}")
```

#### Searching for an Element
```python
nums = [1, 2, 3, 4, 5]

# Check if an element exists
print(3 in nums)  # Output: True

# Get index of an element
print(nums.index(4))  # Output: 3
```
---

## Detailed List Algorithms and Techniques

### Prefix Sum Technique
The **Prefix Sum** technique is used for efficient range queries. It involves precomputing cumulative sums for subarray sum calculations.

#### Example: Sum of Elements in a Range
```python
def prefix_sum(lst):
    prefix = [0] * (len(lst) + 1)
    for i in range(len(lst)):
        prefix[i + 1] = prefix[i] + lst[i]
    return prefix

# Query sum from index l to r
lst = [1, 2, 3, 4, 5]
prefix = prefix_sum(lst)
l, r = 1, 3
print(prefix[r + 1] - prefix[l])  # Output: 9 (2 + 3 + 4)
```

---

### Kadane's Algorithm
Kadane's Algorithm is used to find the **maximum sum subarray** in a list.

#### Time Complexity:
- O(n)

#### Code Example:
```python
def max_subarray_sum(lst):
    max_ending_here = max_so_far = lst[0]
    for x in lst[1:]:
        max_ending_here = max(x, max_ending_here + x)
        max_so_far = max(max_so_far, max_ending_here)
    return max_so_far

# Example Usage
lst = [-2, 1, -3, 4, -1, 2, 1, -5, 4]
print(max_subarray_sum(lst))  # Output: 6 (subarray: [4, -1, 2, 1])
```

---

### Two Pointers Technique
The Two Pointers technique is useful for solving problems involving sorted lists, subarrays, or pairs of numbers that meet certain conditions.

#### Example: Find Two Numbers that Sum to Target
```python
def two_sum(lst, target):
    lst.sort()  # Ensure the list is sorted
    left, right = 0, len(lst) - 1

    while left < right:
        current_sum = lst[left] + lst[right]
        if current_sum == target:
            return (lst[left], lst[right])
        elif current_sum < target:
            left += 1
        else:
            right -= 1
    return None

# Example Usage
lst = [10, 2, 3, 7, 5]
target = 12
print(two_sum(lst, target))  # Output: (5, 7)
```

---
## Advanced Array Techniques

### Sliding Window Technique
The Sliding Window technique is used to solve problems involving subarrays, such as finding the maximum or minimum sum of a subarray of fixed size.

#### Example: Maximum Sum of Subarray of Size K
```python
def max_sum_subarray(lst, k):
    if len(lst) < k:
        return -1

    max_sum = sum(lst[:k])
    window_sum = max_sum

    for i in range(len(lst) - k):
        window_sum = window_sum - lst[i] + lst[i + k]
        max_sum = max(max_sum, window_sum)

    return max_sum

# Example Usage
lst = [2, 1, 5, 1, 3, 2]
k = 3
print(max_sum_subarray(lst, k))  # Output: 9
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
QuickSort is a **divide-and-conquer** algorithm that partitions a list into two halves and recursively sorts them.

#### Time Complexity:
- **Best/Average Case**: O(nlog n)
- **Worst Case**: O(n^2) (occurs when the pivot is poorly chosen)

#### Code Example:
```python
def quicksort(lst):
    if len(lst) <= 1:
        return lst
    pivot = lst[len(lst) // 2]
    left = [x for x in lst if x < pivot]
    middle = [x for x in lst if x == pivot]
    right = [x for x in lst if x > pivot]
    return quicksort(left) + middle + quicksort(right)

# Example Usage
lst = [3, 6, 8, 10, 1, 2, 1]
print(quicksort(lst))  # Output: [1, 1, 2, 3, 6, 8, 10]
```

---

### MergeSort
MergeSort is a stable sorting algorithm that repeatedly divides the list into halves, sorts them, and merges them back.

#### Time Complexity:
- **Best/Average/Worst Case**: O(nlog n)

#### Code Example:
```python
def mergesort(lst):
    if len(lst) <= 1:
        return lst
    mid = len(lst) // 2
    left = mergesort(lst[:mid])
    right = mergesort(lst[mid:])

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
lst = [3, 6, 8, 10, 1, 2, 1]
print(mergesort(lst))  # Output: [1, 1, 2, 3, 6, 8, 10]
```

---

### Searching Algorithms

#### Binary Search
Binary Search is an efficient algorithm for finding an item in a sorted list by repeatedly dividing the search interval in half.

#### Time Complexity:
- **Best Case**: O(1)
- **Worst/Average Case**: O(log n)

#### Code Example:
```python
def binary_search(lst, target):
    low, high = 0, len(lst) - 1
    while low <= high:
        mid = (low + high) // 2
        if lst[mid] == target:
            return mid
        elif lst[mid] < target:
            low = mid + 1
        else:
            high = mid - 1
    return -1

# Example Usage
lst = [1, 2, 3, 4, 5, 6, 7, 8, 9]
print(binary_search(lst, 5))  # Output: 4
```

---

## Recommended LeetCode Problems (Lists)

To solidify your understanding of lists, try solving these problems on [LeetCode](https://leetcode.com/):

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
This algorithm is used to sort a list with three distinct types of elements efficiently (e.g., 0s, 1s, and 2s).

#### Code Example:
```python
def dutch_national_flag(lst):
    low, mid, high = 0, 0, len(lst) - 1
    while mid <= high:
        if lst[mid] == 0:
            lst[low], lst[mid] = lst[mid], lst[low]
            low += 1
            mid += 1
        elif lst[mid] == 1:
            mid += 1
        else:
            lst[mid], lst[high] = lst[high], lst[mid]
            high -= 1

# Example Usage
lst = [2, 0, 2, 1, 1, 0]
dutch_national_flag(lst)
print(lst)  # Output: [0, 0, 1, 1, 2, 2]
```

---

## Summary
This guide provides an in-depth explanation of Python lists, advanced algorithms, LeetCode problem recommendations, and additional techniques tailored to Python's capabilities. Use the examples to practice and solidify your understanding. Happy coding!