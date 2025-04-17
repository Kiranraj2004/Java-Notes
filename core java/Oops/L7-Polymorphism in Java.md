
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
    