
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

## 🧠 **Behind the Scenes – `System.out.println()`**

- Internally calls `toString()` method on the object.
    
- If we print an object (like an exception), Java implicitly calls `.toString()`.
    

---

## 🧰 **Understanding `toString()` Method**

- Every class in Java **inherits from `Object`** (even if not explicitly stated).
    
- The default implementation of `toString()` prints:
    
    ```
    className@hashCode
    ```
    
- But exception classes **override `toString()`** to show:
    
    ```
    java.lang.ArithmeticException: / by zero
    ```
    

---

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
    
