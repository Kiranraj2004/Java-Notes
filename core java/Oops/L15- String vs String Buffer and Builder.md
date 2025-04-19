
## 🔤 **1. String**

- **Immutable**: Once created, it cannot be changed.
    
- **Stored in the String Pool**: Especially when created using literals.
    
- **Performance**: Poor when performing repetitive modifications because each operation creates a new object.
    
- **Thread Safety**: Yes (because it’s immutable, it’s inherently thread-safe).
    
- **Use Case**: Use it when you don’t need to modify the string (e.g., constant text, labels).
    

### ✨ Example:

```java
String s = "Hello";
s.concat(" World"); // Won't change original s
System.out.println(s); // Prints: Hello
```

---

## 🧱 **2. StringBuilder**

- **Mutable**: Can be modified without creating new objects.
    
- **Not Thread Safe**: Multiple threads modifying it simultaneously can cause issues.
    
- **Stored in Heap Memory**
    
- **Performance**: Best for single-threaded environments due to no synchronization overhead.
    
- **Use Case**: Ideal when you need to frequently modify strings in a **single-threaded** program.
    

### ✨ Example:

```java
StringBuilder sb = new StringBuilder("Hello");
sb.append(" World");
System.out.println(sb); // Prints: Hello World
```

---

## 🧵 **3. StringBuffer**

- **Mutable**: Similar to StringBuilder.
    
- **Thread Safe**: All methods are synchronized.
    
- **Stored in Heap Memory**
    
- **Performance**: Slower than StringBuilder because of synchronization overhead.
    
- **Use Case**: Suitable for **multi-threaded** environments where thread safety is required.
    

### ✨ Example:

```java
StringBuffer sb = new StringBuffer("Hello");
sb.append(" World");
System.out.println(sb); // Prints: Hello World
```

---

## 🧪 **Performance Testing Summary**

A loop was used to append text thousands of times using each class:

- **String**: Very slow (many objects created).
    
- **StringBuilder**: Fastest in single-threaded use.
    
- **StringBuffer**: Slightly slower than StringBuilder due to thread safety.
    

---

## 🔄 Internal Working of StringBuilder

- Starts with a character array of default capacity (16).
    
- Appends go into the array.
    
- If array fills, it resizes (usually doubles the size).
    
- All operations return the same object (chaining possible).
    

---

## 📋 Use Case Comparison

|Feature|String|StringBuilder|StringBuffer|
|---|---|---|---|
|Mutable|❌ No|✅ Yes|✅ Yes|
|Thread Safe|✅ Yes|❌ No|✅ Yes|
|Performance|❌ Slow|✅ Fast|⚠️ Moderate|
|Storage|String Pool|Heap|Heap|
|Use Case|Constants|Single Thread|Multi Thread|

---

If you'd like, I can also help you write some example Java code based on this video to reinforce your understanding. Want to try that?