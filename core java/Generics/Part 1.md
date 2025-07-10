

## ✅ **What are Generics in Java?**

**Generics** were introduced in **Java 5** to solve problems related to type safety and type casting. They allow classes, interfaces, and methods to operate on objects of various types while providing **compile-time type safety**.

---

## ❌ **Problem Before Generics**

### Example Without Generics:

```java
import java.util.ArrayList;

public class Main {
    public static void main(String[] args) {
        ArrayList list = new ArrayList();  // raw type (no generics)

        list.add("Hello");
        list.add(123);
        list.add(3.14);

        String str = (String) list.get(0);  // OK
        String str2 = (String) list.get(1); // Runtime error: ClassCastException
    }
}
```

### 🔍 Issues:

1. **Type Safety Problem**: Any type of data can be added. No restrictions.
    
2. **Manual Type Casting**: You have to cast the object while retrieving it.
    
3. **Runtime Exceptions**: If cast is invalid, it throws `ClassCastException`.
    

---

## ✅ **Solution: Using Generics**

### Example With Generics:

```java
import java.util.ArrayList;

public class Main {
    public static void main(String[] args) {
        ArrayList<String> list = new ArrayList<>();  // using generics

        list.add("Hello");
        list.add("World");

        // list.add(123);  // Compile-time error

        String s1 = list.get(0);  // No casting required
        String s2 = list.get(1);

        System.out.println(s1 + " " + s2);
    }
}
```

### ✅ Benefits:

- Compile-time **type safety** (can only add Strings).
    
- No **manual type casting**.
    
- Avoids **runtime errors** like `ClassCastException`.
    

---

## 📦 **How Generics Work Internally**

When you write:

```java
ArrayList<String> list = new ArrayList<>();
```

You’re creating a parameterized type where only `String` values can be added to the list.

Internally, `ArrayList` class is declared like this:

```java
public class ArrayList<E> {
    // E is a type parameter
}
```

This is what allows generics to work. The type (`E`) is replaced with `String` during compilation.

---

## ⚠️ **Raw Type Warning**

If you use:

```java
ArrayList list = new ArrayList(); // raw type
```

Modern IDEs like IntelliJ show a **warning**:

> “ArrayList is a raw type. References to generic type ArrayList should be parameterized”

Always use parameterized types to avoid this warning and ensure type safety.

---

## 📦 **Creating a Custom Generic Class**

### Without Generics (Problematic):

```java
class Box {
    Object value;

    public void setValue(Object value) {
        this.value = value;
    }

    public Object getValue() {
        return value;
    }
}
```

### Problem:

```java
Box box = new Box();
box.setValue(1);
String str = (String) box.getValue(); // ClassCastException at runtime
```

---

### ✅ With Generics:

```java
class Box<T> {
    private T value;

    public void setValue(T value) {
        this.value = value;
    }

    public T getValue() {
        return value;
    }
}
```

### Usage:

```java
Box<Integer> intBox = new Box<>();
intBox.setValue(10);
Integer i = intBox.getValue();  // No cast required

Box<String> strBox = new Box<>();
strBox.setValue("Hello");
String s = strBox.getValue();  // Safe
```

---

## ✅ Summary of Key Points

|Feature|Without Generics|With Generics|
|---|---|---|
|Type Safety|❌ No|✅ Yes|
|Type Casting Required|✅ Yes|❌ No|
|Compile-time Checking|❌ No|✅ Yes|
|Risk of Runtime Errors|✅ Yes (ClassCastException)|❌ No|

---

## ✅ Real-life Analogy

Imagine a box that can contain anything (Object). Without specifying the type, you could put anything inside, and risk breaking it when opening. But if you label the box (Generic), you know what to expect and how to handle it safely.
