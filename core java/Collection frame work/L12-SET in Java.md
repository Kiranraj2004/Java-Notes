
# 📚 SET in Java — Complete Notes + Code Examples

---

## 1. What is a Set?

- `Set` is a collection **that does not allow duplicate elements**.
    
- **Based on Map internally**, so:
    
    - **Time complexity** for insertion and search: **O(1)** (HashSet based).
        
- Operations are **faster** compared to List when uniqueness is needed.
    

---

## 2. Set Implementations:

- **HashSet** – no order maintained (internally uses HashMap).
    
- **LinkedHashSet** – maintains insertion order.
    
- **TreeSet** – maintains elements in **sorted order** (Red-Black tree internally).
    
- **EnumSet** – specialized set for enum types.
    

---

## 3. Basic Code for HashSet

```java
import java.util.*;

public class SetOverview {
    public static void main(String[] args) {
        Set<Integer> set = new HashSet<>();
        
        set.add(12);
        set.add(12); // duplicate, will not be added
        set.add(67);
        
        System.out.println(set); // Output: [67, 12] (order not guaranteed)
    }
}
```

---

## 4. Set Methods:

- `add()`
    
- `remove()`
    
- `clear()`
    
- `contains()`
    
- `size()`
    
- `isEmpty()`
    
- `addAll()`
    
- **Iteration**: Using for-each loop.
    

Example:

```java
System.out.println(set.contains(12)); // true
set.remove(67); // removes 67
set.clear();    // clears the set
System.out.println(set.isEmpty()); // true
```

---

## 5. Internal Working of HashSet:

- HashSet internally uses a **HashMap**.
    
- Keys of the map act as elements of the Set.
    
- **Dummy values** are used inside HashMap (like a fixed object).
    

---

## 6. TreeSet Example (Sorted Order)

```java
import java.util.*;

public class TreeSetExample {
    public static void main(String[] args) {
        Set<Integer> treeSet = new TreeSet<>();
        treeSet.add(12);
        treeSet.add(67);
        treeSet.add(11);
        
        System.out.println(treeSet); // Output: [11, 12, 67] - sorted order
    }
}
```

---

## 7. Thread Safety in Set:

- **HashSet**, **LinkedHashSet**, **TreeSet** ➔ **NOT thread-safe** by default.
    

To make it thread-safe:

```java
Set<Integer> syncSet = Collections.synchronizedSet(new HashSet<>());
```

But if **external synchronization** is needed during iteration:

```java
synchronized(syncSet) {
    for (Integer i : syncSet) {
        System.out.println(i);
    }
}
```

---

## 8. Better Alternative: ConcurrentSkipListSet

- Built-in thread-safe.
    
- Elements are sorted (like TreeSet) but allow concurrent access.
    

Example:

```java
import java.util.concurrent.*;

public class ConcurrentSetExample {
    public static void main(String[] args) {
        Set<Integer> concurrentSet = new ConcurrentSkipListSet<>();
        
        concurrentSet.add(10);
        concurrentSet.add(5);
        concurrentSet.add(20);
        
        System.out.println(concurrentSet); // Output: [5, 10, 20]
    }
}
```

---

## 9. Unmodifiable Set

- Immutable Set creation:
    

```java
Set<Integer> unmodifiableSet = Set.of(1, 2, 3);
// unmodifiableSet.add(4); // Throws UnsupportedOperationException
```

**Note**: Unlike Map, `Set.of` can have more than 10 elements.

You can also use:

```java
Set<Integer> modifiableSet = new HashSet<>(Arrays.asList(1, 2, 3));
Set<Integer> unmodSet = Collections.unmodifiableSet(modifiableSet);
```

---

## 10. NavigableSet and SortedSet

- `TreeSet` implements `NavigableSet`, which extends `SortedSet`.
    
- **Methods available**: `ceiling()`, `floor()`, `higher()`, `lower()`, etc.
    

Example:

```java
NavigableSet<Integer> navSet = new TreeSet<>();
navSet.add(10);
navSet.add(20);
navSet.add(30);

System.out.println(navSet.ceiling(25)); // Output: 30
System.out.println(navSet.floor(25));   // Output: 20
```

---

# 📚 CopyOnWriteArraySet and ConcurrentSkipListSet

---

## 11. Why CopyOnWriteArraySet?

- Used for **read-heavy** operations where **modifications are rare**.
    
- Copy-on-write:
    
    - A **new copy** of the set is created on each modification.
        
- It **avoids ConcurrentModificationException** during iteration.
    

Example:

```java
import java.util.concurrent.CopyOnWriteArraySet;

public class CopyOnWriteSetExample {
    public static void main(String[] args) {
        CopyOnWriteArraySet<Integer> cowSet = new CopyOnWriteArraySet<>();
        
        for (int i = 1; i <= 5; i++) {
            cowSet.add(i);
        }

        System.out.println(cowSet); // [1, 2, 3, 4, 5]

        for (Integer num : cowSet) {
            System.out.print(num + " ");
            cowSet.add(6); // No ConcurrentModificationException
        }
        System.out.println("\n" + cowSet); // [1, 2, 3, 4, 5, 6]
    }
}
```

**Output:**

```
1 2 3 4 5 
[1, 2, 3, 4, 5, 6]
```

---

## 12. Difference between CopyOnWriteArraySet and ConcurrentSkipListSet

|Feature|CopyOnWriteArraySet|ConcurrentSkipListSet|
|---|---|---|
|Thread Safety|Yes|Yes|
|Order|Insertion order|Sorted order|
|Performance|Good for Read-heavy|Balanced|
|Modifications during iteration|No reflection until after loop|Might reflect during iteration (weakly consistent)|
|Use Case|Read-mostly scenarios|Both Read/Write intensive|

