


### 🔹 **Understanding `toString()` Method in Exceptions**

1. **Purpose of `toString()`**:
   - When you `System.out.println(e)` an object (`e` being an exception), Java internally calls the `toString()` method of that exception object.

2. **Default `toString()` Implementation**:
   - All Java classes extend the `Object` class, which provides a default `toString()` method.
   - Default format: `ClassName@Hashcode`.
   - Example for custom class:
     ```java
     Student student = new Student(); 
     System.out.println(student); // calls student.toString()
     ```

3. **Overriding `toString()` in Custom Classes**:
   ```java
   @Override
   public String toString() {
       return String.valueOf(this.id); // assuming id is an integer
   }
   ```
   - This custom output will be used instead of the hashcode format.

4. **How Exceptions Use `toString()`**:
   - Java exceptions override `toString()` in `Throwable` class.
   - Format:
     ```
     ClassName: message
     ```
     E.g., `java.lang.ArithmeticException: / by zero`

---

### 🔹 **Trace of Inheritance in Java Exception Classes**

Java uses an inheritance hierarchy to manage all exceptions:

```
Object
  └── Throwable
       ├── Error                 // For serious system-level issues (rarely handled)
       └── Exception
            ├── IOException     // Checked exception
            └── RuntimeException
                 ├── ArithmeticException
                 ├── NullPointerException
                 └── etc...
```

- **Throwable**: The root class of the exception hierarchy.
- **Error**: Serious errors that applications should not try to catch.
- **Exception**: Errors that can be caught and handled.
- **RuntimeException**: Unchecked exceptions that occur at runtime.

---

### 🔹 **Why Exception Message Appears Well-Formatted**

- The message like `java.lang.ArithmeticException: / by zero` is due to overridden `toString()` in `Throwable` class.
- This class has a `detailMessage` field set during object construction.
- The stack trace and this message are filled when the JVM creates the exception object.

---

### 🔹 **Catching Exceptions using `try-catch`**

#### Basic Syntax:

```java
try {
    // risky code
} catch (ArithmeticException e) {
    System.out.println("Divide by zero happened!");
}
```

- Java jumps to the first matching catch block when an exception occurs.
- Once a match is found, remaining catch blocks are skipped.

---

### 🔹 **Catching Multiple Exceptions (Multiple Catch Blocks)**

```java
try {
    // risky code
} catch (NullPointerException e) {
    System.out.println("Null Pointer Exception occurred");
} catch (ArithmeticException e) {
    System.out.println("Arithmetic Exception occurred");
} catch (Exception e) {
    System.out.println("Some other Exception occurred");
}
```

- Catch more specific exceptions first.
- `Exception` is the parent, so it must be written **after** child exceptions like `ArithmeticException`.
- If `Exception` comes first, child catch blocks become unreachable → Compilation error.

---

### 🔹 **Common Exceptions Explained**

| Exception Type        | When it Occurs                          | Example Scenario                      |
|-----------------------|------------------------------------------|----------------------------------------|
| `ArithmeticException` | Division by zero                        | `int x = 10 / 0;`                      |
| `NullPointerException`| Calling method on `null` object         | `student.setId(123);` when `student` is null |
| `ArrayIndexOutOfBoundsException` | Accessing invalid index        | `arr[10]` where `arr.length = 5`       |

---

### 🔹 **Handling Multiple Exceptions in a Block**

If a `try` block can throw different exceptions:
```java
try {
    student.setId(123);      // may throw NullPointerException
    int x = 10 / 0;          // may throw ArithmeticException
} catch (NullPointerException e) {
    System.out.println("Caught NullPointerException");
} catch (ArithmeticException e) {
    System.out.println("Caught ArithmeticException");
}
```

- Only one `catch` block is executed per exception occurrence.
- Exception message can be printed using `e.getMessage()` or `System.out.println(e);`

---

### 🔹 **Why `Throwable` Should Be Avoided in Catch**

```java
catch (Throwable e) {
    // discouraged unless absolutely necessary
}
```
- Too generic.
- Hard to maintain or debug because it catches even serious errors like `OutOfMemoryError`.
- Better to use specific exception types.

---

### 🔹 **Example Code Based on the Lecture**

```java
public class Main {
    public static void main(String[] args) {
        int[] numerators = {10, 200, 30, 40};
        int[] denominators = {1, 2, 0, 4};
        for (int i = 0; i < numerators.length; i++) {
            try {
                System.out.println(numerators[i] / denominators[i]);
            } catch (ArithmeticException e) {
                System.out.println("Arithmetic Exception: " + e.getMessage());
            } catch (Exception e) {
                System.out.println("Other Exception: " + e.getMessage());
            }
        }
        System.out.println("Good Job 😊");
    }
}
```

---

### 🔹 **Key Takeaways**

- Java's `toString()` method is crucial for cleanly printing exception messages.
- All exceptions in Java ultimately extend the `Throwable` class.
- `Exception` handling ensures that your code doesn’t crash on runtime errors.
- You can create **multiple catch blocks** to handle different types of exceptions.
- Be specific while catching exceptions for better clarity and debugging.
