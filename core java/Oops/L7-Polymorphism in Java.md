
### 🔹 **Definition**

- Polymorphism is one of the four core concepts of Object-Oriented Programming (OOP), along with:
    
    - Encapsulation
        
    - Inheritance
        
    - Abstraction
        
- The term **"Polymorphism"** means **"many forms"** (`poly` = many, `morph` = form).
    
- It allows a method to perform **different tasks** based on the object it is acting upon, **even if the method name and signature are the same**.
    

---

## 🟢 **Types of Polymorphism**

### 1. **Compile-Time Polymorphism (Static Binding)**

- Achieved through **Method Overloading**.
    
- The method to be called is decided **at compile time** based on:
    
    - Number of parameters
        
    - Type of parameters
        

#### ➤ **Example**:

```java
class Calculator {
    void add(int a, int b) { }
    void add(int a, int b, int c) { }
    void add(double a, double b) { }
}
```

- All methods are named `add`, but have **different parameter lists**.
    
- This is method overloading, and the correct method is resolved **during compilation**.
    

---

### 2. **Run-Time Polymorphism (Dynamic Binding)**

- Achieved through **Method Overriding**.
    
- Decision about which method to execute is made **at runtime**.
    

#### ➤ **Example**:

```java
class Animal {
    void sayHello() {
        System.out.println("...");
    }
}

class Dog extends Animal {
    void sayHello() {
        System.out.println("woof");
    }
    void sayBye() {
        System.out.println("bye");
    }
}

class Cat extends Animal {
    void sayHello() {
        System.out.println("meow");
    }
}
```

#### ➤ **Code Usage**:

```java
Animal a1 = new Dog();
Animal a2 = new Cat();

a1.sayHello();  // Output: woof
a2.sayHello();  // Output: meow
```

- Although the reference is of type `Animal`, the method of the **actual object** (`Dog` or `Cat`) is called.
    
- This behavior is known as **Dynamic Method Dispatch**.
    

---

## 🔸 **Dynamic Method Dispatch**

- At runtime, the JVM determines the actual object type and **calls the overridden method**.
    
- This mechanism enables **runtime polymorphism**.
    
- Called **"Dynamic Method Dispatch"** because the decision of which method to call is made **dynamically (at runtime)**.
    

---

## 🔸 **Upcasting and Downcasting**

### ✅ **Upcasting**

- Refers to assigning the child class object to the parent class reference.
    

```java
Animal a = new Dog(); // Valid (upcasting)
```

- We can only call methods **declared in the parent class** using the parent reference.
    

### ❌ **Downcasting**

- Trying to assign the parent class reference to a child class reference directly is not allowed:
    

```java
Dog d = new Animal(); // Invalid
```

- But it can be done through **explicit casting**, only if the object is actually of the child type:
    

```java
Animal a = new Dog();
Dog d = (Dog) a; // Valid, because 'a' refers to a Dog object
```

---

## ⚠️ **Access Limitation via Upcasting**

- When using a parent class reference (like `Animal a = new Dog()`), you **cannot access child-specific methods** (like `sayBye()` in Dog) unless **downcasting** is performed.
    

---

## 🔁 **Summary**

|Type|Achieved By|Binding Type|Time of Decision|
|---|---|---|---|
|Compile-time Polymorphism|Method Overloading|Static|Compile Time|
|Runtime Polymorphism|Method Overriding|Dynamic|Runtime|

---

### 🔚 Final Remarks:

- Method Overloading: **Same method name, different parameter lists**
    
- Method Overriding: **Same method name and signature in parent and child class**
    
- **Upcasting** helps achieve runtime polymorphism.
    
- JVM uses **Dynamic Method Dispatch** to resolve overridden methods.
    
- Always remember: the **object** determines the method execution, not the reference type.


---

### ✅ What's Happening in Your Code?

You have:

```java
Animal a = new Animal(); // Parent object
Animal b = new Dog();    // Parent reference, Child object
```

Then you do:

```java
a.move(); // "Animals can move"
b.move(); // "Dogs can walk and run"
System.out.println(b.i); // prints 1 — from Animal class!
```

---

## 🧠 Why does `b.move()` call the **Dog** method, but `b.i` gives **Animal.i**?

This is because of how Java handles:

|Feature|Java uses|
|---|---|
|**Methods**|**Runtime (dynamic) polymorphism** — a.k.a. method **overriding**|
|**Variables**|**Compile-time (static) binding** — a.k.a. variable **hiding**|

---

### 🔄 Method Overriding (Dynamic Binding)

When you **override a method** (`move()`), Java checks the **actual object type** (`Dog`) at **runtime**, and calls the appropriate method:

```java
b.move(); // Dog's move() runs, because `b` is actually a Dog object
```

---

### 🚫 Variable Hiding (Static Binding)

But **instance variables** (`int i = 1` in Animal, and `int i = 0` in Dog) are **not polymorphic**. Java checks the **reference type** at **compile time**.

