# Linked Lists - The Ultimate DSA Guide Notes

## Overview of Linked Lists

### What are Linked Lists?
A **Linked List** is a linear data structure where each element, called a **node**, contains two parts:
1. **Data**: The actual value of the node.
2. **Pointer (or Reference)**: A link to the next node in the sequence.

Unlike arrays, linked lists do not store elements in contiguous memory locations. This dynamic allocation makes them flexible but also introduces additional complexity.

### Key Features:
1. **Dynamic Size**: The size of the linked list can grow or shrink dynamically without the need for reallocation or reorganization.
2. **Efficient Insertion/Deletion**: Operations such as insertion and deletion are faster compared to arrays, especially for large datasets.
3. **No Random Access**: Elements must be accessed sequentially starting from the head.
4. **Memory Overhead**: Requires additional memory for storing pointers.

### Types of Linked Lists:
1. **Singly Linked List**: Each node points to the next node.
2. **Doubly Linked List**: Each node points to both the next and the previous node.
3. **Circular Linked List**: The last node points back to the first node, forming a circular structure.
4. **Circular Doubly Linked List**: A combination of doubly and circular linked lists.

---

## Basic Operations

### Traversal
Traversal involves visiting each node in the list sequentially, starting from the head.

#### Code Example (Singly Linked List):
```python
class Node:
    def __init__(self, data):
        self.data = data
        self.next = None

class LinkedList:
    def __init__(self):
        self.head = None

    def traverse(self):
        current = self.head
        while current:
            print(current.data, end=" -> ")
            current = current.next
        print("None")

# Example Usage
ll = LinkedList()
ll.head = Node(1)
second = Node(2)
third = Node(3)
ll.head.next = second
second.next = third

ll.traverse()  # Output: 1 -> 2 -> 3 -> None
```

---

### Insertion
Insertion can be done at the beginning, end, or at a specific position.

#### Code Example:
```python
class LinkedList:
    def insert_at_beginning(self, data):
        new_node = Node(data)
        new_node.next = self.head
        self.head = new_node

    def insert_at_end(self, data):
        new_node = Node(data)
        if not self.head:
            self.head = new_node
            return
        current = self.head
        while current.next:
            current = current.next
        current.next = new_node

    def insert_at_position(self, position, data):
        if position == 0:
            self.insert_at_beginning(data)
            return
        new_node = Node(data)
        current = self.head
        for _ in range(position - 1):
            if not current.next:
                raise IndexError("Position out of bounds")
            current = current.next
        new_node.next = current.next
        current.next = new_node

# Example Usage
ll = LinkedList()
ll.insert_at_beginning(2)
ll.insert_at_end(3)
ll.insert_at_position(1, 5)
ll.traverse()  # Output: 2 -> 5 -> 3 -> None
```

---

### Deletion
Deletion can occur at the beginning, end, or a specific position.

#### Code Example:
```python
class LinkedList:
    def delete_at_beginning(self):
        if not self.head:
            return
        self.head = self.head.next

    def delete_at_end(self):
        if not self.head:
            return
        if not self.head.next:
            self.head = None
            return
        current = self.head
        while current.next.next:
            current = current.next
        current.next = None

    def delete_at_position(self, position):
        if position == 0:
            self.delete_at_beginning()
            return
        current = self.head
        for _ in range(position - 1):
            if not current.next:
                raise IndexError("Position out of bounds")
            current = current.next
        if not current.next:
            raise IndexError("Position out of bounds")
        current.next = current.next.next

# Example Usage
ll.delete_at_beginning()
ll.delete_at_end()
ll.delete_at_position(1)
ll.traverse()
```

---

### Reversal
Reversing a linked list can be done iteratively or recursively.

#### Iterative Approach:
```python
def reverse_iterative(self):
    prev = None
    current = self.head
    while current:
        next_node = current.next
        current.next = prev
        prev = current
        current = next_node
    self.head = prev
```

#### Recursive Approach:
```python
def reverse_recursive(self, node):
    if not node or not node.next:
        self.head = node
        return
    self.reverse_recursive(node.next)
    node.next.next = node
    node.next = None
```

---

### Cycle Detection
Detecting a cycle in a linked list can be done using **Floyd's Tortoise and Hare Algorithm**.

#### Code Example:
```python
def detect_cycle(self):
    slow = self.head
    fast = self.head

    while fast and fast.next:
        slow = slow.next
        fast = fast.next.next
        if slow == fast:
            return True

    return False
```

---

## Advanced Algorithms

### Merge Two Sorted Linked Lists
```python
def merge_sorted_lists(l1, l2):
    dummy = Node(0)
    tail = dummy

    while l1 and l2:
        if l1.data < l2.data:
            tail.next = l1
            l1 = l1.next
        else:
            tail.next = l2
            l2 = l2.next
        tail = tail.next

    tail.next = l1 or l2
    return dummy.next
```

### Find Middle Node
```python
def find_middle(self):
    slow = self.head
    fast = self.head

    while fast and fast.next:
        slow = slow.next
        fast = fast.next.next

    return slow.data
```

### Detect and Remove Cycle
```python
def detect_and_remove_cycle(self):
    slow = self.head
    fast = self.head
    while fast and fast.next:
        slow = slow.next
        fast = fast.next.next
        if slow == fast:
            self.remove_cycle(slow)
            return True
    return False

def remove_cycle(self, loop_node):
    ptr1 = self.head
    ptr2 = loop_node
    while ptr1.next != ptr2.next:
        ptr1 = ptr1.next
        ptr2 = ptr2.next
    ptr2.next = None
```

---

## Recommended LeetCode Problems (Linked Lists)

### Easy Level:
1. [Reverse Linked List](https://leetcode.com/problems/reverse-linked-list/)
2. [Middle of the Linked List](https://leetcode.com/problems/middle-of-the-linked-list/)
3. [Merge Two Sorted Lists](https://leetcode.com/problems/merge-two-sorted-lists/)

### Medium Level:
1. [Add Two Numbers](https://leetcode.com/problems/add-two-numbers/)
2. [Remove Nth Node From End of List](https://leetcode.com/problems/remove-nth-node-from-end-of-list/)
3. [Reorder List](https://leetcode.com/problems/reorder-list/)

### Hard Level:
1. [Merge k Sorted Lists](https://leetcode.com/problems/merge-k-sorted-lists/)
2. [Reverse Nodes in k-Group](https://leetcode.com/problems/reverse-nodes-in-k-group/)
3. [Linked List Cycle II](https://leetcode.com/problems/linked-list-cycle-ii/)

---

## Summary
This guide provides an in-depth explanation of linked lists, supported operations, advanced algorithms, and LeetCode problem recommendations. Use the examples and algorithms to strengthen your understanding and problem-solving skills. Happy coding!
