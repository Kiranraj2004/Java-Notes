

## 1. **Method Reference ( `::` Operator )**

- **Definition**:  
    Method reference is a shorthand for calling a method without executing it.
    
- **Purpose**:  
    It makes the code **more readable and cleaner**.
    
- **When to Use**:  
    Instead of a lambda expression **only** calling an existing method, we can use method reference.
    

### How it Works:

- **It refers to an existing method**.
    
- **Replaces lambda expressions**, but **only if** the lambda is simply calling a method.
    

---

### 🛠 Example 1: Using Lambda vs Method Reference

**Lambda Way:**

```java
list.forEach(x -> Test.print(x));
```

**Method Reference Way:**

```java
list.forEach(Test::print);
```

Here, `Test::print` is a **method reference** meaning "refer to `print` method inside `Test` class."

---

### 🔥 Important:

- The operator `::` is called the **Method Reference Operator**.
    
- **Static Method**:  
    You can directly use `ClassName::methodName`.
    
- **Non-static Method**:  
    First, create an object and then refer using `object::methodName`.
    

---

## 2. **Constructor Reference**

- **Definition**:  
    Constructor reference allows you to create objects **without using new inside lambda**.
    
- **Syntax**:  
    `ClassName::new`
    
- **Purpose**:  
    Same as method reference but **for constructors** — **creates a new object** in a clean way.
    

---

### 🛠 Example 2: Creating Students from Names

Instead of:

```java
.map(name -> new Student(name))
```

You can simply write:

```java
.map(Student::new)
```

Here, `Student::new` **refers to the constructor** of the `Student` class.

---

# 📜 Full Code Examples

---

## ✨ Example 1: Method Reference with Static Method

```java
import java.util.Arrays;
import java.util.List;

public class Test {

    public static void print(String s) {
        System.out.println(s);
    }

    public static void main(String[] args) {
        List<String> list = Arrays.asList("Alice", "Bob", "Charlie");

        // Using lambda expression
        list.forEach(x -> Test.print(x));

        System.out.println("---");

        // Using method reference
        list.forEach(Test::print);
    }
}
```

### ✅ Output:

```
Alice
Bob
Charlie
---
Alice
Bob
Charlie
```

---

## ✨ Example 2: Method Reference with Non-Static Method

```java
import java.util.Arrays;
import java.util.List;

public class Test {

    public void print(String s) {
        System.out.println(s);
    }

    public static void main(String[] args) {
        List<String> list = Arrays.asList("Alice", "Bob", "Charlie");

        Test test = new Test(); // Create object because method is non-static

        // Using method reference
        list.forEach(test::print);
    }
}
```

### ✅ Output:

```
Alice
Bob
Charlie
```

---

## ✨ Example 3: Constructor Reference with Student Class

```java
import java.util.List;
import java.util.stream.Collectors;
import java.util.stream.Stream;

class Student {
    private String name;

    public Student(String name) {
        this.name = name;
    }

    // Getter for name (optional, for displaying later)
    public String getName() {
        return name;
    }
}

public class Test {

    public static void main(String[] args) {
        List<String> names = List.of("Alice", "Bob", "Charlie");

        // Convert List<String> to List<Student>
        List<Student> students = names.stream()
                                      .map(Student::new)  // Constructor reference
                                      .collect(Collectors.toList());

        // Print student names
        students.forEach(student -> System.out.println(student.getName()));
    }
}
```

### ✅ Output:

```
Alice
Bob
Charlie
```

---

# 🎯 Summary Table

|Concept|Syntax Example|Purpose|
|---|---|---|
|Static Method Reference|`ClassName::methodName`|Use static methods cleanly|
|Non-static Method Reference|`object::methodName`|Use instance methods|
|Constructor Reference|`ClassName::new`|Create objects using constructor|

---

# 🧠 Key Points

- You can replace a lambda that **only calls a method** with a method reference.
    
- Constructor references are used **to create new objects** without writing `new ClassName(x)` manually.
    
- **Method reference** makes code **short, clean, and easy to read**.
    
- **Static** method references need **no object**, but **non-static** method references **need an object**.
    

-