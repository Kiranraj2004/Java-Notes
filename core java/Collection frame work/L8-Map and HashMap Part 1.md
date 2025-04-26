![[Map interface.png]]


# 📚 Detailed Notes on Map and HashMap

## 1. **Introduction to Map**

- `Map` is **not** a part of the `Collection` hierarchy (does not extend `Collection` interface).
    
- It is a **separate interface** for storing **key-value pairs**.
    
- Examples to understand Map:
    
    - **Dictionary** → Word (Key) → Meaning (Value)
        
    - **Roll Number system** → Roll Number (Key) → Student Name (Value)
        

---

## 2. **Key Characteristics of Map**

- **Key-Value Pair**: Every entry in Map stores two things: a Key and a Value.
    
- **Unique Keys**:
    
    - No two entries can have the same key.
        
    - **Values** can be **duplicated** but **keys must be unique**.
        
- **One Value per Key**: Each key maps to exactly one value.
    
- Some Map implementations maintain insertion order (like `LinkedHashMap`), but **HashMap** does **NOT guarantee any order**.
    

---

## 3. **HashMap Overview**

- `HashMap` is one of the most commonly used **implementations** of `Map`.
    
- It allows storing `null` values and one `null` key.
    
- It does **not** maintain the insertion order.
    

---

# 🧑‍💻 Full Code with Explanation and Expected Output

```java
import java.util.HashMap;
import java.util.Map;
import java.util.Set;

public class HashMapDemo {
    public static void main(String[] args) {
        // Creating a HashMap with Integer as Key and String as Value
        Map<Integer, String> map = new HashMap<>();

        // Inserting key-value pairs using put method
        map.put(1, "Akshit");
        map.put(2, "Neha");
        map.put(3, "Shubham");

        // Printing the entire map
        System.out.println(map);
        // Output: {1=Akshit, 2=Neha, 3=Shubham} (order may vary)

        // Retrieving value by key
        String student = map.get(3);
        System.out.println("Student with roll number 3: " + student);
        // Output: Student with roll number 3: Shubham

        // Trying to get a non-existing key
        String studentNotFound = map.get(69);
        System.out.println("Student with roll number 69: " + studentNotFound);
        // Output: Student with roll number 69: null

        // Checking if a key exists
        boolean hasKey2 = map.containsKey(2);
        System.out.println("Does roll number 2 exist? " + hasKey2);
        // Output: Does roll number 2 exist? true

        // Checking if a value exists
        boolean hasValueShubham = map.containsValue("Shubham");
        System.out.println("Is 'Shubham' present? " + hasValueShubham);
        // Output: Is 'Shubham' present? true

        // Looping through the map using keySet()
        System.out.println("\nLooping using keySet:");
        for (Integer key : map.keySet()) {
            System.out.println("Roll Number: " + key + ", Name: " + map.get(key));
        }
        // Output (order may vary):
        // Roll Number: 1, Name: Akshit
        // Roll Number: 2, Name: Neha
        // Roll Number: 3, Name: Shubham

        // Looping through the map using entrySet()
        System.out.println("\nLooping using entrySet:");
        for (Map.Entry<Integer, String> entry : map.entrySet()) {
            System.out.println("Roll Number: " + entry.getKey() + ", Name: " + entry.getValue());
        }
        // Output (order may vary):
        // Roll Number: 1, Name: Akshit
        // Roll Number: 2, Name: Neha
        // Roll Number: 3, Name: Shubham

        // Modifying all values to uppercase
        for (Map.Entry<Integer, String> entry : map.entrySet()) {
            entry.setValue(entry.getValue().toUpperCase());
        }
        System.out.println("\nAfter converting all names to uppercase:");
        System.out.println(map);
        // Output: {1=AKSHIT, 2=NEHA, 3=SHUBHAM} (order may vary)

        // Demonstrating null key and null value
        map.put(null, "Vipul");
        map.put(null, "Ram");  // This will replace "Vipul" with "Ram"
        map.put(4, null);      // null value is allowed
        map.put(5, null);      // multiple null values are allowed

        System.out.println("\nMap after adding null key and null values:");
        System.out.println(map);
        // Output (order may vary):
        // {null=Ram, 1=AKSHIT, 2=NEHA, 3=SHUBHAM, 4=null, 5=null}
    }
}
```

---

# 📌 Key Points to Remember

