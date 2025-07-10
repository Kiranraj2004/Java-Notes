
## 📌 1. **Bounded Type Parameters (`extends`)**

### ✅ Problem:

Sometimes, you want to **restrict** the type parameter to a certain type or its subclasses. For example, only allow `Number` or its subclasses (`Integer`, `Double`, etc.).

### 🧾 Syntax:

```java
class Box<T extends Number> {
    private T value;

    public void setValue(T value) {
        this.value = value;
    }

    public T getValue() {
        return value;
    }
}
```

### ✅ Valid:

```java
Box<Integer> intBox = new Box<>();
Box<Double> doubleBox = new Box<>();
```

### ❌ Invalid:

```java
Box<String> strBox = new Box<>(); // ❌ Error: String doesn't extend Number
```

### 🧠 Why `Number`?

All wrapper numeric classes (`Integer`, `Double`, `Float`, `Long`, etc.) **extend `java.lang.Number`**, so this bound ensures the type is numeric.

---

## ✌️ 2. **Multiple Bounds (Class + Interface)**

You can use multiple constraints:

- First must be a **class**
    
- Others must be **interfaces**
    
- Use `extends` for all (even for interfaces)
    

### 🧾 Syntax:

```java
class Box<T extends Number & Printable> {
    private T value;
    public void print() {
        value.print(); // Uses Printable interface method
    }
}
```

### 🧾 Supporting Classes:

```java
interface Printable {
    void print();
}

class MyNumber extends Number implements Printable {
    private int data;
    public MyNumber(int data) { this.data = data; }

    @Override public int intValue() { return data; }
    @Override public long longValue() { return data; }
    @Override public float floatValue() { return data; }
    @Override public double doubleValue() { return data; }

    @Override public void print() {
        System.out.println("MyNumber: " + data);
    }
}
```

### ✅ Usage:

```java
Box<MyNumber> box = new Box<>();
box.setValue(new MyNumber(12));
box.print();  // Output: MyNumber: 12
```

### ❗ Rules:

- You can only use `extends` even for interfaces.
    
- Class must appear **first**, then interfaces.
    

---

## 📋 3. **Generic Interfaces**

Just like classes, interfaces can also be generic.

### 🧾 Example:

```java
interface Container<T> {
    void setItem(T item);
    T getItem();
}
```

### ✅ Implementing with Concrete Type:

```java
class StringContainer implements Container<String> {
    private String item;

    public void setItem(String item) { this.item = item; }
    public String getItem() { return item; }
}
```

### ✅ Keeping it Generic:

```java
class GenericContainer<T> implements Container<T> {
    private T item;

    public void setItem(T item) { this.item = item; }
    public T getItem() { return item; }
}
```

---

## 🧾 4. **Enums Are Already Type-Safe**

Enums in Java provide **built-in type safety**.

### ✅ Example:

```java
enum Day { MONDAY, TUESDAY, WEDNESDAY }

Day d = Day.MONDAY; // ✅ OK
```

### ❌ Invalid:

```java
d = 1;         // ❌ Error
d = "Monday";  // ❌ Error
```

> Enums ensure only valid predefined constants are used.

---

## 🛠️ 5. **Generic Constructor**

You can create **generic constructors** even in non-generic classes.

---

### 🧾 Case 1: Constructor in Generic Class

```java
class Box<T> {
    private T value;

    public Box(T value) {
        this.value = value;
    }

    public T getValue() {
        return value;
    }
}
```

---

### 🧾 Case 2: Generic Constructor in Non-Generic Class

```java
class Box2 {
    public <T> Box2(T value) {
        System.out.println("Value: " + value);
    }
}
```

> The `<T>` before the constructor defines a generic constructor **independent of the class type**.

### ✅ Usage:

```java
Box2 b1 = new Box2(10);        // Value: 10
Box2 b2 = new Box2("Hello");   // Value: Hello
```

> Useful when the class itself doesn't need to be generic, but the constructor does.

---

## 📌 Summary of Key Concepts

|Concept|Description|
|---|---|
|`T extends Class`|Restricts T to that class or its subclasses|
|`T extends Class & Interface`|Restricts T to class + multiple interfaces|
|Generic Interfaces|Can be implemented with concrete or generic types|
|Enums|Built-in type safety — can't assign invalid values|
|Generic Constructors|Constructors can be generic even if the class is not|
|Syntax Rule (Multiple Bounds)|Class must come **first**, then interfaces; all declared with `extends`|

---

