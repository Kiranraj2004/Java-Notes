
## ✅ **Java Errors and Exceptions – Introduction**

Java classifies program issues into **three main types of errors**:

### 1. **Syntax Error**

- Detected at **compile-time**.
    
- Violates language rules (e.g., missing `;`, wrong brackets, undeclared variables).
    
- Example:
    
    ```java
    int a = 10  // Missing semicolon → Syntax error
    ```
    

### 2. **Logical Error**

- The program compiles and runs but produces **incorrect output**.
    
- The issue lies in the logic.
    
- Example:
    
    ```java
    // Expected multiplication, but written division
    int result = a / b; // Instead of a * b
    ```
    

### 3. **Runtime Error (Exception)**

- Occurs **during program execution**.
    
- Example: Division by zero, accessing an array index out of bounds, null pointer access.
    
- Example:
    
    ```java
    int a = 10;
    int b = 0;
    int result = a / b; // Runtime exception
    ```
    

---

## 🚨 **What is an Exception?**

> An **exception** is an event that disrupts the normal flow of a program.

- Occurs during runtime.
    
- It's an **object** in Java, thrown by the JVM when a problem arises.
    
- This object is a subclass of `Throwable`.
    

### Syntax:

```java
try {
    // Code that may throw an exception
} catch (ExceptionType name) {
    // Handling code
}
```

---

## 🧪 **Example Code with Division**

### Problem:

```java
int[] numerators = {10, 200, 30, 40};
int[] denominators = {1, 2, 0, 4};

for (int i = 0; i < numerators.length; i++) {
    System.out.println(numerators[i] / denominators[i]);
}
System.out.println("Good Job! 😊");
```

### Output:

```
10
100
Exception in thread "main" java.lang.ArithmeticException: / by zero
```

> 💥 The program **crashes at `30/0`**, and "Good Job" is **never printed**.

---

## 🔐 **Exception Handling with `try-catch`**

### Modified Code:

```java
for (int i = 0; i < numerators.length; i++) {
    try {
        System.out.println(numerators[i] / denominators[i]);
    } catch (ArithmeticException e) {
        System.out.println(e); // Prints the exception
        System.out.println(-1); // Fallback or custom value
    }
}
System.out.println("Good Job! 😊");
```

### Output:

```
10
100
java.lang.ArithmeticException: / by zero
-1
10
Good Job! 😊
```

> ✅ The program does not crash; the flow **continues gracefully** after the error.

---

## 📦 **Exception Object**

- The object is an instance of a subclass of `Throwable`.
    
- For `ArithmeticException`, the object contains:
    
    - Error message (`/ by zero`)
        
    - Stack trace
        
    - Class and line where it occurred
        

---
## 🧠 What is a Stack?

- Java maintains a **call stack** where each method call is **pushed onto the stack**.
    
- When a method finishes, it is **popped off** the stack.
    
- If an exception occurs, Java prints the **call stack** to help developers locate the error.
    

---

## 🔍 What is a Stack Trace?

- A **stack trace** is automatically printed when an exception is **not handled** (or printed manually using `printStackTrace()`).
    
- It shows:
    
    - The **exception type**
        
    - The **error message**
        
    - The **sequence of method calls**
        
    - The **file name** and **line number** where the error occurred
        

---

## ✅ Example: Stack Trace in Action

```java
public class Main {

    public static void main(String[] args) {
        method1();
    }

    static void method1() {
        method2();
    }

    static void method2() {
        int result = 10 / 0; // This causes ArithmeticException
    }
}
```

### 🧾 Output (Stack Trace):

```
Exception in thread "main" java.lang.ArithmeticException: / by zero
	at Main.method2(Main.java:13)
	at Main.method1(Main.java:9)
	at Main.main(Main.java:5)
```

---

## 📚 Breakdown of the Stack Trace:

- `java.lang.ArithmeticException: / by zero`  
    👉 Type and message of the exception.
    
- `at Main.method2(Main.java:13)`  
    👉 Error occurred in `method2` at line 13.
    
- `at Main.method1(Main.java:9)`  
    👉 `method2` was called from `method1` at line 9.
    