- `.put(key, value)` → Insert or replace a key-value pair.
    
- `.get(key)` → Fetch value by key.
    
- `.containsKey(key)` → Check if a key exists.
    
- `.containsValue(value)` → Check if a value exists.
    
- `.keySet()` → Returns a set of all keys (no duplicates).
    
- `.entrySet()` → Returns a set of Map.Entry objects (each having both key and value).
    
- In `HashMap`:
    
    - **One null key is allowed**.
        
    - **Multiple null values are allowed**.
        
    - **Order is not guaranteed**.
        

---

# 🎯 Final Output Summary (Example)

```
{1=Akshit, 2=Neha, 3=Shubham}
Student with roll number 3: Shubham
Student with roll number 69: null
Does roll number 2 exist? true
Is 'Shubham' present? true

Looping using keySet:
Roll Number: 1, Name: Akshit
Roll Number: 2, Name: Neha
Roll Number: 3, Name: Shubham

Looping using entrySet:
Roll Number: 1, Name: Akshit
Roll Number: 2, Name: Neha
Roll Number: 3, Name: Shubham

After converting all names to uppercase:
{1=AKSHIT, 2=NEHA, 3=SHUBHAM}

Map after adding null key and null values:
{null=Ram, 1=AKSHIT, 2=NEHA, 3=SHUBHAM, 4=null, 5=null}
```

---



# 🌟 Detailed Notes on HashMap Internal Working 

---

## 🔹 Basic Map Operations:

- **Replace Operation:**
    
    - When you use `.put(key, newValue)` with an existing key, it **replaces** the old value.
        
    - **Example:**
        
        ```java
        HashMap<Integer, String> map = new HashMap<>();
        map.put(2, "Neha");
        map.put(2, "Mehul");  // Replaces Neha with Mehul
        System.out.println(map);
        ```
        
    - **Output:**
        
        ```
        {2=Mehul}
        ```
        
- **Remove Operation:**
    
    - `.remove(key)` removes the entry by **key**.
        
    - **Example:**
        
        ```java
        HashMap<Integer, String> map = new HashMap<>();
        map.put(31, "Shubham");
        map.remove(31);  // Removes key 31
        System.out.println(map);
        ```
        
    - **Output:**
        
        ```
        {}
        ```
        
- **Another Remove (key, value) method:**
    
    - `.remove(key, value)` removes entry **only if** key maps to the specified value.
        
    - **Example:**
        
        ```java
        HashMap<Integer, String> map = new HashMap<>();
        map.put(31, "Shubham");
        
        boolean removed = map.remove(31, "Nitin");  // Tries to remove 31 mapped to Nitin (wrong value)
        
        System.out.println("Removed? " + removed);
        System.out.println(map);
        ```
        
    - **Output:**
        
        ```
        Removed? false
        {31=Shubham}
        ```
        

---

## 🔹 Performance and Time Complexity:

- **HashMap operations (`put()`, `get()`) are O(1)** in average case.
    
- **Reason:**
    
    - Instead of **linear search** (like a List), HashMap uses a **hash function**.
        
    - You **directly jump** to the index (bucket) where your data is stored.
        
- **Example for List Search (Linear Search):**
    
    ```java
    List<Integer> list = Arrays.asList(12, 23, 34, 45);
    System.out.println(list.contains(34));  // Linear search, O(n)
    ```
    
- **Example for Map Search (Constant Time):**
    
    ```java
    HashMap<Integer, String> map = new HashMap<>();
    map.put(31, "Shubham");
    System.out.println(map.containsKey(31));  // Constant time, O(1)
    ```
    

---

## 🔹 HashMap Internals Overview:

|Component|Description|
|---|---|
|**Key**|Unique identifier|
|**Value**|Data stored corresponding to key|
|**Bucket (Array)**|Internal array where entries (key-value pairs) are stored|
|**Hash Function**|Function that computes index from key|

---

## 🔹 What is a Hash Function?

- Takes an **input (key)** and returns a **fixed-size number** called **hash code**.
    
- **Properties:**
    
    - **Deterministic:** Same input always gives same output.
        
    - **Fixed size:** (Usually 32 bits or 64 bits)
        
    - **Efficient:** Fast to compute.
        

**Hash Code ➡️ Used to determine the bucket (array index)**.

---

## 🔹 How HashMap Stores Data (Step-by-Step):

