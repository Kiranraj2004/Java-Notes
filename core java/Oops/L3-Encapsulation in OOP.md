
## ✅ **Encapsulation in Java - Summary Notes**

### 🧠 **Definition**

Encapsulation is one of the **four pillars** of Object-Oriented Programming (OOP):

- **Encapsulation**
    
- Abstraction
    
- Inheritance
    
- Polymorphism
    

It refers to **binding data (variables)** and **behavior (methods)** together in one unit (class) and **restricting direct access** to some of the object's components.

---

### 📦 **Why Use Encapsulation?**

- Prevent unwanted changes to variables (like setting negative age, roll number, or balance).
    
- Centralized control over the logic of setting/getting values.
    
- Improved data security and validation.
    
- Cleaner, maintainable code.
    

---

### 🏗️ **Class Design in Java**

- A **class** is a blueprint.
    
- It contains:
    
    - **Properties** (Instance Variables/Fields)
        
    - **Behaviors** (Methods)
        

```java
class Student {
    String name;
    int rollNo;
    int age;
}
```

---

### 📍 **Instance vs Local Variables**

- **Instance Variable**: Declared inside a class but outside methods. Tied to each object.
    
- **Local Variable**: Declared inside methods. Temporary.
    

---

### 🔐 **Encapsulation Approach**

1. **Make instance variables `private`** to restrict direct access.
    
2. **Provide `public` methods** (getters/setters) to access and update values.
    

#### Example:

```java
class Student {
    private int age;

    public void setAge(int x) {
        if(x < 0) {
            age = 0;
            System.out.println("Invalid age.");
        } else {
            age = x;
        }
    }

    public int getAge() {
        return age;
    }
}
```

---

### 💡 **Why Use Getters and Setters?**

- Allows validation before assigning values.
    
- Protects internal data of the object.
    
- Centralizes logic in one place (method).
    
- Maintains control over how values are accessed or modified.
    

---

### 🛠️ **Using Getters/Setters in IDE (like IntelliJ)**

- **Shortcut**: Right-click → _Generate_ → _Getter and Setter_ → Select variables.
    
- IDE creates getter/setter methods for selected fields.
    

---

### 🏦 **Encapsulation in Real-Life Example: BankAccount**

```java
class BankAccount {
    private long accountNumber;
    private double balance;

    public void deposit(double amount) {
        if (amount > 0) {
            balance += amount;
            System.out.println("Deposited: " + amount);
        } else {
            System.out.println("Invalid deposit amount");
        }
    }

    public void withdraw(double amount) {
        if (amount > 0 && amount <= balance) {
            balance -= amount;
            System.out.println("Withdrawn: " + amount);
        } else {
            System.out.println("Invalid amount or insufficient balance");
        }
    }

    public double getBalance() {
        return balance;
    }

    // Setters/Getters for accountNumber can be added similarly
}
```

---

### ✅ **Key Points**

- Use **private** for fields.
    
- Use **public** methods to control access.
    
- Use `this.variable` inside setters to distinguish between parameter and instance variable.
    
- Avoid direct field access from outside; always go through methods.
    
