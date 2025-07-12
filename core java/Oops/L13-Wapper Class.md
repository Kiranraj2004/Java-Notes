
## 🔍 Is Java a Pure Object-Oriented Language?

**Short answer:** ❌ No, Java is **not** a _pure_ object-oriented language.

### ✅ Why?

Because Java supports **primitive types** like:

```java
int, float, double, boolean, byte, short, long, char
```

These are **not** objects. That’s why you can’t call methods on them directly like you can on objects.

Example:

```java
int a = 1;
a. // No methods available here
```

But:

```java
String s = "Vipul";
s. // Tons of methods available here
```

So, Java is **object-oriented**, but **not pure** like some languages (e.g., Smalltalk), where **everything is an object**.

---

## 🧱 Primitive Types vs Wrapper Classes

|Primitive Type|Wrapper Class|
|---|---|
|`int`|`Integer`|
|`float`|`Float`|
|`double`|`Double`|
|`boolean`|`Boolean`|
|`char`|`Character`|
|`byte`|`Byte`|
|`short`|`Short`|
|`long`|`Long`|

Example:

```java
int a = 1;         // primitive
Integer b = 1;     // wrapper (autoboxed)
```

Now you can do:

```java
b.toString();      // methods available
```

---

## 🔁 Autoboxing and Unboxing

Java does **automatic conversion** between primitives and their wrapper classes:

- **Autoboxing**: `int` → `Integer`
    
    ```java
    Integer b = 1; // Java does: Integer.valueOf(1)
    ```
    
- **Unboxing**: `Integer` → `int`
    
    ```java
    int c = b; // Java does: b.intValue()
    ```
    

So, this works seamlessly:

```java
Integer x = 5;
int y = x;  // auto-unboxed
```

---

## 🧠 Stack vs Heap (Memory)

- **Primitive variables** are stored in the **stack**.
    
- **Objects** (like `Integer`, `String`, `List`, etc.) are stored in the **heap**, and the variable holds a **reference (pointer)**.
    

---

## 🧪 Why Wrapper Classes Are Important

Some Java APIs (like `Collections`) **only support objects**, not primitives:

```java
List<Integer> list = new ArrayList<>(); // ✅
List<int> list = new ArrayList<>();     // ❌ Not allowed
```

---

## 🔁 Method Calls and Object References

When you pass an object (like `Student`) to a method:

- You pass the **reference (address)**, not the actual object.
    
- But reassigning that reference in the method **doesn’t change** the original reference.
    

Example:

```java
void updateStudent(Student s) {
    s = new Student();  // This changes only the local copy of reference
    s.id = 2;
}

Student a = new Student();
a.id = 1;
updateStudent(a);
System.out.println(a.id);  // Output: 1 (not 2)
```

However, if you **mutate** the object (without reassigning):

```java
void updateStudent(Student s) {
    s.id = 2;
}

Student a = new Student();
a.id = 1;
updateStudent(a);
System.out.println(a.id);  // Output: 2
```

So, **changing fields works**, but **reassigning the reference doesn’t** affect the original.

---

## 🔍 Object Equality: `==` vs `.equals()`

Java provides two ways to compare objects:

---

### 🔸 1. **`==` Operator (Reference Equality)**

- Checks whether **two references point to the same object** in memory.
    
- Does **not compare content**.
    

#### 📌 Example:

```java
String s1 = new String("hello");
String s2 = new String("hello");

System.out.println(s1 == s2);      // false (different objects)
System.out.println(s1.equals(s2)); // true  (same content)
```

Here, `s1` and `s2` are two different objects in memory, so `==` returns `false`, but their contents are equal, so `.equals()` returns `true`.

---

### 🔸 2. **`.equals()` Method (Content Equality)**

- Defined in `Object` class.
    
- Can be **overridden** by classes to compare the **actual content** of objects.
    
- Default implementation in `Object` compares references (like `==`), but most classes (e.g., `String`, `Integer`) **override** it to compare content.
    

#### 📌 Example:

```java
Integer a = new Integer(100);
Integer b = new Integer(100);

System.out.println(a == b);      // false (different references)
System.out.println(a.equals(b)); // true  (same integer value)
```

---

## 🧠 Behind the Scenes

|Comparison Type|Checks|When to Use|
|---|---|---|
|`==`|Reference (memory address)|You want to know if two variables refer to the same object|
|`.equals()`|Content (logical equality)|You want to compare the actual content or value|

---

### 🧪 Example with Custom Class:

```java
class Person {
    String name;

    Person(String name) {
        this.name = name;
    }

    // Override equals for content comparison
    public boolean equals(Object o) {
        if (this == o) return true;
        if (!(o instanceof Person)) return false;
        Person p = (Person) o;
        return this.name.equals(p.name);
    }
}

public class Main {
    public static void main(String[] args) {
        Person p1 = new Person("Alice");
        Person p2 = new Person("Alice");

        System.out.println(p1 == p2);      // false
        System.out.println(p1.equals(p2)); // true (because we overrode equals)
    }
}
```

