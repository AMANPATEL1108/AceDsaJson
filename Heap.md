## Priority Queues in Java: A Comprehensive Guide

### Table of Contents

1. [Introduction to Priority Queues](#introduction-to-priority-queues)
2. [Types of Heaps](#types-of-heaps)
3. [Priority Queue Operations](#priority-queue-operations)
4. [Implementing Priority Queue in Java](#implementing-priority-queue-in-java)
5. [Applications of Priority Queues](#applications-of-priority-queues)
6. [Common Priority Queue Problems](#common-priority-queue-problems)
7. [Best Practices and Tips](#best-practices-and-tips)
8. [Conclusion](#conclusion)

### Introduction to Priority Queues

A **Priority Queue** is an advanced version of a queue where each element is assigned a priority. The element with the highest priority is dequeued before other elements, regardless of their insertion order. It is typically implemented using a **Heap** (Min-Heap or Max-Heap).

Key characteristics of a priority queue:

- Elements are processed based on priority, not just the insertion order.
- The underlying data structure is usually a **Heap**, which allows efficient access to the highest or lowest priority element.
- Commonly used in scenarios like scheduling, pathfinding algorithms, and resource management.

### Types of Heaps

1. **Min-Heap**:

   - The element with the smallest priority value is always at the top (root).
   - Used to implement a priority queue where the smallest element is dequeued first.

2. **Max-Heap**:
   - The element with the largest priority value is always at the top.
   - Used to implement a priority queue where the largest element is dequeued first.

### Priority Queue Operations

- **Insert (enqueue)**: Adds an element to the priority queue with a given priority.
- **Remove (dequeue)**: Removes and returns the element with the highest priority (Min or Max depending on the type).
- **Peek**: Returns the element with the highest priority without removing it.
- **Size**: Returns the number of elements in the priority queue.
- **isEmpty**: Checks if the priority queue is empty.

### Implementing Priority Queue in Java

Java provides the `PriorityQueue` class in the `java.util` package, which by default is implemented as a **Min-Heap**. If you need a Max-Heap, you can use a custom comparator.

#### Using `java.util.PriorityQueue` (Min-Heap):

```java
import java.util.PriorityQueue;

PriorityQueue<Integer> minHeap = new PriorityQueue<>();
minHeap.add(10);  // Insert 10
minHeap.add(5);   // Insert 5
minHeap.add(20);  // Insert 20

System.out.println(minHeap.peek());  // Peek: 5 (Smallest element)
System.out.println(minHeap.poll());  // Dequeue: 5
System.out.println(minHeap.poll());  // Dequeue: 10
```

#### Max-Heap using a Custom Comparator:

```java
import java.util.PriorityQueue;
import java.util.Comparator;

PriorityQueue<Integer> maxHeap = new PriorityQueue<>(Comparator.reverseOrder());
maxHeap.add(10);  // Insert 10
maxHeap.add(5);   // Insert 5
maxHeap.add(20);  // Insert 20

System.out.println(maxHeap.peek());  // Peek: 20 (Largest element)
System.out.println(maxHeap.poll());  // Dequeue: 20
System.out.println(maxHeap.poll());  // Dequeue: 10
```

#### Custom Heap Implementation:

If you want full control, you can implement a heap manually using an array.

```java
class MinHeap {
    private int[] heap;
    private int size;
    private int capacity;

    public MinHeap(int capacity) {
        this.capacity = capacity;
        this.size = 0;
        heap = new int[capacity];
    }

    private int parent(int i) { return (i - 1) / 2; }
    private int leftChild(int i) { return 2 * i + 1; }
    private int rightChild(int i) { return 2 * i + 2; }

    public void insert(int key) {
        if (size == capacity) {
            System.out.println("Heap Overflow");
            return;
        }
        heap[size] = key;
        int current = size;
        size++;

        while (current != 0 && heap[parent(current)] > heap[current]) {
            swap(current, parent(current));
            current = parent(current);
        }
    }

    public int remove() {
        if (size == 0) {
            System.out.println("Heap Underflow");
            return -1;
        }
        int root = heap[0];
        heap[0] = heap[size - 1];
        size--;
        heapify(0);
        return root;
    }

    private void heapify(int i) {
        int smallest = i;
        int left = leftChild(i);
        int right = rightChild(i);

        if (left < size && heap[left] < heap[smallest])
            smallest = left;
        if (right < size && heap[right] < heap[smallest])
            smallest = right;
        if (smallest != i) {
            swap(i, smallest);
            heapify(smallest);
        }
    }

    private void swap(int x, int y) {
        int temp = heap[x];
        heap[x] = heap[y];
        heap[y] = temp;
    }
}
```

### Applications of Priority Queues

- **Dijkstra's Algorithm**:
  Priority queues are used to efficiently find the shortest path in a weighted graph.

- **Task Scheduling**:
  Operating systems use priority queues to manage CPU task scheduling, ensuring high-priority tasks are handled first.

- **Huffman Encoding**:
  Priority queues help in constructing the Huffman Tree, which is used in data compression algorithms.

- **Event-Driven Simulations**:
  Events with higher priority are processed first in simulations of real-world systems.

### Common Priority Queue Problems

1. **Merge K Sorted Lists**:
   Merge `k` sorted linked lists into one sorted list using a priority queue.

2. **Find Kth Largest Element in an Array**:
   Use a Min-Heap to efficiently find the `k`th largest element.

3. **Top K Frequent Elements**:
   Given an array of elements, return the `k` most frequent elements.

```java
// Example: Find Kth Largest Element in an Array
public int findKthLargest(int[] nums, int k) {
    PriorityQueue<Integer> minHeap = new PriorityQueue<>();
    for (int num : nums) {
        minHeap.add(num);
        if (minHeap.size() > k) {
            minHeap.poll();  // Keep only the k largest elements
        }
    }
    return minHeap.peek();
}
```

### Best Practices and Tips

1. Use **Min-Heap** for problems involving the smallest elements, and **Max-Heap** for the largest elements.
2. If the input elements are dynamic or not known in advance, priority queues are often a good choice.
3. Be mindful of the **heap size** when solving problems like "Top K Elements" to avoid unnecessary memory usage.
4. Utilize Java's **Comparator** or **lambda functions** to define custom priority queues when default behavior (natural ordering) isn't sufficient.

### Conclusion

Priority Queues (Heaps) are essential data structures in many algorithms, offering efficient solutions to problems involving ordering, scheduling, and selection. With a solid understanding of how heaps work and how to implement them, you can tackle complex problems like Dijkstra's algorithm, task scheduling, and data compression.
