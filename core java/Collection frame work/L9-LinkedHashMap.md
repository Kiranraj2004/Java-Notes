
# 🧠 LinkedHashMap Detailed Notes (with examples)

---

## 1. What is a LinkedHashMap?

- `LinkedHashMap` is a subclass of `HashMap`.
    
- **Main difference** from `HashMap`:  
    It **maintains the insertion order** of elements.
    

---

## 2. Basic LinkedHashMap Example

```java
import java.util.HashMap;
import java.util.LinkedHashMap;
import java.util.Map;

public class LinkedHashMapDemo {
    public static void main(String[] args) {
        // Using HashMap
        Map<String, String> hashMap = new HashMap<>();
        hashMap.put("Orange", "L");
        hashMap.put("Guava", "G");

        System.out.println("HashMap Output:");
        for (Map.Entry<String, String> entry : hashMap.entrySet()) {
            System.out.println(entry.getKey() + " -> " + entry.getValue());
        }

        System.out.println();

        // Using LinkedHashMap
        Map<String, String> linkedHashMap = new LinkedHashMap<>();
        linkedHashMap.put("Orange", "L");
        linkedHashMap.put("Guava", "G");

        System.out.println("LinkedHashMap Output:");
        for (Map.Entry<String, String> entry : linkedHashMap.entrySet()) {
            System.out.println(entry.getKey() + " -> " + entry.getValue());
        }
    }
}
```

### Output:

```
HashMap Output:
Guava -> G
Orange -> L

LinkedHashMap Output:
Orange -> L
Guava -> G
```

> ⚡ **HashMap doesn't guarantee order**, but LinkedHashMap maintains **insertion order**.

---

## 3. How LinkedHashMap Maintains Order?

- **Internally uses** a **Doubly Linked List**.
    
- Each entry (key-value pair) is part of this linked list.
    
- Maintains the **order of insertion** OR **order of access** based on a flag (`accessOrder`).
    

---

## 4. LinkedHashMap Constructors

```java
// Basic Constructor
LinkedHashMap<K, V> linkedHashMap = new LinkedHashMap<>();

// Constructor with initial capacity and load factor
LinkedHashMap<K, V> linkedHashMap = new LinkedHashMap<>(int initialCapacity, float loadFactor);

// Constructor with accessOrder
LinkedHashMap<K, V> linkedHashMap = new LinkedHashMap<>(int initialCapacity, float loadFactor, boolean accessOrder);
```

|Parameter|Meaning|
|---|---|
|`initialCapacity`|Initial array size (like HashMap)|
|`loadFactor`|When to resize the map|
|`accessOrder`|`false`: insertion order, `true`: access order|

---

## 5. Understanding `accessOrder`

- **Default (`false`)** → maintains **insertion order**.
    
- **If `true`**, **accessing** (get/put) a key will **move it to end** of the list.
    
- Useful for **Least Recently Used (LRU) cache** systems.
    

### Example of `accessOrder = true`

```java
import java.util.LinkedHashMap;
import java.util.Map;

public class LinkedHashMapAccessOrderDemo {
    public static void main(String[] args) {
        LinkedHashMap<String, Integer> linkedMap = new LinkedHashMap<>(5, 0.75f, true);

        linkedMap.put("Orange", 1);
        linkedMap.put("Apple", 2);
        linkedMap.put("Guava", 3);

        System.out.println("Before accessing:");
        System.out.println(linkedMap);

        // Access "Apple"
        linkedMap.get("Apple");

        System.out.println("After accessing Apple:");
        System.out.println(linkedMap);

        // Access "Orange"
        linkedMap.get("Orange");

        System.out.println("After accessing Orange:");
        System.out.println(linkedMap);
    }
}
```

### Output:

```
Before accessing:
{Orange=1, Apple=2, Guava=3}
After accessing Apple:
{Orange=1, Guava=3, Apple=2}
After accessing Orange:
{Guava=3, Apple=2, Orange=1}
```

> ⚡ Accessing a key moves it to the end.

---

## 6. Special Methods in LinkedHashMap

- `getOrDefault(key, defaultValue)`  
    → Return value if present, else return the `defaultValue`.
    
- `putIfAbsent(key, value)`  
    → Only insert if key is **NOT already present**.
    

---

## 7. LRU Cache Using LinkedHashMap

### Full Code

```java
import java.util.LinkedHashMap;
import java.util.Map;

public class LRUCache<K, V> extends LinkedHashMap<K, V> {

    private int capacity; // Maximum number of entries allowed

    // Constructor
    public LRUCache(int capacity) {
        super(capacity, 0.75f, true); // accessOrder = true
        this.capacity = capacity;
    }

    // Override this method to remove eldest entry
    @Override
    protected boolean removeEldestEntry(Map.Entry<K, V> eldest) {
        return size() > capacity;
    }

    // Demo main method
    public static void main(String[] args) {
        LRUCache<String, Integer> studentMap = new LRUCache<>(3);

        studentMap.put("Bob", 99);
        studentMap.put("Alice", 89);
        studentMap.put("Ram", 91);

        System.out.println("After adding 3 students:");
        System.out.println(studentMap);

        // Add one more student -> LRU will be removed
        studentMap.put("Vipul", 89);
        System.out.println("\nAfter adding Vipul:");
        System.out.println(studentMap);

        // Access "Ram" to make it recently used
        studentMap.get("Ram");

        // Add another student
        studentMap.put("John", 85);
        System.out.println("\nAfter accessing Ram and adding John:");
        System.out.println(studentMap);
    }
}
```

### Output:

```
After adding 3 students:
{Bob=99, Alice=89, Ram=91}

After adding Vipul:
{Alice=89, Ram=91, Vipul=89}

After accessing Ram and adding John:
{Vipul=89, Ram=91, John=85}
```

> ⚡ `Bob` was removed first when `Vipul` added.  
> ⚡ `Alice` was removed when `John` added (since `Ram` was recently accessed).

---

# 🚀 Important Points to Remember

- LinkedHashMap internally uses a doubly linked list.
    
- Use `accessOrder = true` to make it **access order** instead of insertion order.
    
- Overhead: Slightly **slower** and **more memory** usage compared to HashMap.
    
- LinkedHashMap is **not thread-safe** (use `Collections.synchronizedMap()` if needed).
    
- Useful for making **LRU Caches**, **caching mechanisms**, **order sensitive maps**.
    

---

