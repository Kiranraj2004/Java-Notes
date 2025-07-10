
## ✅ Java Generics (Advanced) – Detailed Notes

---

### 🔷 1. **Bounded Type Parameters**

#### ✅ What are they?

They restrict the type parameters to a specific class or interface.

#### ✅ Syntax:

```java
class Box<T extends Number> { ... }
```

#### ✅ Example:

```java
class Box<T extends Number> {
    T value;

    Box(T value) {
        this.value = value;
    }

    void printValue() {
        System.out.println(value);
    }
}
```

Only classes that extend `Number` (like `Integer`, `Double`, `Float`) can be passed.

#### ❌ Invalid:

```java
Box<String> box = new Box<>("Hello"); // Error: String doesn't extend Number
```

---

### 🔷 2. **Multiple Bounds**

#### ✅ Syntax:

```java
<T extends ClassName & Interface1 & Interface2>
```

- Class must come **first**
    
- Interfaces follow using `&`
    

#### ✅ Example:

```java
interface Printable {
    void print();
}

class MyNumber extends Number implements Printable {
    int value;

    MyNumber(int value) {
        this.value = value;
    }

    public void print() {
        System.out.println(value);
    }

    public int intValue() { return value; }
    public long longValue() { return value; }
    public float floatValue() { return value; }
    public double doubleValue() { return value; }
}

class Box<T extends Number & Printable> {
    T item;
    Box(T item) {
        this.item = item;
    }

    void printBox() {
        item.print();
    }
}
```

---

### 🔷 3. **Generic Constructors**

#### ✅ You can have a generic constructor even in a non-generic class.

```java
class Box2 {
    <T> Box2(T value) {
        System.out.println("Value: " + value);
    }
}

public class Main {
    public static void main(String[] args) {
        Box2 b = new Box2("Hello");
    }
}
```

---

### 🔷 4. **Generic Methods**

#### ✅ Syntax:

```java
public <T> void printArray(T[] arr) {
    for (T element : arr) {
        System.out.println(element);
    }
}
```

#### ✅ Example with Overloading:

```java
public <T> void display(T data) {
    System.out.println("Generic: " + data);
}

public void display(Integer data) {
    System.out.println("Integer: " + data);
}
```

---

### 🔷 5. **Wildcard in Generics**

|Type|Syntax|Use|
|---|---|---|
|Unbounded|`<?>`|Accept any type (Read-only)|
|Upper Bound|`<? extends Number>`|Accept Number or subclasses|
|Lower Bound|`<? super Integer>`|Accept Integer or superclasses|

---

#### ✅ Example (Unbounded Wildcard):

```java
public void printList(List<?> list) {
    for (Object obj : list) {
        System.out.println(obj);
    }
}
```

---

#### ✅ Example (Upper Bound – Read Only):

```java
public double sum(List<? extends Number> list) {
    double total = 0;
    for (Number n : list) {
        total += n.doubleValue();
    }
    return total;
}
```

---

#### ✅ Example (Lower Bound – Write Allowed):

```java
public void addNumbers(List<? super Integer> list) {
    list.add(10); // Allowed
}
```

---

### 🔷 6. **Type Erasure**

- **Generic information is removed at compile time.**
    
- The bytecode only sees raw types like `Object`.
    
- Allows **backward compatibility** with older Java versions.
    

#### ✅ Example:

```java
Box<String> box = new Box<>("Hello");
```

At runtime, JVM sees:

```java
Box box = new Box("Hello"); // Erased type
```

So:

```java
T → Object
T extends Number → Number
```

---

### 🔷 7. **Generic Exceptions**

#### ❌ Not Allowed:

```java
class MyGenericException<T> extends Exception {} // Error
```

#### ❓ Why?

- Generics use **type erasure**.
    
- At runtime, **exception types must be exact** (like `IOException`, `NullPointerException`)
    
- `catch` blocks can't distinguish between generic types.
    

---

#### ✅ Workaround:

Use a **non-generic exception** class but allow generic constructors or members.

```java
class MyException extends Exception {
    public <T> MyException(T data) {
        super(data.toString());
    }
}
```

#### ✅ Usage:

```java
try {
    throw new MyException("This is a custom message");
} catch (MyException e) {
    System.out.println(e.getMessage());
}
```

---

### 🧠 Summary of What You've Learned

|Topic|Covered|
|---|---|
|Bounded Type Parameters|✅|
|Multiple Bounds (`extends Class & Interface`)|✅|
|Generic Constructors|✅|
|Generic Methods|✅|
|Wildcards (`?`, `? extends`, `? super`)|✅|
|Type Erasure|✅|
|Generic Exceptions & Limitations|✅|

-