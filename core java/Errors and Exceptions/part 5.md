
## ✅ Java Exception Handling — Advanced Concepts

---

### 🔁 1. **Multi-Catch Blocks**

- You can catch multiple exceptions in a single `catch` block using the pipe (`|`) symbol.
    

```java
try {
    // code that may throw multiple exceptions
} catch (ArithmeticException | NullPointerException e) {
    System.out.println("Caught an Arithmetic or Null Pointer Exception");
}
```

- ❌ You **cannot** catch exceptions in a multi-catch if they are in the same hierarchy (i.e., subclass & superclass). Compiler will show an error:
    

```java
// ❌ This is invalid because RuntimeException is superclass of ArithmeticException
catch (RuntimeException | ArithmeticException e) { }
```

---

### 🧵 2. **Exception Propagation and Stack Trace**

- If an exception is not handled where it occurs, it propagates up the call stack.
    
- Example:
    

```java
void level3() {
    int[] arr = new int[4];
    System.out.println(arr[5]);  // Throws IndexOutOfBoundsException
}

void level2() {
    level3();
}

void level1() {
    level2();
}
```

- If not handled, the exception bubbles up to `main()` and the program crashes.
    
- **Stack trace** shows the method call path leading to the exception.
    

```java
try {
    level1();
} catch (Exception e) {
    for (StackTraceElement ste : e.getStackTrace()) {
        System.out.println(ste);
    }
}
```

Or simply:

```java
e.printStackTrace();
```

---

### 🧾 3. **Checked vs Unchecked Exceptions**

|Type|Description|Checked by Compiler?|
|---|---|---|
|**Checked**|Must handle or declare using `throws`|✅ Yes|
|**Unchecked**|Runtime exceptions, not enforced by compiler|❌ No|

#### Examples:

- **Checked**: `IOException`, `FileNotFoundException`
    
- **Unchecked**: `NullPointerException`, `ArithmeticException`, `IndexOutOfBoundsException`
    

---

### 🎯 4. **throws Keyword**

- Used in method signature to pass exception handling responsibility to the caller.
    

```java
public void readFile() throws FileNotFoundException {
    FileReader fr = new FileReader("a.txt");
}
```

- Propagate it up:
    

```java
public void method1() throws FileNotFoundException {
    readFile();
}

public void main(String[] args) throws FileNotFoundException {
    method1();
}
```

---

### 💣 5. **throw Keyword**

- Used to explicitly throw an exception.
    

```java
throw new FileNotFoundException("File not found!");
```

- Must be declared in method using `throws`:
    

```java
public void read() throws FileNotFoundException {
    throw new FileNotFoundException("File missing");
}
```

---

### 🔐 6. **finally Block**

- Code inside `finally` block always runs regardless of exception or return statement.
    

```java
public int divide(int a, int b) {
    try {
        return a / b;
    } catch (ArithmeticException e) {
        return -1;
    } finally {
        System.out.println("Cleanup/closing resource");
    }
}
```

- Helps avoid resource leaks (e.g., file readers not being closed).
    

---

### 📦 7. **Try-With-Resources (Java 7+)**

- Simplifies resource management (e.g., file streams).
    
- Automatically closes resources that implement `AutoCloseable`.
    

```java
try (BufferedReader br = new BufferedReader(new FileReader("a.txt"))) {
    System.out.println(br.readLine());
} catch (IOException e) {
    e.printStackTrace();
}
```

- No need for finally block to close the stream.
    

---

### 🛠 8. **Custom Exception Handling**

#### 🔹 Step 1: Create Custom Exception

```java
public class InsufficientFundsException extends Exception {
    private double amount;

    public InsufficientFundsException(String message, double amount) {
        super(message);
        this.amount = amount;
    }

    public double getAmount() {
        return amount;
    }
}
```

#### 🔹 Step 2: Use It in Business Logic

```java
public class BankAccount {
    private double balance;

    public BankAccount(double amount) {
        this.balance = amount;
    }

    public void withdraw(double amount) throws InsufficientFundsException {
        if (amount > balance) {
            throw new InsufficientFundsException("Not enough balance", amount);
        }
        balance -= amount;
    }
}
```

#### 🔹 Step 3: Catch the Custom Exception

```java
try {
    BankAccount account = new BankAccount(10);
    account.withdraw(100);
} catch (InsufficientFundsException e) {
    System.out.println("Caught: " + e.getMessage());
    System.out.println("Attempted to withdraw: " + e.getAmount());
}
```

#### 🔹 Optionally Override `toString()`

```java
@Override
public String toString() {
    return "InsufficientFundsException: Tried to withdraw " + amount;
}
```

---

### 🧠 Summary of Concepts Covered

|Concept|Explanation|
|---|---|
|**Multi-catch**|Catch multiple exceptions in one catch block.|
|**Stack trace**|Tracks method calls leading to the exception.|
|**Checked exception**|Must be handled or declared with `throws`.|
|**Unchecked exception**|Occurs at runtime, compiler doesn't enforce.|
|**throws vs throw**|`throws` declares, `throw` generates.|
|**finally block**|Always executes cleanup code.|
|**try-with-resources**|Auto-closes resources like streams/readers.|
|**Custom exceptions**|Used for business-specific exception handling.|



## 🔑 Syntax of `throws`

```java
returnType methodName(params) throws ExceptionType1, ExceptionType2 {
    // method body
}
```

---

## 📌 When to Use `throws`

- When a method **might cause a checked exception**, but you want to **let the caller handle it**.
    
- It's typically used with **checked exceptions** (like `IOException`, `SQLException`).
    

---

## ✅ Example: Using `throws`

```java
import java.io.*;

public class Main {

    // This method may throw FileNotFoundException
    static void readFile() throws FileNotFoundException {
        FileReader fr = new FileReader("nonexistent.txt"); // may throw exception
    }

    public static void main(String[] args) {
        try {
            readFile(); // Caller handles the exception
        } catch (FileNotFoundException e) {
            System.out.println("File not found: " + e.getMessage());
        }
    }
}
```

### 🧾 Output:

```
File not found: nonexistent.txt (The system cannot find the file specified)
```

---

## 🧠 Key Points

|Feature|Description|
|---|---|
|`throws`|Declares an exception|
|Used with|Mostly checked exceptions|
|Who handles?|The **caller** of the method|
|Multiple exceptions|Can declare more than one: `throws IOException, SQLException`|

---

## ❌ Common Misunderstanding

- `throws` **does not throw** the exception itself — it just **declares** that the method might throw it.
    
- To actually throw an exception, use `throw`:
    

```java
throw new IOException("File not found");
```

> 🔁 `throw` — used to **actually throw** an exception  
> 🧾 `throws` — used to **declare** an exception in method signature

---

## ✅ Example: Multiple Exceptions with `throws`

```java
import java.io.*;
import java.sql.SQLException;

public class Main {

    static void riskyMethod() throws IOException, SQLException {
        // just simulating
        if (true) throw new IOException("I/O issue");
        if (false) throw new SQLException("SQL issue");
    }

    public static void main(String[] args) {
        try {
            riskyMethod();
        } catch (IOException | SQLException e) {
            System.out.println("Handled: " + e.getMessage());
        }
    }
}
```

---

## 📝 Summary

|Keyword|Purpose|
|---|---|
|`throws`|Declares that a method might throw exceptions|
|`throw`|Actually throws an exception|
|Best used for|Letting callers handle checked exceptions|

Let me know if you want examples with custom exceptions or how `throws` differs from `try-catch`.