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

## Sorting Algorithms

### 1. QuickSort
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

### 2. MergeSort
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

## Searching Algorithms

### 1. Binary Search
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

## Two Pointers Technique
The Two Pointers technique is used for problems involving sorted arrays, subarrays, or pairs of numbers that meet certain conditions.

#### Example: Removing Duplicates
```python
def remove_duplicates(arr):
    if not arr:
        return 0
    write_index = 1
    for i in range(1, len(arr)):
        if arr[i] != arr[i - 1]:
            arr[write_index] = arr[i]
            write_index += 1
    return write_index

# Example Usage
arr = [1, 1, 2, 2, 3, 3, 4]
new_length = remove_duplicates(arr)
print(arr[:new_length])  # Output: [1, 2, 3, 4]
```

---

## Sliding Window Technique
The Sliding Window technique is commonly used to solve problems involving subarrays, such as finding the maximum or minimum sum of a subarray of fixed size.

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

---

## Summary
This guide provides an in-depth explanation of arrays and associated techniques. Use the code examples to practice and solidify your understanding. Happy coding!
