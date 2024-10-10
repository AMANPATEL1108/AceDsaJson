## Queues in Java: A Comprehensive Guide

### Table of Contents

1. [Introduction to Queues](#introduction-to-queues)
2. [Queue Operations](#queue-operations)
3. [Types of Queues](#types-of-queues)
4. [Implementing a Queue in Java](#implementing-a-queue-in-java)
5. [Applications of Queues](#applications-of-queues)
6. [Common Queue Problems](#common-queue-problems)
7. [Best Practices and Tips](#best-practices-and-tips)
8. [Conclusion](#conclusion)

### Introduction to Queues

A **Queue** is a linear data structure that follows the **FIFO (First In, First Out)** principle. The element inserted first is the one to be removed first. Queues are widely used in scenarios like scheduling, task management, and buffering.

Key characteristics of queues:

- Follows the **FIFO** principle.
- Basic operations: **enqueue**, **dequeue**, **peek**.
- Can be implemented using arrays, linked lists, or even stacks.

### Queue Operations

- **Enqueue**: Add an element to the end (rear) of the queue.
- **Dequeue**: Remove and return the element from the front of the queue.
- **Peek**: Get the front element without removing it.
- **isEmpty**: Check if the queue is empty.
- **Size**: Get the number of elements in the queue.

### Types of Queues

- **Simple Queue**: Follows the standard FIFO principle.
- **Circular Queue**: The last position connects back to the first, forming a circle.
- **Priority Queue**: Each element has a priority, and elements with higher priority are dequeued first.
- **Deque (Double-Ended Queue)**: Allows insertion and deletion from both ends.

### Implementing a Queue in Java

#### Using `java.util.Queue` Interface (LinkedList-based):

```java
import java.util.LinkedList;
import java.util.Queue;

Queue<Integer> queue = new LinkedList<>();

queue.offer(10);  // Enqueue 10
queue.offer(20);  // Enqueue 20

System.out.println(queue.peek());  // Peek: 10
System.out.println(queue.poll());  // Dequeue: 10
System.out.println(queue.isEmpty());  // Check if empty
```

#### Custom Implementation (Array-based Queue):

```java
class Queue {
    private int arr[];
    private int front, rear, capacity, count;

    Queue(int size) {
        arr = new int[size];
        capacity = size;
        front = 0;
        rear = -1;
        count = 0;
    }

    public void enqueue(int item) {
        if (count == capacity) {
            System.out.println("Queue Overflow");
            return;
        }
        rear = (rear + 1) % capacity;
        arr[rear] = item;
        count++;
    }

    public int dequeue() {
        if (count == 0) {
            System.out.println("Queue Underflow");
            return -1;
        }
        int item = arr[front];
        front = (front + 1) % capacity;
        count--;
        return item;
    }

    public int peek() {
        if (count == 0) {
            System.out.println("Queue is empty");
            return -1;
        }
        return arr[front];
    }

    public boolean isEmpty() {
        return count == 0;
    }

    public int size() {
        return count;
    }
}
```

#### Circular Queue Implementation:

```java
class CircularQueue {
    private int arr[];
    private int front, rear, capacity, count;

    CircularQueue(int size) {
        arr = new int[size];
        capacity = size;
        front = 0;
        rear = -1;
        count = 0;
    }

    public void enqueue(int item) {
        if (count == capacity) {
            System.out.println("Queue Overflow");
            return;
        }
        rear = (rear + 1) % capacity;
        arr[rear] = item;
        count++;
    }

    public int dequeue() {
        if (count == 0) {
            System.out.println("Queue Underflow");
            return -1;
        }
        int item = arr[front];
        front = (front + 1) % capacity;
        count--;
        return item;
    }

    public int peek() {
        if (count == 0) {
            System.out.println("Queue is empty");
            return -1;
        }
        return arr[front];
    }

    public boolean isEmpty() {
        return count == 0;
    }

    public int size() {
        return count;
    }
}
```

### Applications of Queues

- **Scheduling**:
  Queues are used in CPU scheduling, disk scheduling, and task management.

- **Buffering**:
  Used in data streaming, such as IO Buffers, and network queues to handle packet traffic.

- **Breadth-First Search (BFS)**:
  BFS uses queues to explore nodes level by level.

- **Cache Management**:
  Implementing a first-come, first-served caching system (e.g., FIFO cache).

### Common Queue Problems

1. **Implement Queue using Stacks**:
   Design a queue using two stacks to hold elements.

2. **Circular Tour Problem**:
   Given petrol stations and distances, find if there's a circular tour that visits all stations.

3. **Rotten Oranges Problem**:
   Given a grid of fresh and rotten oranges, determine the minimum time required to rot all the fresh oranges.

```java
// Example: Implement Queue using Two Stacks
class MyQueue {
    Stack<Integer> stack1 = new Stack<>();
    Stack<Integer> stack2 = new Stack<>();

    public void enqueue(int x) {
        stack1.push(x);
    }

    public int dequeue() {
        if (stack2.isEmpty()) {
            while (!stack1.isEmpty()) {
                stack2.push(stack1.pop());
            }
        }
        if (!stack2.isEmpty()) {
            return stack2.pop();
        } else {
            System.out.println("Queue is empty");
            return -1;
        }
    }
}
```

### Best Practices and Tips

1. **Use Queues** when you need a **FIFO** structure.
2. For dynamically resizing queues, consider using `LinkedList` or `Deque`.
3. **Circular Queues** can be efficient in terms of memory when dealing with fixed-size buffers.
4. Be cautious with queue overflows and underflows in custom implementations.

### Conclusion

Queues are widely used and highly efficient data structures for scenarios involving sequential processing and resource management. Understanding how to implement and utilize queues is crucial for solving problems like scheduling, task processing, and breadth-first traversal.
