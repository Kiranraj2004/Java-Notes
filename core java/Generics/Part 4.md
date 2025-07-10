
## ✅ Java Generics – Full Notes with Code & Output

---

### 🔹 1. **What Are Generics in Java?**

- Generics allow you to write **type-safe, reusable code**.
    
- Introduced in Java 5 to eliminate **type casting** and **ClassCastException** at runtime.
    

---

### 🔹 2. **Generic Classes**

#### 📘 Syntax:

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

#### ✅ Usage:

```java
Box<Integer> intBox = new Box<>();
intBox.setValue(10);
System.out.println(intBox.getValue()); // Output: 10

Box<String> strBox = new Box<>();
strBox.setValue("Hello");
System.out.println(strBox.getValue()); // Output: Hello
```

- `T` is a **placeholder** for the actual type passed during object creation.
    
- The class is now **type-safe**, so no casting is needed.
    

#### 🔁 You can also use any letter like `<E>`, `<K,V>`, but by convention:

- T → Type
    
- K → Key
    
- V → Value
    
- E → Element
    
- N → Number
    

---

### 🔹 3. **Generic Class with Multiple Type Parameters**

```java
class Pair<K, V> {
    private K key;
    private V value;

    public Pair(K key, V value) {
        this.key = key;
        this.value = value;
    }

    public K getKey() { return key; }
    public V getValue() { return value; }
}
```

#### ✅ Usage:

```java
Pair<String, Integer> pair = new Pair<>("Age", 30);
System.out.println(pair.getKey());   // Output: Age
System.out.println(pair.getValue()); // Output: 30
```

---

### 🔹 4. **Generic Interfaces**

```java
interface Container<T> {
    T getItem();
}
```

#### Implementing the Interface:

```java
class StringContainer implements Container<String> {
    private String item;
    public String getItem() { return item; }
}
```

---

### 🔹 5. **Bounded Type Parameters**

#### 💡 Use `extends` to restrict the types:

```java
class Box<T extends Number> {
    private T value;
}
```

- Now only `Integer`, `Double`, `Float`, etc. are allowed (subclasses of `Number`).
    

#### ❌ Invalid:

```java
Box<String> box = new Box<>(); // Error: String does not extend Number
```

---

### 🔹 6. **Multiple Bounds**

```java
class Box<T extends Number & Printable> {
    private T value;
}
```

- First must be a **class**, rest must be **interfaces**.
    
- Use only `extends`, even for interfaces.
    

#### Example:

```java
interface Printable {
    void print();
}

class MyNumber extends Number implements Printable {
    int val;

    MyNumber(int val) { this.val = val; }

    public void print() { System.out.println("Value: " + val); }

    public int intValue() { return val; }
    public long longValue() { return val; }
    public float floatValue() { return val; }
    public double doubleValue() { return val; }
}

Box<MyNumber> box = new Box<>();
```

---

### 🔹 7. **Enum Type Safety**

```java
enum Day { MONDAY, TUESDAY }

Day d = Day.MONDAY;       // ✅ Valid
Day d2 = "MONDAY";        // ❌ Error: Type mismatch
```

- Enums are inherently **type-safe**.
    

---

### 🔹 8. **Generic Constructors**

Even if class is not generic, constructor can be:

```java
class Box2 {
    <T> Box2(T value) {
        System.out.println("Value: " + value);
    }
}
```

#### ✅ Usage:

```java
Box2 b1 = new Box2("Hello");
Box2 b2 = new Box2(10);
```

---

### 🔹 9. **Generic Methods**

#### 📘 Syntax:

```java
public <T> void printArray(T[] array) {
    for (T item : array) {
        System.out.println(item);
    }
}
```

#### ✅ Usage:

```java
Integer[] intArr = {1, 2, 3};
String[] strArr = {"Hello", "World"};
printArray(intArr);
printArray(strArr);
```

---

### 🔹 10. **Generic Method Overloading**

```java
public <T> void display(T value) {
    System.out.println("Generic: " + value);
}

public void display(Integer value) {
    System.out.println("Integer: " + value);
}
```

#### ✅ Output:

```java
display(10);         // Integer: 10
display("Hello");    // Generic: Hello
```

---

### 🔹 11. **Generic Method with Bounded Types**

```java
public <T extends Number> double add(T a, T b) {
    return a.doubleValue() + b.doubleValue();
}
```

#### ✅ Usage:

```java
System.out.println(add(10, 20));   // 30.0
System.out.println(add(5.5, 4.5)); // 10.0
```

---

### 🔹 12. **Wildcard (?) in Generics**

- Used to denote **unknown type**.
    

#### ✅ Read-only Method (Safe):

```java
public void printList(List<?> list) {
    for (Object obj : list) {
        System.out.println(obj);
    }
}
```

#### ❌ Not Safe for Write:

```java
List<?> list = new ArrayList<Integer>();
list.add(10); // Compile-time error
```

---

### 🔹 13. **Wildcards in Method Arguments**

```java
public <T> void copy(List<? extends T> source, List<? super T> dest) {
    for (T item : source) {
        dest.add(item);
    }
}
```

- `? extends T` = can read from source (child types)
    
- `? super T` = can write to destination (parent types)
    

---

## 🧠 Summary

|Concept|Purpose|
|---|---|
|Generic Class|Type-safe reusable classes|
|Generic Method|Type-safe logic within methods|
|Generic Constructor|Generic constructor even in non-generic class|
|Bounded Type Parameters|Restrict allowed types (e.g. `T extends Number`)|
|Multiple Bounds|`T extends Class & Interface1 & Interface2`|
|Wildcards (?)|Represent unknown types in read-only contexts|
|Enum Type Safety|Enum prevents assigning wrong type values|
