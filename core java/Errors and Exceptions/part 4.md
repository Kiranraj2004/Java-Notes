
## ✅ 1. `toString()` Method in Exceptions

### Concept:

- Every class in Java extends `Object`, which has a `toString()` method.
    
- When an exception object is printed (`System.out.println(e)`), `toString()` is implicitly called.
    

### In Built-in Exception:

```java
ArithmeticException e = new ArithmeticException("Divide by zero");
System.out.println(e);
```

### Output:

```
java.lang.ArithmeticException: Divide by zero
```

### Breakdown:

- `java.lang.ArithmeticException` → Full class name.
    
- `Divide by zero` → Message passed in constructor.
    
- `Throwable` class defines `toString()` to include both.
    

---

## ✅ 2. Multi-Catch Blocks

### Syntax:

```java
try {
    // code
} catch (ArithmeticException | NullPointerException e) {
    System.out.println("Common handler");
}
```

### Rule:

- The exceptions must be **disjoint** (no subclass-superclass relationship).
    
- Otherwise, you get a **compile-time error**.
    

---

## ✅ 3. Multiple Catch Blocks

### Example:

```java
try {
    Student s = null;
    s.setId(123);  // NullPointerException
} catch (NullPointerException e) {
    System.out.println("Null Pointer Exception");
} catch (ArithmeticException e) {
    System.out.println("Arithmetic Exception");
} catch (Exception e) {
    System.out.println("Generic Exception");
}
```

### Flow:

- First matching catch block is executed.
    
- Parent class `Exception` should be last; otherwise, child-specific blocks become unreachable.
    

---

## ✅ 4. Exception Propagation

### Example:

```java
public static void level3() {
    int[] arr = new int[5];
    int x = arr[10]; // ArrayIndexOutOfBoundsException
}

public static void level2() {
    level3();
}

public static void level1() {
    level2();
}
```

### If called from `main()`:

- Stack trace shows:
    
    - Exception in `level3()`
        
    - Called by `level2()`, then `level1()`, then `main()`.
        

### Stack Trace:

```
Exception in thread "main" java.lang.ArrayIndexOutOfBoundsException
    at level3(...)
    at level2(...)
    at level1(...)
    at main(...)
```

---

## ✅ 5. Stack Trace Programmatically

```java
catch (Exception e) {
    for (StackTraceElement ste : e.getStackTrace()) {
        System.out.println(ste);
    }
}
```

### Or:

```java
e.printStackTrace(); // Same output
```

---

## ✅ 6. Checked vs Unchecked Exceptions

### ✅ Unchecked:

- Not checked at compile time.
    
- Subclasses of `RuntimeException`.
    

Examples:

- `NullPointerException`
    
- `ArithmeticException`
    
- `ArrayIndexOutOfBoundsException`
    

### ✅ Checked:

- Checked at compile time.
    
- Must be caught or declared with `throws`.
    

Examples:

- `IOException`
    
- `FileNotFoundException`
    
- `SQLException`
    

### Example:

```java
FileReader fr = new FileReader("abc.txt"); // Checked
```

Compile-time error: “Unhandled exception type FileNotFoundException”.

---

## ✅ 7. `throws` Keyword

### Usage:

- Declares that a method can throw an exception.
    

```java
public static void readFile() throws FileNotFoundException {
    FileReader fr = new FileReader("abc.txt");
}
```

- Caller's responsibility to handle or declare.
    

---

## ✅ 8. `throw` Keyword

### Usage:

- Used to throw an exception manually.
    

```java
throw new FileNotFoundException("File missing");
```

Must either:

- Be handled in `try-catch`, or
    
- Declared in `throws` clause.
    

---

## ✅ 9. Try-Catch-Finally Block

### Purpose of `finally`:

- Executes regardless of exception or return statement.
    

### Example:

```java
public static int divide(int a, int b) {
    try {
        return a / b;
    } catch (ArithmeticException e) {
        return -1;
    } finally {
        System.out.println("Finally block executed");
    }
}
```

### Output:

```
Finally block executed
-1
```

> Even if `return` is in try/catch, `finally` runs before returning.

---

## ✅ 10. Use Case of `finally` in File Handling

### Problem:

Resources like `FileReader`, `BufferedReader`, or DB connections must be closed.

### Example:

```java
BufferedReader br = null;
try {
    br = new BufferedReader(new FileReader("data.txt"));
    // Read logic
} catch (IOException e) {
    e.printStackTrace();
} finally {
    if (br != null) br.close(); // Must be closed to release system resources
}
```

---

## 🔄 Recap of Key Java Exception Keywords

|Keyword|Purpose|
|---|---|
|`try`|Wraps code that may throw an exception|
|`catch`|Handles specific exception types|
|`finally`|Always runs after try/catch (used for cleanup)|
|`throw`|Manually throws an exception|
|`throws`|Declares that a method may throw exceptions|

---

## 💡 Pro Tips

- Always use specific catch blocks before generic ones.
    
- Use `finally` to release resources.
    
- Understand exception flow to debug errors better.
    
- `throw` is used for forcing exceptions, `throws` is used for declaring potential ones.
    
- Stack trace helps in pinpointing error location quickly.
    