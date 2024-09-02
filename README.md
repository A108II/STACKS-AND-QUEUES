# Stacks & Quesues Documentation
# Stacks

A stack is a Last-In-First-Out (LIFO) data structure, where elements are added and removed from the top.

## Classes

### 1. **Node Class**
The `Node` class represents each element in the stack.

- **Constructor:** Takes a `value` and initializes `value` and `next` properties.
  
```javascript
class Node {
    constructor(value) {
        this.value = value; // Value of the node
        this.next = null;    // Pointer to the next node (initially null)
    }
}
```

### 2. **Stack Class**
The `Stack` class manages the stack operations.

- **Constructor:** Initializes a new stack with a single node, setting it as the top.

```javascript
class Stack {
    constructor(value) {
        const new_node = new Node(value);
        this.top = new_node; // Points to the top of the stack
        this.length = 1;     // Tracks the number of elements in the stack
    }
}
```

### 3. **Methods**

#### a. **push(value)**: Adds a new node to the top of the stack.

- Creates a new `Node`.
- If the stack is empty (`length === 0`), the new node becomes the top.
- Otherwise, the new node's `next` pointer references the current top, and the top is updated.
- Increments the stack's length and returns the stack object.

```javascript
push(value) {
    const new_node = new Node(value);
    if (this.length === 0) {
        this.top = new_node;
    } else {
        new_node.next = this.top;
        this.top = new_node;
    }
    this.length++;
    return this;
}
```

#### b. **pop()**: Removes the top node from the stack and returns it.

- If the stack is empty (`length === 0`), returns `undefined`.
- Stores the current top in a temporary variable.
- Updates the top to the next node and disconnects the removed node.
- Decrements the stack's length and returns the removed node.

```javascript
pop() {
    if (this.length === 0) {
        return undefined;
    }
    let temp = this.top;
    this.top = this.top.next;
    temp.next = null;
    this.length--;
    return temp;
}
```

## Usage Example

```javascript
let stack1 = new Stack(3); // Creates a stack with initial value 3
stack1.push(87);           // Stack: 87 -> 3
stack1.push(34);           // Stack: 34 -> 87 -> 3
stack1.push(29);           // Stack: 29 -> 34 -> 87 -> 3
stack1.pop();              // Removes 29, Stack: 34 -> 87 -> 3
```

# Queues

A queue is a First-In-First-Out (FIFO) data structure, where elements are added at the end and removed from the front.

## Classes

### 1. **Node Class**
The `Node` class represents each element in the queue.

- **Constructor:** Takes a `value` and initializes `value` and `next` properties.
  
```javascript
class Node {
    constructor(value) {
        this.value = value; // Value of the node
        this.next = null;    // Pointer to the next node (initially null)
    }
}
```

### 2. **Queue Class**
The `Queue` class manages the queue operations.

- **Constructor:** Initializes a new queue with a single node, setting it as both the first and last element.

```javascript
class Queue {
    constructor(value) {
        const new_node = new Node(value);
        this.first = new_node; // Points to the first node in the queue
        this.last = new_node;  // Points to the last node in the queue
        this.length = 1;       // Tracks the number of elements in the queue
    }
}
```

### 3. **Methods**

#### a. **enqueue(value)**: Adds a new node to the end of the queue.

- Creates a new `Node`.
- If the queue is empty (`length === 0`), the new node becomes both the first and last node.
- Otherwise, the current last node's `next` pointer references the new node, and the last is updated.
- Increments the queue's length and returns the queue object.

```javascript
enqueue(value) {
    const new_node = new Node(value);
    if (this.length === 0) {
        this.first = new_node;
        this.last = new_node;
    } else {
        this.last.next = new_node; // Link current last to the new node
        this.last = new_node;      // Update last to the new node
    }
    this.length++;
    return this;
}
```

#### b. **dequeue()**: Removes the first node from the queue and returns it.

- If the queue is empty (`length === 0`), returns `undefined`.
- Stores the current first node in a temporary variable.
- Updates the first to the next node and disconnects the removed node.
- Decrements the queue's length.
- If the queue becomes empty, it sets `last` to `null`.
- Returns the removed node.

```javascript
dequeue() {
    if (this.length === 0) {
        return undefined;
    }
    let temp = this.first;   // Store the current first node
    this.first = this.first.next; // Update first to the next node
    temp.next = null;        // Disconnect the removed node
    this.length--;

    if (this.length === 0) {
        this.last = null;    // If queue is empty, reset last to null
    }

    return temp;
}
```

## Usage Example

```javascript
let queue1 = new Queue(3); // Creates a queue with initial value 3
queue1.enqueue(5);         // Queue: 3 -> 5
queue1.enqueue(8);         // Queue: 3 -> 5 -> 8
queue1.enqueue(1);         // Queue: 3 -> 5 -> 8 -> 1
queue1.dequeue();          // Removes 3, Queue: 5 -> 8 -> 1
```

