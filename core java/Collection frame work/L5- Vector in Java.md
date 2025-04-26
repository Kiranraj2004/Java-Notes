
## 1. **Introduction to Vector**

- **Vector** is part of `java.util` package.
    
- It is a **legacy class**, meaning it **existed before** the Collection Framework.
    
- **Implements:** `List` interface (after Collection Framework came).
    
- **Special Feature:**  
    → It is **synchronized**, which means it is **thread-safe**.  
    → Unlike **ArrayList** and **LinkedList** which are **not synchronized**.
    

---

## 2. **Why use Vector?**

- If you are in a **multi-threaded environment** (i.e., multiple threads accessing the same list), then **use Vector**.
    
- If you are in a **single-threaded environment**, **prefer ArrayList** instead, because synchronization adds unnecessary overhead (locking/unlocking).
    

---

## 3. **Features of Vector**

- **Dynamic Array:** Like ArrayList, Vector internally uses an array that grows as needed.
    
- **Synchronized:** All methods are synchronized to ensure thread safety.
    
- **Legacy Class:** Existed before Collection Framework but later adapted.
    
- **Random Access:** Elements can be accessed directly via index.
    

---

## 4. **Constructors of Vector**

There are **4 constructors**:

|Constructor|Description|
|:--|:--|
|`Vector()`|Default capacity = 10|
|`Vector(int initialCapacity)`|Sets an initial capacity|
|`Vector(int initialCapacity, int capacityIncrement)`|Sets capacity and how much to increment when full|
|`Vector(Collection<? extends E> c)`|Creates vector from another collection|

---

## 5. **Example - Creating a Vector**

### Simple Vector Creation

```java
import java.util.Vector;

public class VectorDemo {
    public static void main(String[] args) {
        Vector<Integer> vector = new Vector<>();
        System.out.println(vector.capacity()); // Output: 10
    }
}
```

---

### Constructor with Initial Capacity

```java
Vector<Integer> vector = new Vector<>(12);
System.out.println(vector.capacity()); // Output: 12
```

---

### Constructor with Capacity Increment

```java
public class VectorCapacityIncrement {
    public static void main(String[] args) {
        Vector<Integer> vector = new Vector<>(5, 3);

        // Adding 5 elements
        for (int i = 0; i < 5; i++) {
            vector.add(i);
        }
        System.out.println("Capacity after 5 elements: " + vector.capacity()); // Output: 5

        // Adding 1 more element
        vector.add(5);
        System.out.println("Capacity after 6th element: " + vector.capacity()); // Output: 8

        // Adding up to 8 elements (no change yet)
        vector.add(6);
        vector.add(7);
        System.out.println("Capacity after 8 elements: " + vector.capacity()); // Output: 8

        // Adding one more element (should grow)
        vector.add(8);
        System.out.println("Capacity after 9th element: " + vector.capacity()); // Output: 11
    }
}
```

---

### Constructor with Collection

```java
import java.util.*;

public class VectorFromCollection {
    public static void main(String[] args) {
        LinkedList<Integer> linkedList = new LinkedList<>();
        linkedList.add(2);
        linkedList.add(3);

        Vector<Integer> vector = new Vector<>(linkedList);
        System.out.println(vector); // Output: [2, 3]
    }
}
```

---

## 6. **Common Methods of Vector**

|Method|Description|
|:--|:--|
|`add(E e)`|Add element at end|
|`add(int index, E element)`|Add at specific index|
|`get(int index)`|Retrieve element by index|
|`set(int index, E element)`|Replace element at index|
|`remove(int index)`|Remove by index|
|`remove(Object o)`|Remove by object|
|`size()`|Current number of elements|
|`isEmpty()`|Checks if empty|
|`clear()`|Remove all elements|

---

## 7. **Example - Using Vector Methods**

```java
import java.util.Vector;

public class VectorMethodsDemo {
    public static void main(String[] args) {
        Vector<Integer> vector = new Vector<>();

        vector.add(1);
        vector.add(2);
        vector.add(3);
        System.out.println(vector); // [1, 2, 3]

        vector.add(1, 10);
        System.out.println(vector); // [1, 10, 2, 3]

        System.out.println(vector.get(2)); // 2

        vector.set(2, 20);
        System.out.println(vector); // [1, 10, 20, 3]

        vector.remove(1);
        System.out.println(vector); // [1, 20, 3]

        System.out.println("Size: " + vector.size()); // Size: 3
        System.out.println("Is Empty: " + vector.isEmpty()); // false

        vector.clear();
        System.out.println(vector); // []
    }
}
```

---

## 8. **Internal Working of Vector**

- When the number of elements exceeds the capacity, **Vector doubles its size** (unless `capacityIncrement` is specified).
    
- It **creates a new array**, copies all elements into it.
    

---

## 9. **Synchronization and Performance**

- **All methods are synchronized** (you can check by opening source code: methods are marked `synchronized`).
    
- **Only one thread** can access Vector methods at a time.
    
- **Good for multi-threading** ❗
    
- **Bad for single-threaded programs** — unnecessary overhead due to locking.
    

---

## 10. **Difference Between ArrayList and Vector**

|ArrayList|Vector|
|:--|:--|
|Not synchronized|Synchronized|
|Faster|Slower (due to thread-safety)|
|Use for Single-threaded apps|Use for Multi-threaded apps|
|Grows by 50%|Doubles capacity|

---

## 11. **Thread-Safety Example**

### ❌ ArrayList (Problem of Thread Safety)

```java
import java.util.*;

public class ArrayListThreadProblem {
    public static void main(String[] args) throws InterruptedException {
        List<Integer> list = new ArrayList<>();

        Runnable task = () -> {
            for (int i = 0; i < 1000; i++) {
                list.add(i);
            }
        };

        Thread t1 = new Thread(task);
        Thread t2 = new Thread(task);

        t1.start();
        t2.start();

        t1.join();
        t2.join();

        System.out.println("Size: " + list.size());
    }
}
```

#### **Expected Size = 2000, but Real Output:**

- Random sizes like **1566**, **1461**, etc.
    
- Reason: **ArrayList is not synchronized.**
    

---

### ✅ Vector (Thread Safe)

```java
import java.util.*;

public class VectorThreadSafe {
    public static void main(String[] args) throws InterruptedException {
        List<Integer> list = new Vector<>();

        Runnable task = () -> {
            for (int i = 0; i < 1000; i++) {
                list.add(i);
            }
        };

        Thread t1 = new Thread(task);
        Thread t2 = new Thread(task);

        t1.start();
        t2.start();

        t1.join();
        t2.join();

        System.out.println("Size: " + list.size());
    }
}
```

#### **Expected and Real Output:**

```
Size: 2000
```

- No issue — because **Vector ensures thread-safety**.
    

---

# 📝 Final Quick Summary:

- **Vector = Legacy + Thread-safe + Dynamic array**.
    
- For **multi-threaded** apps, prefer **Vector**.
    
- For **single-threaded** apps, prefer **ArrayList**.
    
- Remember: **Synchronization = Slow performance** if unnecessary.
    

