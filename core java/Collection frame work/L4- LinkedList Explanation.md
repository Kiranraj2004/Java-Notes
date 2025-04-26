
## 1. **Understanding List and ArrayList**

- In `List` or `ArrayList`, elements are stored **contiguously** (i.e., in continuous memory).
    
- Accessing elements is fast, like `arr[i]` because it's just a **base address + index** calculation.
    

## 2. **Problem with Continuous Memory**

- When elements are stored sequentially:
    
    - Memory should be free in a large enough continuous block.
        
    - Resizing needs creating a bigger array and copying elements.
        

---

## 3. **Introduction to Linked List**

- **LinkedList** does **NOT** use continuous memory.
    
- Instead, it uses a structure where:
    
    - Each element (called a **Node**) contains:
        
        - The actual **data** (value).
            
        - A **reference** (pointer) to the **next Node**.
            

> **Analogy:**  
> Suppose you visit a locker (Node 1) and inside, there's a slip with the address of the next locker (Node 2), and so on.

---

## 4. **Node Structure**

- Each **Node** stores:
    
    1. **Data** (any value like int, String, etc.)
        
    2. **Pointer/Reference** to the next node.
        

If a node is the **last node**, its pointer points to `null`.

---

## 5. **Types of Linked Lists**

|Type|Description|
|:--|:--|
|**Singly Linked List**|Node points to **next node only**.|
|**Doubly Linked List**|Node points to **next** and **previous** nodes.|
|**Circular Linked List**|Last node points to **first node** (making a circle).|

---

## 6. **LinkedList in Java Collections**

- In Java, `LinkedList` is part of the **Collection Framework**.
    
- It implements the `List` interface.
    
- Internally, Java’s `LinkedList` is a **Doubly Linked List**.
    
    - Each node has:
        
        - `data`
            
        - `next` pointer
            
        - `prev` pointer
            

---

# **Self-Created LinkedList Example (Code)**

Let’s manually create a simple linked list in Java to understand:

```java
// File: Test.java

class Test {
    public static void main(String[] args) {
        // Creating nodes manually
        Node node1 = new Node(1);
        Node node2 = new Node(2);
        Node node3 = new Node(3);

        // Linking nodes
        node1.next = node2;
        node2.next = node3;

        // Traversing the linked list
        Node temp = node1; // start with head node
        while (temp != null) {
            System.out.print(temp.value + " -> ");
            temp = temp.next;
        }
        System.out.print("null");
    }
}

// Node class
class Node {
    public int value;
    public Node next;

    public Node(int value) {
        this.value = value;
        this.next = null; // next initially null
    }
}
```

---

### **Output:**

```
1 -> 2 -> 3 -> null
```

---

✅ **Explanation of Code:**

- Created 3 nodes manually with values 1, 2, and 3.
    
- Linked them: `node1.next = node2; node2.next = node3;`
    
- Used a while loop to traverse until we reach `null`.
    

---

# **Working with Java's Built-in LinkedList**

Java already provides `LinkedList` class.

Here’s an example:

```java
import java.util.LinkedList;

class Test {
    public static void main(String[] args) {
        LinkedList<Integer> list = new LinkedList<>();

        // Adding elements
        list.add(1);
        list.add(2);
        list.add(3);

        // Printing list
        System.out.println(list);

        // Accessing elements (index based)
        System.out.println("Element at index 1: " + list.get(1));
        
        // Removing element
        list.remove(1);
        System.out.println("After removing index 1: " + list);
    }
}
```

---

### **Output:**

```
[1, 2, 3]
Element at index 1: 2
After removing index 1: [1, 3]
```

---

✅ **Key Points for Java’s `LinkedList`:**

- Unlike arrays, `LinkedList` does **NOT** need continuous memory.
    
- To get an element by index, **internally it traverses** from the beginning (looping step by step).
    
- That’s why random access in a `LinkedList` is **slow** compared to `ArrayList`.
    

---

# **Summary Table**

|Feature|ArrayList|LinkedList|
|:--|:--|:--|
|Memory|Continuous|Non-continuous (Nodes)|
|Access Speed|Fast (O(1))|Slow (O(n))|
|Insert/Delete Middle|Slow|Fast|
|Structure|Array|Node (Data + Pointer)|

---


## 1. **Removing an Element in LinkedList**

- **In ArrayList**:  
    To delete an element, all the elements to the right must be **shifted** one place left.  
    ❗ This shifting makes deletion expensive.
    
- **In LinkedList**:  
    Just **change the pointer** (reference) of the previous node to the next node.  
    ❗ No need to shift elements — just update references!
    

---

## 2. **Insertion in LinkedList**

- To insert a new element:
    
    - Create a new node.
        
    - Set its `next` pointer to the current node.
        
    - Set the previous node’s `next` pointer to this new node.
        
    
    ✅ Insertion becomes very easy compared to ArrayList!
    

---

## 3. **Comparison: LinkedList vs ArrayList**

|Feature|LinkedList|ArrayList|
|:--|:--|:--|
|Insert/Delete in middle|✅ Efficient (just change pointers)|❌ Expensive (shift elements)|
|Random Access|❌ Slow (must traverse from start)|✅ Fast (direct index access)|
|Memory Overhead|❌ Higher (stores extra pointers)|✅ Lower (just stores elements)|

---

## 4. **Random Access in LinkedList**

- **Slow** because memory is **non-contiguous**.
    
- To get an element at an index, must **traverse** the list from the start.
    

### Example:

```java
LinkedList<Integer> list = new LinkedList<>();
list.add(10);
list.add(20);
list.add(30);

System.out.println(list.get(2)); // Output: 30
```

