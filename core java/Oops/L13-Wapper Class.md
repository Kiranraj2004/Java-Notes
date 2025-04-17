
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

- `==` checks **reference equality** (are they the same object in memory).
    
- `.equals()` checks **value equality** (if the objects are meaningfully equal).
    

```java
Integer a = 100;
Integer b = 100;

System.out.println(a == b);        // true (cached in Integer pool)
System.out.println(a.equals(b));   // true

Integer x = 200;
Integer y = 200;

System.out.println(x == y);        // false (different objects)
System.out.println(x.equals(y));   // true
```

---

## ✅ Conclusion

- Java is **object-oriented**, but **not purely** object-oriented due to primitive types.
    
- You can use **wrapper classes** to convert primitives into objects.
    
- Java handles this conversion automatically using **autoboxing/unboxing**.
    
- Be careful with **object references** in methods—they can be a source of confusion!
    
- Always use `.equals()` for comparing objects unless you're sure `==` is what you need.
    

---

Would you like a visual diagram for how object references work in method calls or how stack/heap memory is structured in these examples?