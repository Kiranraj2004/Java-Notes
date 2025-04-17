
## 🧠 **What is Abstraction?**

- **Definition**: Abstraction means **hiding internal implementation details** and showing only the functionality to the user.
    
- **Real-life example**:
    
    - Think about an **AC remote**:
        
        - You can **increase/decrease temperature**, change modes, etc.
            
        - You don’t need to know **how it works internally**.
            
        - This is abstraction — **you operate a system without knowing internal logic**.
            

---

## 👨‍💻 **Abstraction in Java**

Abstraction in Java can be achieved using:

1. **Abstract Classes**
    
2. **Interfaces** (explained in later videos)
    

---

### 🔹 **Abstract Class**

- A class that is **declared with `abstract` keyword**.
    
- It **cannot be instantiated** (you can't create its object).
    
- It can have:
    
    - **Abstract methods** (without body)
        
    - **Concrete methods** (with body)
        

---

### 🔸 **Abstract Method**

- A method that is **declared without a body**.
    
- Syntax:
    
    ```java
    abstract void sayHello();  // No body
    ```
    
- If a class has even **one abstract method**, then the **class must be abstract**.
    
- If you forget to declare the class as abstract, compiler error:
    
    ```
    Abstract method in non-abstract class
    ```
    

---

## ✅ Example:

### Abstract class: `Animal`

```java
abstract class Animal {
    abstract void sayHello(); // Abstract method

    void sleep() {
        System.out.println("Animal is sleeping...");
    }

    private int age;
    private String name;

    // Getters and Setters
}
```

- `sayHello()` is abstract → Must be implemented by subclasses.
    
- `sleep()` is concrete (regular method).
    
- `Animal` can’t be instantiated.
    

---

### Subclass: `Dog`

```java
class Dog extends Animal {
    @Override
    void sayHello() {
        System.out.println("Dog says: Woof!");
    }
}
```

### Subclass: `Cat`

```java
class Cat extends Animal {
    @Override
    void sayHello() {
        System.out.println("Cat says: Meow!");
    }
}
```

---

### Main Class (Testing)

```java
public class Test {
    public static void main(String[] args) {
        Dog dog = new Dog();
        dog.sayHello(); // Output: Woof!

        Animal animal = new Dog(); // Reference of abstract class
        animal.sayHello();         // Output: Woof!
    }
}
```

- ✅ You **can’t create object** of `Animal` (abstract class).
    
- ✅ But you **can create its reference** pointing to a subclass object (Dog, Cat, etc.).
    

---

## 🚫 Object Creation of Abstract Class

```java
Animal a = new Animal(); // ❌ Error: Animal is abstract; cannot be instantiated
```

---

## 💡 When to Use Abstraction?

- When you have a **generic base class** (e.g., Animal, Vehicle) and **many child classes** (e.g., Dog, Cat, Car, Bike).
    
- Use abstraction to:
    
    - **Define standard behavior** in the base class.
        
    - Force child classes to **provide their own implementations**.
        

---

## 📦 Access Modifiers Recap

- `public`: Accessible everywhere.
    
- `private`: Accessible only in the same class.
    
- **Default (no modifier)**: Package-private – accessible only in the same package.
    
- `protected`: Accessible in the same package + subclasses in other packages.
    

> If a subclass is in another package, it can’t override a method from the parent class unless that method is **public** or **protected**.

---

## 🚲 Additional Example: `Vehicle`

```java
abstract class Vehicle {
    abstract void accelerate();
    abstract void brake();
}
```

- All types of vehicles (Bike, Car, etc.) **must implement** `accelerate()` and `brake()` methods.
    
- This defines a **standard contract** for subclasses.
    

---

## ✅ Summary

|Concept|Description|
|---|---|
|Abstraction|Hiding internal details and showing functionality.|
|Abstract Class|Declared with `abstract` keyword, can’t be instantiated.|
|Abstract Method|Declared without body; must be implemented by child class.|
|Concrete Method|Regular method with a body.|
|Use Case|When common behavior needs to be defined in the base class and implemented differently by each subclass.|
