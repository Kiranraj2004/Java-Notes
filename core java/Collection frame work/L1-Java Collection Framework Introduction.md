
---

## 🗂️ Java Collection Framework – 

### 📌 1. **What is a Collection?**

- A **collection** is a **group of elements or objects**.
    
- Real-life analogy: Collection of coins, bottle caps, etc.
    
- In Java, it means a group of **objects like Strings, Integers, etc.**
    

---
## 📚 What is **Collection Framework** in Java?

**Collection Framework** is a **set of classes and interfaces** in Java that helps you **store**, **manage**, and **manipulate** groups of objects **efficiently**.

In simple words:

> **Collection Framework = Pre-built tools to handle groups of data (objects) easily.**

---

# 🎯 Why Collection Framework?

Before Java 1.2, Java had some classes like `Vector`, `Stack`, `Hashtable`, but:

- They were **inconsistent** (worked differently).
    
- There was **no common structure** (no interface to connect them).
    
- **Difficult** to use and remember.
    

👉 So, Java introduced the **Collection Framework** to solve these problems and **standardize** how collections are handled.

---

# 🛠️ What does Collection Framework include?

It includes:

| Part           | What it does                                   | Example                           |
| -------------- | ---------------------------------------------- | --------------------------------- |
| **Interfaces** | Define the basic operations (rules/blueprints) | `List`, `Set`, `Queue`, `Map`     |
| **Classes**    | Actual implementations of those interfaces     | `ArrayList`, `HashSet`, `HashMap` |
| **Algorithms** | Ready-made methods to manipulate collections   | Sorting, Searching, Shuffling     |
### 📌 2. **Why Do We Need a Collection Framework?**

#### 🔙 Before Java 1.2:

- Java had classes like:
    
    - `Vector`
        
    - `Stack`
        
    - `Hashtable`
        
- These were used to handle collections but had **major drawbacks**:
    
    - **Inconsistency** in design.
        
    - **No common interface** – every class worked differently.
        
    - **No interoperability** – difficult to use them together.
        
    - **Hard to remember and use** due to different method names and behaviors.
        

#### ✅ Introduction of Collection Framework (Java 1.2 / Java 2):

- Solved all prior issues by introducing:
    
    - **Common interfaces**
        
    - **Interoperability**
        
    - **Generic methods**
        
    - **Cleaner structure**
        

---

### 📌 3. **Main Goal of Collection Framework**

- Provide a **standard architecture** for manipulating and storing groups of objects.
    
- Enable:
    
    - Writing **generic and reusable methods**
        
    - Managing collections using common methods and behaviors
        

---

### 📌 4. **Core Interfaces in the Collection Framework**

1. **Collection Interface** – _Root interface of most collections_
    
2. **List Interface**
    
    - Ordered collection
        
    - Allows **duplicates**
        
    - Example: `ArrayList`, `LinkedList`
        
3. **Set Interface**
    
    - **No duplicates**
        
    - Unordered (unless using `LinkedHashSet`)
        
    - Example: `HashSet`, `TreeSet`
        
4. **Queue Interface**
    
    - Follows **FIFO** (First In First Out) principle
        
    - Example: `PriorityQueue`, `LinkedList`
        
5. **Deque Interface** _(Double Ended Queue)_
    
    - Can insert and remove from **both ends**
        
    - Example: `ArrayDeque`
        
6. **Map Interface**
    
    - Stores **key-value pairs**
        
    - Not a child of `Collection` interface
        
    - Example: `HashMap`, `TreeMap`, `ConcurrentHashMap`
        

---

### 📌 5. **Hierarchy Overview**

#### 🔸 Collection Framework Hierarchy:

```
java.lang.Iterable
     ↓
Collection (Interface)
     ↓
  --------------------------
  |           |           |
List        Set         Queue
                          ↓
                     Deque, BlockingQueue
```

- **Map** is a **separate hierarchy**, not a subtype of `Collection`.
    
![[collection framework hierarchy.png]]


---

### 📌 6. **Iterable Interface**

- **Root interface** of the entire collection framework.
    
- Located in `java.lang` package.
    
- Any class that implements `Iterable` can be used in **for-each loops**.
    

#### Methods of Iterable:

- `iterator()` – Returns an `Iterator` to iterate over elements.
    

---

### 📌 7. **Collection Interface**

- Root of the **Collection branch**.
    
- Part of `java.util` package.
    
- Cannot be instantiated – it's an **interface**.
    
- Provides **blueprint for basic operations** like:
    
    - `add()`, `remove()`, `size()`, `clear()`, `contains()`, etc.
        

---

### 📌 8. **Summary of Interfaces and Implementations**

|Interface|Key Features|Common Implementations|
|---|---|---|
|List|Ordered, allows duplicates|`ArrayList`, `LinkedList`, `Vector`|
|Set|Unordered, no duplicates|`HashSet`, `LinkedHashSet`, `TreeSet`|
|Queue|FIFO ordering|`PriorityQueue`, `LinkedList`|
|Deque|Double-ended queue|`ArrayDeque`, `LinkedList`|
|Map|Key-value pairs|`HashMap`, `TreeMap`, `Hashtable`|