- `at Main.main(Main.java:5)`  
    👉 `method1` was called from `main()` at line 5.
    

---

## 🛠️ Using `printStackTrace()` Manually

You can also print the stack trace in a `catch` block:

```java
try {
    int result = 10 / 0;
} catch (ArithmeticException e) {
    e.printStackTrace(); // prints the full stack trace
}
```

---

## 🔧 Why Stack Trace is Important?

- It tells you **where** the error happened.
    
- Shows the **method call path** leading to the exception.
    
- Helps you **debug deeply nested methods** or **libraries**.
    

---

## 🧠 **Behind the Scenes – `System.out.println()`**

- Internally calls `toString()` method on the object.
    
- If we print an object (like an exception), Java implicitly calls `.toString()`.
    

---

## 🔍 What is `toString()` in Java?

- The `toString()` method is defined in the `Object` class.
    
- Its purpose is to return a string representation of the object.
    
- Every class in Java either **inherits** or **overrides** this method.
    

---

## 🧪 Default Behavior of `toString()`

If a class **does not override** `toString()`, it returns a string like:

```
ClassName@HashCode
```

### ✅ Example: Without Overriding `toString()`

```java
class Student {
    int id;
    String name;
    
    Student(int id, String name) {
        this.id = id;
        this.name = name;
    }
}

public class Main {
    public static void main(String[] args) {
        Student s = new Student(101, "Alice");
        System.out.println(s);           // Implicit call to s.toString()
        System.out.println(s.toString()); // Explicit call
    }
}
```

### 🧾 Output:

```
Student@15db9742
Student@15db9742
```

✅ It shows `ClassName@HashCode` because we didn’t override `toString()`.

---

## ✅ Overriding `toString()` in Custom Classes

You can override `toString()` to print custom information:

```java
class Student {
    int id;
    String name;

    Student(int id, String name) {
        this.id = id;
        this.name = name;
    }

    @Override
    public String toString() {
        return "Student[id=" + id + ", name=" + name + "]";
    }
}

public class Main {
    public static void main(String[] args) {
        Student s = new Student(101, "Alice");
        System.out.println(s);
    }
}
```

### 🧾 Output:

```
Student[id=101, name=Alice]
```

✅ Now `toString()` returns a human-readable string because we overrode it.

---

## ⚠️ How Exception Classes Override `toString()`

Exception classes like `ArithmeticException`, `NullPointerException`, etc., **override** the `toString()` method to provide detailed error messages.

### ✅ Example with Exception:

```java
public class Main {
    public static void main(String[] args) {
        try {
            int result = 10 / 0;  // This causes ArithmeticException
        } catch (ArithmeticException e) {
            System.out.println(e);           // e.toString()
            System.out.println(e.toString()); // Explicit
        }
    }
}
```

### 🧾 Output:

```
java.lang.ArithmeticException: / by zero
java.lang.ArithmeticException: / by zero
```

✅ This is because the `ArithmeticException` class overrides `toString()` like this:

```java
public String toString() {
    return getClass().getName() + ": " + getMessage();
}
```

---

## 🧠 Summary

|Case|`toString()` Output|
|---|---|
|Custom class (not overridden)|`ClassName@hashCode`|
|Custom class (overridden)|Your custom string|
|Exception class|`ExceptionClass: Message`|

	

## 🧩 Summary of Key Concepts

|Concept|Explanation|
|---|---|
|`Syntax Error`|Caught at compile time|
|`Logical Error`|Incorrect output, hard to catch|
|`Runtime Error`|Exception thrown at runtime|
|`Exception`|Object representing error|
|`try-catch`|Used to catch and handle exceptions|
|`ArithmeticException`|Thrown for division by zero|
|`toString()`|Automatically called when printing objects|
|`System.out.println(obj)`|Internally runs `obj.toString()`|

---

## 🔚 **Best Practices for Exception Handling**

- Always **catch specific exceptions** first (e.g., `ArithmeticException`) before more generic ones (e.g., `Exception`).
    
- Never leave `catch` block empty.
    
- Use logging instead of `System.out.println` in production.
    
- Avoid excessive use of try-catch; fix logic where possible.
    
