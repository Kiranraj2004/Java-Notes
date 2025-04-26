
## 1. **Introduction to Stack**

- Stack is a part of the **Collection Framework** in Java.
    
- `Stack` **extends** `Vector`, so it inherits all methods from `Vector`.
    
- **Stack follows LIFO** (Last-In-First-Out) principle:
    
    - Last element added → First element removed.
        

**Example**:  
Stack of books or cookies — you always pick from the top first.

---

## 2. **Basic Operations in Stack**

|Operation|Description|
|---|---|
|`push(E item)`|Adds an item to the top of the stack.|
|`pop()`|Removes and returns the top item of the stack.|
|`peek()`|Returns the top item without removing it.|
|`isEmpty()`|Checks if the stack is empty.|
|`size()`|Returns the number of elements in the stack.|
|`search(Object o)`|Returns the 1-based position of the element from the top.|

---

## 3. **Stack and Vector Relationship**

- Stack extends `Vector`, so **all vector methods are also available** to Stack.
    
- You can **add at a specific index**, **remove** elements by index, etc.
    
- **All operations in Stack (from Vector) are synchronized** → Thread-safe.
    

---

## 4. **Java Code Example for Stack**

```java
import java.util.Stack;

public class StackDemo {
    public static void main(String[] args) {
        Stack<Integer> stack = new Stack<>();

        // Pushing elements onto the stack
        stack.push(1);
        stack.push(2);
        stack.push(3);
        stack.push(4);
        stack.push(5);
        System.out.println("Initial Stack: " + stack);

        // Popping the top element
        int popped = stack.pop();
        System.out.println("Popped element: " + popped);
        System.out.println("Stack after pop: " + stack);

        // Peeking the top element
        int top = stack.peek();
        System.out.println("Top element (after pop): " + top);
        System.out.println("Stack after peek: " + stack);

        // Checking if stack is empty
        System.out.println("Is stack empty? " + stack.isEmpty());

        // Size of the stack
        System.out.println("Current size of stack: " + stack.size());

        // Searching an element
        int position = stack.search(3);
        System.out.println("Position of element 3 (from top): " + position);
    }
}
```

---

## 5. **Expected Output**

```
Initial Stack: [1, 2, 3, 4, 5]
Popped element: 5
Stack after pop: [1, 2, 3, 4]
Top element (after pop): 4
Stack after peek: [1, 2, 3, 4]
Is stack empty? false
Current size of stack: 4
Position of element 3 (from top): 2
```

---

## 6. **Other Ways to Implement Stack Behavior**

> You can **simulate Stack** using other data structures too:

---

### (A) **Using LinkedList as Stack**

- `LinkedList` allows efficient insertion/removal from both ends (because it’s a doubly-linked list).
    

**Code:**

```java
import java.util.LinkedList;

public class LinkedListAsStack {
    public static void main(String[] args) {
        LinkedList<Integer> stack = new LinkedList<>();

        // Push elements
        stack.addLast(1);
        stack.addLast(2);
        stack.addLast(3);
        System.out.println("Initial LinkedList (as Stack): " + stack);

        // Peek top
        int top = stack.getLast();
        System.out.println("Top element: " + top);

        // Pop element
        int popped = stack.removeLast();
        System.out.println("Popped element: " + popped);
        System.out.println("Stack after pop: " + stack);

        // Check empty
        System.out.println("Is stack empty? " + stack.isEmpty());
    }
}
```

---

### (B) **Using ArrayList as Stack**

- `ArrayList` is not ideal for stack, but it **can** be used manually.
    
- No direct methods like `push/pop/peek`, you have to manage indexes manually.
    

**Code:**

```java
import java.util.ArrayList;

public class ArrayListAsStack {
    public static void main(String[] args) {
        ArrayList<Integer> stack = new ArrayList<>();

        // Push elements
        stack.add(1);
        stack.add(2);
        stack.add(3);
        System.out.println("Initial ArrayList (as Stack): " + stack);

        // Peek top
        int top = stack.get(stack.size() - 1);
        System.out.println("Top element: " + top);

        // Pop element
        int popped = stack.remove(stack.size() - 1);
        System.out.println("Popped element: " + popped);
        System.out.println("Stack after pop: " + stack);

        // Check empty
        System.out.println("Is stack empty? " + stack.isEmpty());
    }
}
```

---

## 7. **Important Points**

- `Stack` internally uses `Vector`, which internally uses **Array**.
    
- Hence, insertion and removal from the end (`push` and `pop`) are in **O(1)** time.
    
- Since `Stack` is synchronized, it’s slower than `LinkedList` or `ArrayList` in single-threaded applications.
    
- **Recommendation**:
    
    - In multi-threaded cases → prefer `Stack`.
        
    - In single-threaded cases → use `LinkedList` or **better** `ArrayDeque` (we'll study `Deque` later).
        

---

## 8. **Quick Comparison Table**

|Structure|Time Complexity (Push/Pop)|Thread Safe|Comment|
|---|---|---|---|
|Stack|O(1)|Yes|Safe but slower|
|LinkedList|O(1)|No|Fast|
|ArrayList|O(1) (Amortized)|No|Manual handling required|
|ArrayDeque|O(1)|No|Recommended for Stack behavior|

---

# ✅ Summary:

- Stack = LIFO
    
- Push → Add to top
    
- Pop → Remove from top
    
- Peek → See top element
    
- Use `Stack`, `LinkedList`, or `ArrayDeque` depending on your use case.
    