1. **Hash the Key:**
    
    - Key is passed through a **hash function** to generate a hash code.
        
2. **Find the Index:**
    
    - Apply formula:
        
        ```
        index = hashCode % arraySize
        ```
        
    - Where `%` means **modulus** (remainder).
        
3. **Store in Bucket:**
    
    - Store key-value pair at that index inside the internal array.
        

---

## 🔹 Important:

- **Multiple entries** can exist at **same index** (called **collision**).
    
    - We'll study how **collision resolution** happens later (via **LinkedList** or **Tree**).
        

---

## 🔹 Example Code for Complete Flow:

```java
import java.util.HashMap;

public class HashMapDemo {
    public static void main(String[] args) {
        // Step 1: Create a HashMap
        HashMap<Integer, String> map = new HashMap<>();

        // Step 2: Add entries
        map.put(31, "Shubham");
        map.put(11, "Aksha");
        map.put(2, "Neha");
        
        System.out.println("Initial Map: " + map);

        // Step 3: Replace an existing value
        map.put(2, "Mehul");  // Replace Neha with Mehul
        System.out.println("After Replacing 2: " + map);

        // Step 4: Remove an entry by key
        map.remove(31);
        System.out.println("After Removing key 31: " + map);

        // Step 5: Try removing key-value pair
        boolean removed = map.remove(31, "Nitin");  // Wrong value
        System.out.println("Was (31, Nitin) removed? " + removed);

        // Step 6: Search for a key
        boolean exists = map.containsKey(11);
        System.out.println("Is key 11 present? " + exists);

        // Step 7: Time Complexity Demonstration
        // (compare with List for understanding)
    }
}
```

**Expected Output:**

```
Initial Map: {2=Neha, 11=Aksha, 31=Shubham}
After Replacing 2: {2=Mehul, 11=Aksha, 31=Shubham}
After Removing key 31: {2=Mehul, 11=Aksha}
Was (31, Nitin) removed? false
Is key 11 present? true
```

---

# 🌟 Quick Summary Chart

|Operation|Time Complexity|
|---|---|
|`.put(key, value)`|O(1) average|
|`.get(key)`|O(1) average|
|`.remove(key)`|O(1) average|
|`.containsKey(key)`|O(1) average|
|List `.contains(value)`|O(n)|


## 1. Finding Key in HashMap

- First, **hash code** of the key is generated using Java's **inbuilt `hashCode()` method**.
    
- From that hash code, the **index** is calculated (typically using modulus `%` with array length).
    
- Now, at that index (bucket), we need to **search** for the key-value pair.
    

---

## 2. Why Searching in Array is Needed?

- You might wonder: _“Sir, why search? It’s an array, just fetch the value!”_  
    → No.
    
- Because of **collisions** (same index for different keys), multiple key-value pairs **can exist** at one index.
    
- Therefore, **searching** is necessary even inside a single bucket.
    

---

## 3. What is Stored at Each Bucket (Index)?

- At each index of internal array:
    
    - We **don’t** store simple key-value directly.
        
    - We store a **LinkedList** of key-value pairs (if collisions occur).
        

> 📌 **Data Structure** used = **Linked List** (Before Java 8)  
> 📌 After Java 8, it can be **Linked List** or **Red-Black Tree** (if too many collisions).

---

## 4. What is Collision?

- **Collision** occurs when **two different keys** produce **the same hash** and hence, same index.
    
- Reason: **Hash function** can generate **only finite number** of hash values.
    
- But **inputs are infinite** ⇒ collisions are unavoidable.
    

---

## 5. Example of Collision:

```java
public class SimpleHashExample {
    public static void main(String[] args) {
        String s1 = "ABC";
        String s2 = "CBA";

        int h1 = simpleHash(s1);
        int h2 = simpleHash(s2);

        System.out.println("Hash of " + s1 + ": " + h1);
        System.out.println("Hash of " + s2 + ": " + h2);
    }

    public static int simpleHash(String input) {
        return input.length() * 2;  // Dummy simple hash function
    }
}
```

**Output:**

```
Hash of ABC: 6
Hash of CBA: 6
```

- Even though `"ABC"` and `"CBA"` are different, **hash is same** ⇒ **Collision**.
    

---

## 6. How HashMap Handles Collisions

- If multiple entries are mapped to same bucket:
    
    - They are **chained** in a **Linked List**.
        
