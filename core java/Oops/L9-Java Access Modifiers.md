
### 🛡 Java Access Modifiers – Quick Summary
**Access Modifiers in Java** are **keywords** used to **control the visibility (access level)** of classes, methods, constructors, and variables (fields). They help in **encapsulating** code and determining **where a member or class can be accessed from**.

|Modifier|Same Class|Same Package|Subclass (Different Package)|Everywhere|
|---|---|---|---|---|
|**public**|✅|✅|✅|✅|
|**protected**|✅|✅|✅|❌|
|**default** (no modifier)|✅|✅|❌|❌|
|**private**|✅|❌|❌|❌|

---

### 💡 Key Concepts Recap:

- **`public`**: Accessible from _anywhere_. Perfect for APIs and utility methods/classes meant to be used globally.
    
- **`private`**: Only accessible _within the same class_. Great for encapsulation — hiding fields or methods that shouldn't be accessed directly.
    
- **`protected`**:
    
    - Accessible _within the same package_.
        
    - Also accessible in _subclasses_, even if those subclasses are in a different package.
        
    - Ideal when you want to allow inheritance but still maintain a degree of control.
        
- **`default`** (when no modifier is specified):
    
    - Accessible _only within the same package_.
        
    - Not accessible from outside packages, even in subclasses.
        
    - Good for package-private helpers or internal logic.
        


### 1. `public`

- **Access Level**: Everywhere.
    
- Can be accessed from any other class, package, or subclass.
    
- Example:
    
    ```java
    public class Car {
        public String brand;
        public void drive() {
            System.out.println("Driving...");
        }
    }
    ```
    

---

### 2. `private`

- **Access Level**: Only within the **same class**.
    
- Cannot be accessed from outside the class, not even by subclasses.
    
- Example:
    
    ```java
    public class Car {
        private String engineNumber;
    
        private void startEngine() {
            System.out.println("Engine started");
        }
    }
    ```
    

---

### 3. `protected`

- **Access Level**:
    
    - Within the same class,
        
    - Within the same package,
        
    - **In subclasses** (even in different packages).
        
- Commonly used in **inheritance**.
    
- Example:
    
    ```java
    public class Vehicle {
        protected String type;
    }
    
    public class Bike extends Vehicle {
        void showType() {
            System.out.println(type);
        }
    }
    ```
    

---

### 4. _Default_ (no modifier)

- If no modifier is specified, it’s called **default** access.
    
- **Access Level**: Only within the same **package**.
    
- Example:
    
    ```java
    class Animal {
        void makeSound() {
            System.out.println("Sound...");
        }
    }
    ```
    

---


### 🧱 Class-Level Rules:

- **Top-level classes** can only be `public` or default. They _cannot_ be `private` or `protected`.
    
- **Nested classes** (classes within classes) _can_ be `private`, `protected`, etc.
    

---

### 🛠 Real-World Use Cases:

- **Private Constructor**:
    
    - Prevents object creation.
        
    - Common in **Singleton patterns** and **utility classes** (`Math`, `Collections`).
        
- **Static Methods**:
    
    - Belong to the class, not to objects.
        
    - Can be accessed without creating an instance.
        
- **Singleton Pattern**:
    
    ```java
    public class School {
        private static School instance = null;
        private School() {}  // private constructor
    
        public static School getInstance() {
            if (instance == null) {
                instance = new School();
            }
            return instance;
        }
    }
    ```
    

---