```java
System.out.println(b.i); // Animal's `i`, because `b` is of type Animal
```

Even though `b` actually points to a `Dog` object, the compiler uses the type of `b` (which is `Animal`) to resolve variables.

---

### ✅ How to access `Dog`'s `i`?

You need to cast it:

```java
System.out.println(((Dog)b).i); // prints 0 — now accessing Dog's i
```

---

## 📌 Summary:

- **Methods are overridden** → Java uses **object type** at **runtime**.
    
- **Variables are hidden** → Java uses **reference type** at **compile time**.
    

### However, in the runtime, JVM figures out the object type and would run the method that belongs to that particular object.


### Questions 1
#### class Animal { 
public void move() {
System.out.println("Animals can move");
}
}
class Dog extends Animal { 
public void move() {
System.out.println("Dogs can walk and run");
} 
public void bark() {
System.out.println("Dogs can bark");
}
} 
public class TestDog { 
public static void main(String args[]) { 
Animal a = new Animal(); // Animal reference and object Animal b = new Dog(); // Animal reference but Dog object a.move(); // runs the method in Animal class b.move(); // runs the method in Dog class b.bark(); 
}
}
#### Output

TestDog.java:26: error: cannot find symbol
      b.bark();
       ^
  symbol:   method bark()
  location: variable b of type Animal
1 error

This program will throw a compile time error since b's reference type Animal doesn't have a method by the name of bark.





### 🔥 Java Dynamic Binding (a.k.a. Late Binding or Runtime Polymorphism)

**Dynamic binding** in Java means that **method calls are resolved at runtime** — not at compile time — based on the actual object type (not the reference type).

---

### 📘 What does this really mean?

Let’s take a basic example:

```java
class Animal {
    public void sound() {
        System.out.println("Animal makes a sound");
    }
}

class Dog extends Animal {
    public void sound() {
        System.out.println("Dog barks");
    }
}

public class Test {
    public static void main(String[] args) {
        Animal a = new Dog();  // Reference type is Animal, but object is Dog
        a.sound();             // What happens here?
    }
}
```

#### Output:

```
Dog barks
```

---

### 💡 Why does this happen?

Java sees that `a` is declared as type `Animal`, but the actual object is of type `Dog`. So at **runtime**, it dynamically **binds** the `sound()` method to the one in the `Dog` class.

This is called **dynamic method dispatch**, and it's a core feature of **runtime polymorphism**.

---

### 🔍 When does dynamic binding happen?

- ✅ **Only with instance methods**
    
- ❌ **Not with fields (variables)** — they are resolved at **compile time**
    
- ❌ **Not with static methods** — those are resolved using the **reference type**
    
- ❌ **Not with private methods** — they can't be overridden
    

---

### 👀 Quick Static vs Dynamic Binding Summary:

| Feature              | Binding Time      | Based On                    |
| -------------------- | ----------------- | --------------------------- |
| **Instance methods** | Runtime (dynamic) | Actual object type          |
| **Static methods**   | Compile time      | Reference type              |
| **Fields/Variables** | Compile time      | Reference type              |
| **Private methods**  | Compile time      | Class in which it's defined |
|                      |                   |                             |


Great! Let’s break down **static binding** (aka **early binding**) in Java with clarity.

---

### 🧠 **What is Static Binding in Java?**

**Static binding** means that the **method or variable to be called is resolved at compile time** — _based on the reference type_, not the actual object.

This is also called **early binding**, because everything is "bound" before your code actually runs.

---

### ✅ When does Static Binding happen?

- **Static methods**
    
- **Private methods**
    
- **Final methods**
    
- **Fields/variables**
    
- **Overloaded methods** (not overridden)
    

---

### 🧪 Example:

```java
class Animal {
    static void run() {
        System.out.println("Animal runs");
    }
}

class Dog extends Animal {
    static void run() {
        System.out.println("Dog runs");
    }
}

public class Test {
    public static void main(String[] args) {
        Animal a = new Dog();  // Reference type is Animal
        a.run();               // Which run() gets called?
    }
}
```

#### Output:

```
Animal runs
```

> Why not `Dog runs`?  
> Because **static methods are bound at compile time**, and the compiler checks the **reference type (`Animal`)**, not the object type (`Dog`).

---

### 📌 Important Notes

- Static binding gives **better performance** since it's resolved at compile time.
- static methos can't be overridden
    
- You **cannot override** static, private, or final methods — they are **hidden**, not overridden.
    
- That's why dynamic polymorphism (runtime method overriding) only works with **non-static, non-final, non-private instance methods**.
    

---

### 🆚 Static vs Dynamic Binding

|Feature|Static Binding|Dynamic Binding|
|---|---|---|
|Resolved at|Compile time|Runtime|
|Involves|Static, final, private methods, variables|Overridden methods|
|Based on|Reference type|Actual object type|
|Polymorphism type|Compile-time (overloading)|Runtime (overriding)|

---

Want an example showing **both static and dynamic binding in the same code** to compare side by side?