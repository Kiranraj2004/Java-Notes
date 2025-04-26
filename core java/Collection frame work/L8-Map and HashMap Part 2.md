
# ✍️ Detailed Notes: HashMap Internal Working, Collision Handling, HashCode & Equals

---

## 1. **Basic HashMap Behavior**

- `HashMap` stores data in `(key, value)` pairs.
    
- It uses the **hashCode** of the key to calculate an **index** in the internal array.
    
- Formula:  
    ➔ `index = hashCode(key) % array_size`  
    (array size is initially 16 by default).
    

---

## 2. **When there is No Collision**

- If two keys generate different indexes → each key-value is stored at its unique place.
    
- Operations like `put()` and `get()` work in **O(1)** (constant time).
    

---

## 3. **What is a Collision?**

- **Collision** happens when **two different keys** generate **the same index**.
    
- In that case, HashMap handles it internally:
    
    - It uses a **LinkedList** at that bucket (index) to store multiple entries.
        
    - First the earlier object is stored, then the next object is linked after it, and so on.
        
- If **too many** elements (≥ 8) come at the same bucket after collision,  
    → HashMap converts **LinkedList into a Red-Black Tree** (for faster search in O(log N)).
    

---

## 4. **Example given**

Imagine we store fruits and their quantities:

|Fruit|Quantity|
|---|---|
|Apple|50|
|Banana|30|
|Orange|80|
|Grape|20|

- Apple goes to index 9.
    
- Banana goes to index 4.
    
- Orange goes to index 14.
    
- Grape **also** goes to index 14 (collision with Orange).
    
- So, at index 14, a linked list will store: Orange → Grape.
    

---

## 5. **How Retrieval Happens?**

- If we call `map.get("Grape")`:
    
    - Calculate **hashCode** of "Grape".
        
    - Find **index** (hashCode % size).
        
    - Traverse the **LinkedList** at that index.
        
    - Use **equals() method** to check:
        
        - Is current node's key equal to "Grape"?
            
        - If yes → return its value.
            

---

## 6. **Importance of hashCode() and equals()**

- `hashCode()` is used to find the **bucket index**.
    
- `equals()` is used to **find the exact key** inside the bucket (when collision happens).
    

---

## 7. **Problem with Custom Objects as Key**

Suppose, now we use a **custom class** like `Student` or `Person` as the key.

- By default, Java uses `Object` class methods:
    
    - `hashCode()` is based on memory address.
        
    - `equals()` checks memory address (reference equality).
        
- This causes a problem:
    
    - Even if two different `Person` objects have the **same data** (name, id),  
        Java will treat them as **different** because their memory address is different.
        

---

## 8. **Example Given**

We create 3 objects:

|Object|Name|ID|
|---|---|---|
|p1|Alice|1|
|p2|Bob|2|
|p3|Alice|1 (again)|

Now:

- p1 and p3 **look identical** (same name and id).
    
- But `p1 != p3` in Java because their memory addresses are different unless you override `hashCode()` and `equals()` properly.
    

---

## 9. **Real Solution**

✅ **Override `hashCode()` and `equals()`** inside your custom class (`Person`, `Student` etc.)

- So that equality is based on **values** (name, id) not memory address.
    

---

# ✅ Full Java Code (with Output)

Here’s the complete Java program explained above:

```java
import java.util.HashMap;
import java.util.Map;
import java.util.Objects;

class Person {
    private String name;
    private int id;

    public Person(String name, int id) {
        this.name = name;
        this.id = id;
    }

    // Generate Getters
    public String getName() {
        return name;
    }

    public int getId() {
        return id;
    }

    // Overriding hashCode() and equals()
    @Override
    public int hashCode() {
        return Objects.hash(name, id); // Based on name and id fields
    }

    @Override
    public boolean equals(Object o) {
        if (this == o) return true; // same memory reference
        if (o == null || getClass() != o.getClass()) return false; // different type
        Person person = (Person) o;
        return id == person.id && Objects.equals(name, person.name); // compare id and name
    }
}

public class HashMapExample {
    public static void main(String[] args) {

        Map<Person, String> map = new HashMap<>();

        Person p1 = new Person("Alice", 1);
        Person p2 = new Person("Bob", 2);
        Person p3 = new Person("Alice", 1); // same as p1 (data wise)

        map.put(p1, "Engineer");
        map.put(p2, "Designer");
        map.put(p3, "Manager"); // Should overwrite p1's value if equals/hashCode are correctly overridden

        // Now let's print the map
        for (Map.Entry<Person, String> entry : map.entrySet()) {
            Person person = entry.getKey();
            String designation = entry.getValue();
            System.out.println(person.getName() + " (" + person.getId() + ") : " + designation);
        }
    }
}
```

---

# 🖨️ OUTPUT:

```
Bob (2) : Designer
Alice (1) : Manager
```

✅ As you see, even though `p3` was a **new object**,  
→ Because we correctly overrode `equals()` and `hashCode()`,  
→ It updated the value of "Alice" from "Engineer" to "Manager".

---

# ✨ Summary

|Concept|Key Point|
|---|---|
|HashMap uses hashCode()|to find bucket index|
|HashMap uses equals()|to match key when collision happens|
|Default hashCode()/equals()|works on memory address (not data)|
|Custom Objects as Key|Must override hashCode() and equals()|
|Java 8 HashMap Improvement|LinkedList ➔ Tree (after 8 items at one bucket)|
