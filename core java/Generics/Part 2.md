
---

## ✅ Recap: What are Generics?

Generics allow classes, interfaces, and methods to operate on _typed parameters_, enhancing **type safety**, **code reusability**, and **compile-time checks**.

---

## 📦 1. **Creating a Custom Generic Class**

### 🧾 Syntax:

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

Here:

- `T` is a **type parameter** (placeholder).
    
- At **runtime**, `T` will be replaced by the actual type like `String`, `Integer`, etc.
    

### ✅ Usage:

```java
Box<Integer> intBox = new Box<>();
intBox.setValue(10);
int i = intBox.getValue();  // No casting needed
System.out.println(i);      // Output: 10
```

```java
Box<String> strBox = new Box<>();
strBox.setValue("Hello");
String s = strBox.getValue();
System.out.println(s);      // Output: Hello
```

---

## 🧠 2. **Generic Type Parameters**

### 🤔 What is `T`?

- `T` is a **placeholder** used in class/interface/method declarations.
    
- You can use any identifier like `T`, `X`, `Data`, but Java convention prefers:
    
    - `T` – Type
        
    - `E` – Element
        
    - `K` – Key
        
    - `V` – Value
        
    - `N` – Number
        

> ✅ **Convention:** Use **single capital letters** for clarity and convention compliance.

---

## ✌️ 3. **Generic Class with Multiple Type Parameters**

You can use more than one type parameter in a class.

### 🧾 Example: Generic Pair Class

```java
class Pair<K, V> {
    private K key;
    private V value;

    public Pair(K key, V value) {
        this.key = key;
        this.value = value;
    }

    public K getKey() {
        return key;
    }

    public V getValue() {
        return value;
    }
}
```

### ✅ Usage:

```java
Pair<String, Integer> agePair = new Pair<>("Age", 30);
System.out.println(agePair.getKey());   // Output: Age
System.out.println(agePair.getValue()); // Output: 30
```

> 🧠 Using generics here avoids the need to create separate classes for each data type.

---

## 📑 4. **Generic Interfaces**

You can also define generic **interfaces** just like generic classes.

### 🧾 Syntax:

```java
interface Container<T> {
    void setItem(T item);
    T getItem();
}
```

---

## 🧩 5. **Implementing a Generic Interface**

### Approach 1: Specify the type at implementation

```java
class StringContainer implements Container<String> {
    private String item;

    public void setItem(String item) {
        this.item = item;
    }

    public String getItem() {
        return item;
    }
}
```

### ✅ Usage:

```java
StringContainer sc = new StringContainer();
sc.setItem("Hello");
System.out.println(sc.getItem()); // Output: Hello
```

---

### Approach 2: Keep the class generic too

```java
class GenericContainer<T> implements Container<T> {
    private T item;

    public void setItem(T item) {
        this.item = item;
    }

    public T getItem() {
        return item;
    }
}
```

### ✅ Usage:

```java
GenericContainer<Integer> gc = new GenericContainer<>();
gc.setItem(100);
System.out.println(gc.getItem()); // Output: 100
```

---

## ⚠️ Common Errors and Fixes

|Problem|Solution|
|---|---|
|`Cannot resolve symbol 'T'`|You forgot to declare `<T>` in class/interface|
|`Type mismatch`|Ensure the correct type is used in object creation|
|Using non-generic type with generic method|Make sure the caller uses a type parameter|

---

## ✅ Summary: Key Learnings

|Concept|Example|Notes|
|---|---|---|
|Generic Class|`class Box<T> { ... }`|T can be anything: Integer, String, etc.|
|Generic Type Parameter|`<T>, <K,V>`|Convention: T=Type, K=Key, V=Value|
|Multiple Type Parameters|`class Pair<K, V>`|Combine multiple types in one class|
|Generic Interface|`interface Container<T> { ... }`|Works like classes|
|Implementing Generic Interface|`class A<T> implements B<T>`|Ensure all types are consistently passed|
|Compile-time Safety|`Box<String>`, `Pair<Integer, String>`|No ClassCastException or unsafe casting|

---

