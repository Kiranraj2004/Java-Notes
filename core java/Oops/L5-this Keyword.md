
## 🔹 **Definition of `this` Keyword**

> In Java, **`this`** is a **reference variable** that refers to the **current object** of the class.

Whenever you use `this` inside a method or constructor, it refers to the **object that called the method or is being constructed**.

---

## ✅ **Why is `this` used?**

### 1. **To refer to current class instance variables**

When **local variables (e.g., constructor or method parameters)** have the same names as **instance variables**, `this` helps to differentiate between them.

#### 🔸 Example:

```java
class Student {
    String name;
    int age;

    Student(String name, int age) {
        this.name = name; // 'this.name' is instance variable, 'name' is constructor parameter
        this.age = age;
    }
}
```

---

### 2. **To call current class methods**

You can use `this` to **explicitly call another method** of the current class.

#### 🔸 Example:

```java
class Demo {
    void display() {
        System.out.println("Display method called");
    }

    void show() {
        this.display(); // same as calling display()
    }
}
```

---

### 3. **To call current class constructor**

Used to call one constructor from another **(constructor chaining)** within the same class.

#### 🔸 Example:

```java
class Student {
    String name;
    int age;

    Student() {
        this("Unknown", 0); // calling another constructor
    }

    Student(String name, int age) {
        this.name = name;
        this.age = age;
    }
}
```

---

### 4. **To pass current object as a parameter**

You can pass `this` as an argument in method or constructor calls.

#### 🔸 Example:

```java
class A {
    void display(A obj) {
        System.out.println("Object received");
    }

    void send() {
        display(this); // passing current object as parameter
    }
}
```

---

### 5. **To return current object**

Useful in method chaining by returning the same object from a method.

#### 🔸 Example:

```java
class Student {
    String name;

    Student setName(String name) {
        this.name = name;
        return this;
    }
}
```

---

## 🔚 Summary Table

|Use Case|Purpose|
|---|---|
|`this.variable`|Access current object’s variable|
|`this.method()`|Call current object’s method|
|`this()`|Call another constructor|
|`this` as argument|Pass current object|
|`return this`|Return current object (for method chaining)|
