
## ✅ **Constructors in Java – Notes**

### 🔹 **What is a Constructor?**

- A **constructor** is a special method used to **initialize objects** in Java.
    
- It is **called automatically** when an object is created using `new`.
    
- Constructors have **no return type** (not even `void`) and must have the **same name** as the class.
    

---

### 🔹 **Syntax of a Constructor**

```java
class Student {
    String name;
    int rollNumber;
    int age;

    // Default Constructor
    Student() {
        age = 10; // Example of setting a default value
    }

    // Parameterized Constructor
    Student(String name, int rollNumber, int age) {
        this.name = name;
        this.rollNumber = rollNumber;
        this.age = age;
    }
}
```

---

### 🔹 **Types of Constructors**

|Type|Description|
|---|---|
|**Default Constructor**|No parameters. It is **provided by Java by default** if no constructor is defined.|
|**Parameterized Constructor**|Accepts arguments to initialize fields when object is created.|
|**Overloaded Constructor**|Multiple constructors with different parameter lists (constructor overloading).|

---

### 🔹 **Default Constructor Behavior**

- If **no constructor** is written, Java **automatically provides** a default one.
    
- Default values are:
    
    - `null` for `String`
        
    - `0` for `int`
        
    - `0.0` for `float/double`
        
    - `false` for `boolean`
        

**Example:**

```java
Student s = new Student(); // Calls default constructor
System.out.println(s.name); // null
System.out.println(s.rollNumber); // 0
System.out.println(s.age); // 10 (if set in constructor)
```

---

### 🔹 **Parameterized Constructor**

- Used to initialize values **at the time of object creation**.
    
- **Avoids the need** to call multiple setter methods later.
    

**Example:**

```java
Student s2 = new Student("Kiran", 101, 20);
```

---

### 🔹 **Constructor Overloading**

- You can have **multiple constructors** with the **same name** but different parameter lists.
    
- Similar to **method overloading**.
    

**Examples:**

```java
Student(String name) { this.name = name; }

Student(int rollNumber) { this.rollNumber = rollNumber; }

Student(String name, int rollNumber, int age) {
    this.name = name;
    this.rollNumber = rollNumber;
    this.age = age;
}
```

---

### ⚠️ **Important Rule**

- If you **define any constructor** (parameterized or not), **Java will not provide the default constructor**.
    
- So, if you still want a no-argument constructor, you must **explicitly define** it yourself.
    

**Error Example:**

```java
Student s = new Student(); // Error if only parameterized constructor is defined
```

---

### 🔹 **"this" Keyword in Constructor**

- Used to **differentiate** between **instance variables** and **local parameters**.
    

```java
this.age = age; // Assigns local 'age' to the object's 'age'
```

---

### 🔹 **Use Cases**

- Initialize values directly while creating object.
    
- Avoids multiple setter calls.
    
- Can be used to **validate** or apply **conditions** (e.g., `age > 10`) during initialization.
    

---

