
## ✅ PART 1: Multi-Catch and Disjoint Rule

### 🔹 What is Multi-Catch?

- Java allows catching multiple exception types in a single `catch` block using the **pipe symbol `|`**:
    

```java
try {
    // risky code
} catch (NullPointerException | ArithmeticException e) {
    System.out.println("Handled one of the exceptions");
}
```

### ⚠️ Disjoint Rule in Multi-Catch:

- The exceptions combined in a multi-catch block **must not have an inheritance relationship**.
    
- ❌ This will **not compile**:
    

```java
catch (ArithmeticException | RuntimeException e) {
    // Compile-time error
}
```

- Because `ArithmeticException` is a subclass of `RuntimeException`.
    

✅ **Correct** usage:

```java
catch (NullPointerException | IOException e) {
    // Both are unrelated (disjoint), so valid
}
```

---

## ✅ PART 2: Example: Array Index Out of Bounds Exception

### 🔹 Code Example:

```java
int[] arr = {1, 2, 3, 4};
for (int i = 0; i < 10; i++) {
    System.out.println(arr[i]);
}
```

- Only 0 to 3 are valid indices.
    
- When `i = 4`, it throws:  
    ❌ `ArrayIndexOutOfBoundsException`
    

### 🔹 Effect of Exception:

- Execution stops **immediately** when the exception occurs.
    
- Subsequent code (e.g., `System.out.println("Good job!")`) does not execute unless exception is handled.
    

### 🔹 With Try-Catch:

```java
try {
    for (int i = 0; i < 10; i++) {
        System.out.println(arr[i]);
    }
} catch (Exception e) {
    System.out.println("Caught an exception: " + e);
}
System.out.println("Good job!"); // This will now print
```

---

## ✅ PART 3: Exception Propagation

### 🔹 What is Exception Propagation?

- If a method throws an exception and doesn't handle it, the exception propagates to the calling method.
    

### 🔹 Example:

```java
void level3() {
    int[] a = new int[5];
    a[5] = 10; // Index out of bounds
}

void level2() {
    level3();
}

void level1() {
    level2();
}

public static void main(String[] args) {
    level1(); // No try-catch here
}
```

### 🔹 Result:

- JVM prints a **stack trace**, showing:
    
    - Exception occurred in `level3`
        
    - Called by `level2`
        
    - Called by `level1`
        
    - Called by `main`
        

### 🔹 Stack Trace Meaning:

- A **stack trace** is a snapshot of the method call stack when an exception occurs.
    
- It helps developers trace **where the error happened** and **how the flow reached there**.
    

---

## ✅ PART 4: Printing Stack Trace Manually

```java
try {
    level1();
} catch (Exception o) {
    StackTraceElement[] stack = o.getStackTrace();
    for (StackTraceElement e : stack) {
        System.out.println(e);
    }
}
```

- You can also use:
    

```java
o.printStackTrace();
```

- Output is the same – it prints the full method call hierarchy with line numbers.
    

---

## ✅ PART 5: `getMessage()` vs `printStackTrace()`

|Method|Purpose|
|---|---|
|`getMessage()`|Returns the **message** passed when exception was created|
|`printStackTrace()`|Prints the **full exception + call stack** to console|
|`getStackTrace()`|Returns array of `StackTraceElement` objects|

---

## ✅ PART 6: Unchecked Exceptions

### 🔹 Definition:

- **Not checked** at compile time.
    
- JVM handles them at **runtime**.
    
- Subclasses of `RuntimeException`.
    

### 🔹 Examples:

- `NullPointerException`
    
- `ArithmeticException`
    
- `ArrayIndexOutOfBoundsException`
    

### 🔹 Behavior:

```java
Student a = null;
a.setId(123); // ❌ NullPointerException at runtime
```

- No compiler error.
    
- Runtime crash if unhandled.
    

---

## ✅ PART 7: Checked Exceptions

### 🔹 Definition:

- **Checked at compile time**.
    
- You **must** handle them using `try-catch` or `throws`.
    

### 🔹 Examples:

- `IOException`
    
- `FileNotFoundException`
    
- `SQLException`
    

### 🔹 Example:

```java
FileReader fr = new FileReader("a.txt");
```

❌ Compile-time error:

```
unhandled exception: java.io.FileNotFoundException
```

### ✅ Fix:

```java
try {
    FileReader fr = new FileReader("a.txt");
} catch (Exception e) {
    System.out.println("Handled file error");
}
```

✅ Or more specific:

```java
catch (FileNotFoundException e) { ... }
```

- `FileNotFoundException` ⟶ subclass of `IOException`
    
- `IOException` ⟶ subclass of `Exception`
    

---

## ✅ PART 8: Exception Class Hierarchy Recap

```
Object
  └── Throwable
        ├── Exception
        │     ├── IOException
        │     ├── SQLException
        │     └── RuntimeException
        │            ├── NullPointerException
        │            ├── ArithmeticException
        │            ├── IndexOutOfBoundsException
        └── Error (e.g., OutOfMemoryError)
```

---

## ✅ Summary

|Feature|Checked Exception|Unchecked Exception|
|---|---|---|
|**Compiler check?**|✅ Yes|❌ No|
|**Must handle with try/catch?**|✅ Yes|❌ Optional|
|**Common examples**|`IOException`, `SQLException`|`NullPointerException`, `ArithmeticException`|
|**Super class**|`Exception`|`RuntimeException`|
|**When occurs**|Compile-time|Runtime|