---

## 13. Example showing **weak consistency** in ConcurrentSkipListSet

```java
import java.util.concurrent.ConcurrentSkipListSet;

public class WeakConsistencyExample {
    public static void main(String[] args) {
        ConcurrentSkipListSet<Integer> skipSet = new ConcurrentSkipListSet<>();
        for (int i = 1; i <= 5; i++) {
            skipSet.add(i);
        }

        for (Integer num : skipSet) {
            System.out.print(num + " ");
            if (num == 5) {
                skipSet.add(6);
            }
        }
        
        System.out.println("\n" + skipSet);
    }
}
```

**Output:**

```
1 2 3 4 5 
[1, 2, 3, 4, 5, 6]
```

- Notice: 6 may **not appear** during iteration!
    

---

# ⚡ Summary:

|Concept|Important Points|
|---|---|
|Set|No duplicates|
|HashSet|No order|
|LinkedHashSet|Insertion order maintained|
|TreeSet|Sorted order|
|EnumSet|Specialized for Enums|
|Collections.synchronizedSet|External synchronization needed|
|ConcurrentSkipListSet|Thread safe + sorted|
|CopyOnWriteArraySet|Thread safe + read-heavy operations|
|Weak consistency|ConcurrentSkipListSet has weak consistency during iteration|

-

### **TreeSet vs LinkedHashSet**

Both `TreeSet` and `LinkedHashSet` are implementations of the `Set` interface in Java, but they differ in terms of their internal structures and the behavior they exhibit.

### **1. TreeSet:**

- **Implementation:** `TreeSet` is a **NavigableSet** that is based on a **Red-Black Tree**.
    
- **Ordering:** It stores elements in a **sorted order**, according to their natural ordering or by a comparator provided at the time of creation.
    
- **Performance:**
    
    - **Time Complexity for Operations:**
        
        - **Add:** O(log n)
            
        - **Remove:** O(log n)
            
        - **Contains:** O(log n)
            
    - The time complexity is logarithmic because of the underlying balanced tree structure.
        
- **Null Elements:** `TreeSet` does **not** allow `null` elements. If you try to add `null`, it will throw a `NullPointerException`.
    
- **Use Case:** Use `TreeSet` when you want to maintain elements in a sorted order.
    

**Example of TreeSet:**

```java
import java.util.*;

public class TreeSetExample {
    public static void main(String[] args) {
        // Creating a TreeSet of integers
        Set<Integer> treeSet = new TreeSet<>();
        
        // Adding elements
        treeSet.add(10);
        treeSet.add(5);
        treeSet.add(20);
        treeSet.add(15);
        
        // Printing elements
        System.out.println("TreeSet: " + treeSet);
        
        // Checking if a particular element is present
        System.out.println("Contains 10? " + treeSet.contains(10));
        
        // Removing an element
        treeSet.remove(5);
        System.out.println("After removing 5: " + treeSet);
        
        // TreeSet is always sorted
    }
}
```

**Output:**

```
TreeSet: [5, 10, 15, 20]
Contains 10? true
After removing 5: [10, 15, 20]
```

### **2. LinkedHashSet:**

- **Implementation:** `LinkedHashSet` is an implementation of the `Set` interface backed by a **HashMap**. It maintains a **doubly-linked list** running through all of its entries.
    
- **Ordering:** It preserves the **insertion order** of the elements. The elements are iterated in the order they were inserted into the set.
    
- **Performance:**
    
    - **Time Complexity for Operations:**
        
        - **Add:** O(1) on average
            
        - **Remove:** O(1) on average
            
        - **Contains:** O(1) on average
            
    - The time complexity for operations is constant because of the hash-based structure.
        
- **Null Elements:** `LinkedHashSet` allows `null` elements.
    
- **Use Case:** Use `LinkedHashSet` when you need to maintain the order of insertion, or when the order in which elements are added is important.
    

**Example of LinkedHashSet:**

```java
import java.util.*;

public class LinkedHashSetExample {
    public static void main(String[] args) {
        // Creating a LinkedHashSet of integers
        Set<Integer> linkedHashSet = new LinkedHashSet<>();
        
        // Adding elements
        linkedHashSet.add(10);
        linkedHashSet.add(5);
        linkedHashSet.add(20);
        linkedHashSet.add(15);
        
        // Printing elements
        System.out.println("LinkedHashSet: " + linkedHashSet);
        
        // Checking if a particular element is present
        System.out.println("Contains 10? " + linkedHashSet.contains(10));
        
        // Removing an element
        linkedHashSet.remove(5);
        System.out.println("After removing 5: " + linkedHashSet);
        
        // Elements maintain insertion order
    }
}
```

**Output:**

```
LinkedHashSet: [10, 5, 20, 15]
Contains 10? true
After removing 5: [10, 20, 15]
```

### **Key Differences Between TreeSet and LinkedHashSet:**

|Feature|**TreeSet**|**LinkedHashSet**|
|---|---|---|
|**Ordering**|Sorted (natural or by comparator)|Maintains insertion order|
|**Implementation**|Red-Black Tree (NavigableSet)|HashMap with a doubly-linked list|
|**Null Elements**|Does not allow `null` elements|Allows `null` elements|
|**Performance (Add/Remove/Contains)**|O(log n)|O(1) on average|
|**Use Case**|When you need sorted elements|When insertion order is important|

### **Conclusion:**

- **Choose TreeSet** when you need your elements to be sorted.
    
- **Choose LinkedHashSet** when you need to preserve the order of insertion and still have the fast lookup and removal operations of a hash set.