---

## ✅ Summary

|Expression|Meaning|Result (for objects)|
|---|---|---|
|`a == b`|Same memory location?|`true` or `false`|
|`a.equals(b)`|Same content/value?|Depends on `.equals()`|

## ✅ Conclusion

- Java is **object-oriented**, but **not purely** object-oriented due to primitive types.
    
- You can use **wrapper classes** to convert primitives into objects.
    
- Java handles this conversion automatically using **autoboxing/unboxing**.
    
- Be careful with **object references** in methods—they can be a source of confusion!
    
- Always use `.equals()` for comparing objects unless you're sure `==` is what you need.




## 🔍 Primitive Equality in Java: `==` vs `.equals()`

---

### ✅ 1. **`==` with Primitives**

- `==` compares the **actual values** of primitives.
- Works perfectly with all primitive types (`int`, `double`, `char`, `boolean`, etc.)

#### 🔹 Example:

```java
int a = 10;
int b = 10;
System.out.println(a == b); // ✅ true — compares values
```

---

### ❌ 2. **`.equals()` with Primitives — Not Allowed**

- You **cannot** call `.equals()` on primitive types directly.
- Primitives are **not objects**, and `.equals()` is a method from the `Object` class.

#### 🔹 Example:

```java
int a = 10;
// System.out.println(a.equals(10)); // ❌ Compile-time error
```

To use `.equals()`, you must use **wrapper classes** (e.g., `Integer`, `Double`):

```java
Integer a = 10;
Integer b = 10;
System.out.println(a.equals(b)); // ✅ true — compares content
```

---

## ⚠️ Autoboxing and `==` with Wrapper Classes

Java caches some wrapper objects (e.g., `Integer` from -128 to 127):

```java
Integer a = 100;
Integer b = 100;
System.out.println(a == b); // ✅ true — same cached object

Integer x = 200;
Integer y = 200;
System.out.println(x == y); // ❌ false — different objects
System.out.println(x.equals(y)); // ✅ true — same value
```

---

## ✅ Summary Table

| Type        | `==`                         | `.equals()`                    |
|-------------|------------------------------|--------------------------------|
| Primitives  | ✅ Compares values directly  | ❌ Not allowed (compile error) |
| Wrappers    | ✅ Compares references        | ✅ Compares values (overridden) |

---

### ✅ Best Practice:

- Use `==` for **primitive types**.
- Use `.equals()` for **objects** (including wrapper classes like `Integer`, `Double`, etc.) to compare **values**, not references.





### Let's break it down clearly. You're observing the behavior of `==` on **Integer objects**, and it's confusing because:

- `a == b` is `true` when both are `100`
    
- `x == y` is `false` when both are `200`
    

Even though both `a` and `b` and `x` and `y` have the **same values** — so why the different result?

---

## 🔍 The Reason: **Integer Caching in Java**

Java uses a special **Integer cache** for performance.

### 🔹 Caching range: `-128 to 127`

- **Integer values in this range are cached** (i.e., reused).
    
- If you assign a value in this range, Java **reuses** the same object.
    
- Outside this range, **new objects** are created, even if the value is the same.
    

---

### ✅ Example 1: Within Cache Range (−128 to 127)

```java
Integer a = 100;
Integer b = 100;
System.out.println(a == b); // ✅ true — same cached object
```

- `a` and `b` point to the **same object**.
    
- `==` compares **references**, so it's `true`.
    

---

### ❌ Example 2: Outside Cache Range (> 127 or < -128)

```java
Integer x = 200;
Integer y = 200;
System.out.println(x == y); // ❌ false — different objects
```

- `x` and `y` are **two different objects** with the same value.
    
- `==` compares **references**, so it's `false`.
    
- But:
    

```java
System.out.println(x.equals(y)); // ✅ true — compares values
```

- `.equals()` compares **values**, not memory references.
    

---

### 🔧 Behind the scenes:

```java
Integer a = 100;  // uses Integer.valueOf(100) → returns cached object
Integer x = 200;  // uses Integer.valueOf(200) → creates a new object
```

The `Integer.valueOf(int i)` method checks the cache:

```java
if (i >= -128 && i <= 127)
    return cached[i + 128];
else
    return new Integer(i);
```

---

## ✅ Summary

|Value|Cached?|`==` Result (if same value)|
|---|---|---|
|`100`|✅ Yes|`true` (same object)|
|`200`|❌ No|`false` (different objects)|

---

Let me know if you want to explore the source code of `Integer.valueOf()` or write a demo!