- When adding:
    
    - Check if key already exists (to update), else **append new node**.
        
- When searching:
    
    - **Traverse linked list** at that index.
        

---

## 7. From LinkedList to Red-Black Tree

- If **LinkedList becomes too long** (> 8 nodes by default):
    
    - It gets **converted into a Red-Black Tree**.
        
    - To improve search performance from **O(n)** → **O(log n)**.
        

**Quick facts about Red-Black Tree:**

- It's a **Self-balancing Binary Search Tree (BST)**.
    
- Operations like search/insert/delete are **O(log n)**.
    
- Used to avoid worst-case linear time searches.
    

---

## 8. HashMap Resizing & Rehashing

- Initial internal array size = **16**.
    
- **Load Factor** (default) = **0.75**.
    
- When **current number of entries > 16 × 0.75 = 12**, resizing happens.
    
- **Resizing**:
    
    - Double the array size (e.g., 16 → 32).
        
    - **Recalculate** the index for all existing keys (called **Rehashing**).
        

### Constructor Example:

```java
import java.util.HashMap;

public class HashMapConstructorExample {
    public static void main(String[] args) {
        HashMap<Integer, String> map = new HashMap<>(17, 0.5f);

        map.put(1, "One");
        map.put(2, "Two");
        map.put(3, "Three");

        System.out.println(map);
    }
}
```

- Here:
    
    - Initial capacity = **17**.
        
    - Load factor = **0.5**.
        
    - **Rehashing** will happen when size crosses **17 × 0.5 = 8.5 (~9 elements)**.
        

---

## 9. Summary of HashMap Working:

|Step|Action|
|:-:|:-:|
|1|Generate hash code of key|
|2|Calculate index (bucket) from hash|
|3|Search inside the bucket (linked list or tree)|
|4|If key exists → update value|
|5|If not → add new node|
|6|Handle collisions|
|7|Resize and rehash if load factor exceeded|

---

# 🚀 Final Full Example of HashMap Internal Working (Custom Version)

### Full Custom HashMap Code Example:

```java
import java.util.LinkedList;

class CustomHashMap<K, V> {
    private class Node {
        K key;
        V value;
        Node(K key, V value) {
            this.key = key;
            this.value = value;
        }
    }

    private LinkedList<Node>[] buckets;
    private int size = 0;
    private final float loadFactor = 0.75f;

    public CustomHashMap() {
        buckets = new LinkedList[16];
    }

    private int hash(K key) {
        return Math.abs(key.hashCode()) % buckets.length;
    }

    private void rehash() {
        LinkedList<Node>[] oldBuckets = buckets;
        buckets = new LinkedList[oldBuckets.length * 2];
        size = 0;
        for (LinkedList<Node> bucket : oldBuckets) {
            if (bucket != null) {
                for (Node node : bucket) {
                    put(node.key, node.value);
                }
            }
        }
    }

    public void put(K key, V value) {
        int index = hash(key);
        if (buckets[index] == null) {
            buckets[index] = new LinkedList<>();
        }

        for (Node node : buckets[index]) {
            if (node.key.equals(key)) {
                node.value = value;
                return;
            }
        }

        buckets[index].add(new Node(key, value));
        size++;

        if ((float)size / buckets.length > loadFactor) {
            rehash();
        }
    }

    public V get(K key) {
        int index = hash(key);
        LinkedList<Node> bucket = buckets[index];

        if (bucket != null) {
            for (Node node : bucket) {
                if (node.key.equals(key)) {
                    return node.value;
                }
            }
        }
        return null;
    }
}

public class CustomHashMapDemo {
    public static void main(String[] args) {
        CustomHashMap<Integer, String> map = new CustomHashMap<>();

        map.put(31, "Shubham");
        map.put(47, "Aman");
        map.put(63, "Ravi");
        map.put(79, "Vikram");

        System.out.println("Value for key 31: " + map.get(31));
        System.out.println("Value for key 47: " + map.get(47));
        System.out.println("Value for key 79: " + map.get(79));
    }
}
```

### Output:

```
Value for key 31: Shubham
Value for key 47: Aman
Value for key 79: Vikram
```

---

# ✨ Extra Tip:

- **Resizing (rehash) doubles array size**.
    
- **Linked List** → **Tree** (after 8+ nodes in one bucket).
    
- **Hash collisions** handled using chaining (linked list first, tree later).
    

---