> 🔵 **Time complexity**:
> 
> - `ArrayList.get(index)`: **O(1)**
>     
> - `LinkedList.get(index)`: **O(n)**
>     

---

## 5. **Memory Overhead**

- **LinkedList** stores **data + pointers (next, previous)** → more memory usage.
    
- **ArrayList** stores only **data**.
    

---

## 6. **Important Methods in LinkedList**

### (a) Add Elements

```java
LinkedList<Integer> ll = new LinkedList<>();
ll.add(1);           // Add at end
ll.addFirst(0);       // Add at beginning
ll.addLast(2);        // Add at end
System.out.println(ll);
```

**Output**:

```
[0, 1, 2]
```

---

### (b) Get Elements

```java
System.out.println(ll.getFirst()); // 0
System.out.println(ll.getLast());  // 2
```

---

### (c) Remove Elements

```java
ll.removeFirst();  // Removes 0
ll.removeLast();   // Removes 2
ll.remove(0);      // Removes by index (after previous removals, 1 is at index 0)

System.out.println(ll);
```

**Output**:

```
[]
```

---

### (d) Remove If (Using Predicate) — Java 8 feature

```java
LinkedList<Integer> numbers = new LinkedList<>();
numbers.add(2);
numbers.add(3);
numbers.add(4);
numbers.add(5);

numbers.removeIf(x -> x % 2 == 0); // Remove even numbers
System.out.println(numbers);
```

**Output**:

```
[3, 5]
```

> 🔵 `removeIf(Predicate)` will remove all elements satisfying the given condition.

---

### (e) Create LinkedList On The Fly

```java
LinkedList<String> animals = new LinkedList<>(Arrays.asList("Cat", "Dog", "Lion", "Elephant"));
System.out.println(animals);
```

**Output**:

```
[Cat, Dog, Lion, Elephant]
```

---

### (f) Remove All (common elements)

```java
LinkedList<String> animals = new LinkedList<>(Arrays.asList("Cat", "Dog", "Lion", "Elephant"));
LinkedList<String> animalsToRemove = new LinkedList<>(Arrays.asList("Dog", "Lion"));

animals.removeAll(animalsToRemove);

System.out.println(animals);
```

**Output**:

```
[Cat, Elephant]
```

---

## 7. **ArrayList also supports removeAll**

```java
ArrayList<Integer> list1 = new ArrayList<>(Arrays.asList(1, 2, 3, 4));
ArrayList<Integer> list2 = new ArrayList<>(Arrays.asList(2, 4));

list1.removeAll(list2);
System.out.println(list1);
```

**Output**:

```
[1, 3]
```

---

## 8. **Polymorphism (Reference of List)**

You can use `LinkedList` reference as `List` type.

```java
List<Integer> list = new LinkedList<>();
list.add(1);
list.add(2);
System.out.println(list);
```

✅ Advantage: **Flexibility**  
❌ Disadvantage: **Cannot access LinkedList-specific methods** like `addFirst`, `addLast`.

---

## 9. **LinkedList can behave like different data structures**

- Behaves like **List** ✅
    
- Behaves like **Stack** ✅ (use `push`, `pop`)
    
- Behaves like **Queue** ✅ (use `offer`, `poll`)
    

> 🔥 Very **powerful** class!

---

# 🔥 Full Code Summary with Outputs:

```java
import java.util.*;

public class LinkedListDemo {
    public static void main(String[] args) {
        
        // LinkedList basic operations
        LinkedList<Integer> ll = new LinkedList<>();
        ll.add(1);
        ll.addFirst(0);
        ll.addLast(2);
        System.out.println("LinkedList: " + ll); // [0, 1, 2]
        
        // Get first and last
        System.out.println("First: " + ll.getFirst()); // 0
        System.out.println("Last: " + ll.getLast());   // 2
        
        // Remove first, last, by index
        ll.removeFirst();
        ll.removeLast();
        ll.remove(0); // Now list is empty
        System.out.println("After Removals: " + ll);   // []
        
        // RemoveIf example
        LinkedList<Integer> numbers = new LinkedList<>(Arrays.asList(2, 3, 4, 5));
        numbers.removeIf(x -> x % 2 == 0);
        System.out.println("After removeIf (even numbers): " + numbers); // [3,5]
        
        // RemoveAll example
        LinkedList<String> animals = new LinkedList<>(Arrays.asList("Cat", "Dog", "Lion", "Elephant"));
        LinkedList<String> animalsToRemove = new LinkedList<>(Arrays.asList("Dog", "Lion"));
        animals.removeAll(animalsToRemove);
        System.out.println("After removeAll: " + animals); // [Cat, Elephant]
        
        // ArrayList removeAll example
        ArrayList<Integer> alist1 = new ArrayList<>(Arrays.asList(1, 2, 3, 4));
        ArrayList<Integer> alist2 = new ArrayList<>(Arrays.asList(2, 4));
        alist1.removeAll(alist2);
        System.out.println("ArrayList after removeAll: " + alist1); // [1,3]
        
        // LinkedList as List reference
        List<Integer> list = new LinkedList<>();
        list.add(10);
        list.add(20);
        System.out.println("List reference LinkedList: " + list); // [10, 20]
    }
}
```

---

# ✅ Final Summary:

- Insertion and Deletion are fast in **LinkedList**.
    
- Random Access is fast in **ArrayList**.
    
- LinkedList requires more **memory** (because of storing references).
    
- You can use **removeIf**, **removeAll**, **addFirst**, **addLast** methods in LinkedList.
    
- LinkedList can act like **List**, **Stack**, **Queue**.
    
