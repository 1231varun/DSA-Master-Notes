# Linked Lists - The Ultimate DSA Guide Notes (JavaScript)

## Overview of Linked Lists

### What are Linked Lists?
A **Linked List** is a linear data structure where each element, called a **node**, contains two parts:
1. **Data**: The actual value of the node.
2. **Pointer (or Reference)**: A link to the next node in the sequence.

Unlike arrays, linked lists do not store elements in contiguous memory locations. This dynamic allocation makes them flexible but introduces additional complexity.

### Key Features:
1. **Dynamic Size**: The size of the linked list can grow or shrink dynamically without the need for reallocation or reorganization.
2. **Efficient Insertion/Deletion**: Operations like insertion and deletion are faster compared to arrays, especially for large datasets.
3. **No Random Access**: Elements must be accessed sequentially starting from the head.
4. **Memory Overhead**: Additional memory is required to store pointers.

### Types of Linked Lists:
1. **Singly Linked List**: Each node points to the next node.
2. **Doubly Linked List**: Each node points to both the next and the previous node.
3. **Circular Linked List**: The last node points back to the first node, forming a circular structure.

---

## Basic Operations

### Traversal
Traversal involves visiting each node in the list sequentially, starting from the head.

#### Code Example (Singly Linked List):
```javascript
class Node {
  constructor(data) {
    this.data = data;
    this.next = null;
  }
}

class LinkedList {
  constructor() {
    this.head = null;
  }

  traverse() {
    let current = this.head;
    while (current) {
      process.stdout.write(`${current.data} -> `);
      current = current.next;
    }
    console.log("null");
  }
}

// Example Usage
const ll = new LinkedList();
ll.head = new Node(1);
ll.head.next = new Node(2);
ll.head.next.next = new Node(3);

ll.traverse(); // Output: 1 -> 2 -> 3 -> null
```

---

### Insertion
Insertion can be done at the beginning, end, or a specific position.

#### Code Example:
```javascript
class LinkedList {
  insertAtBeginning(data) {
    const newNode = new Node(data);
    newNode.next = this.head;
    this.head = newNode;
  }

  insertAtEnd(data) {
    const newNode = new Node(data);
    if (!this.head) {
      this.head = newNode;
      return;
    }
    let current = this.head;
    while (current.next) {
      current = current.next;
    }
    current.next = newNode;
  }

  insertAtPosition(position, data) {
    if (position === 0) {
      this.insertAtBeginning(data);
      return;
    }
    const newNode = new Node(data);
    let current = this.head;
    for (let i = 0; i < position - 1; i++) {
      if (!current.next) {
        throw new Error("Position out of bounds");
      }
      current = current.next;
    }
    newNode.next = current.next;
    current.next = newNode;
  }
}

// Example Usage
const ll = new LinkedList();
ll.insertAtBeginning(2);
ll.insertAtEnd(3);
ll.insertAtPosition(1, 5);
ll.traverse(); // Output: 2 -> 5 -> 3 -> null
```

---

### Deletion
Deletion can occur at the beginning, end, or a specific position.

#### Code Example:
```javascript
class LinkedList {
  deleteAtBeginning() {
    if (!this.head) return;
    this.head = this.head.next;
  }

  deleteAtEnd() {
    if (!this.head) return;
    if (!this.head.next) {
      this.head = null;
      return;
    }
    let current = this.head;
    while (current.next.next) {
      current = current.next;
    }
    current.next = null;
  }

  deleteAtPosition(position) {
    if (position === 0) {
      this.deleteAtBeginning();
      return;
    }
    let current = this.head;
    for (let i = 0; i < position - 1; i++) {
      if (!current.next) {
        throw new Error("Position out of bounds");
      }
      current = current.next;
    }
    if (!current.next) {
      throw new Error("Position out of bounds");
    }
    current.next = current.next.next;
  }
}

// Example Usage
const ll = new LinkedList();
ll.insertAtBeginning(1);
ll.insertAtEnd(3);
ll.insertAtEnd(4);
ll.deleteAtPosition(1);
ll.traverse(); // Output: 1 -> 4 -> null
```

---

### Reversal
Reversing a linked list can be done iteratively or recursively.

#### Iterative Approach:
```javascript
reverseIterative() {
  let prev = null;
  let current = this.head;
  while (current) {
    const nextNode = current.next;
    current.next = prev;
    prev = current;
    current = nextNode;
  }
  this.head = prev;
}
```

#### Recursive Approach:
```javascript
reverseRecursive(node = this.head) {
  if (!node || !node.next) {
    this.head = node;
    return node;
  }
  const reversedList = this.reverseRecursive(node.next);
  node.next.next = node;
  node.next = null;
  return reversedList;
}
```

---

### Cycle Detection
Detecting a cycle in a linked list can be done using **Floyd's Tortoise and Hare Algorithm**.

#### Code Example:
```javascript
detectCycle() {
  let slow = this.head;
  let fast = this.head;

  while (fast && fast.next) {
    slow = slow.next;
    fast = fast.next.next;
    if (slow === fast) return true;
  }
  return false;
}
```

---

## Advanced Algorithms

### Merge Two Sorted Linked Lists
```javascript
function mergeSortedLists(l1, l2) {
  const dummy = new Node(0);
  let tail = dummy;

  while (l1 && l2) {
    if (l1.data < l2.data) {
      tail.next = l1;
      l1 = l1.next;
    } else {
      tail.next = l2;
      l2 = l2.next;
    }
    tail = tail.next;
  }

  tail.next = l1 || l2;
  return dummy.next;
}
```

### Find Middle Node
```javascript
findMiddle() {
  let slow = this.head;
  let fast = this.head;

  while (fast && fast.next) {
    slow = slow.next;
    fast = fast.next.next;
  }

  return slow.data;
}
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
This guide provides an in-depth explanation of linked lists, supported operations, advanced algorithms, and LeetCode problem recommendations tailored for JavaScript. Use the examples and algorithms to strengthen your understanding and problem-solving skills. Happy coding!
