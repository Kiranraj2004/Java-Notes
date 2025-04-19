
### 🔑 **Core Concepts of `static` in Java**

#### 1. **What `static` Does**

- Belongs to the **class**, not the instance.
    
- Shared across all objects.
    
- Saves memory — only **one copy** exists.
    

---

#### 2. **Where You Can Use `static`**

- Variables (`static int count`)
    
- Methods (`static void printSomething()`)
    
- Blocks (`static { // code }`)
    
- Nested classes (`static class Helper` — you'll get into this later)
    

---

#### 3. **Use Cases**

##### ✅ Static Variables

- Great for **counters**, like number of objects created.
    

```java
static int count = 0;
```

##### ✅ Static Methods

- Can be called **without creating an object**.
    
- Can't use non-static members directly.
    

```java
public static int max(int a, int b) {
    return a > b ? a : b;
}
```

##### ✅ Static Blocks

- Used for **static initialization logic**.
    

```java
static {
    // Runs once when class is loaded
    System.out.println("Class Loaded");
}
```

##### ✅ Utility Classes

- Example: `Math`, `Collections`, or your own `Utils` with reusable logic like `trimAndCapitalize()`.
    

##### ✅ Singleton Pattern

- Restrict a class to a **single instance**.
    
- Use `static` to provide global access.
    

```java
public class School {
    private static School instance = new School();
    private School() {} // private constructor

    public static School getInstance() {
        return instance;
    }
}
```

---

#### 4. **Rules to Remember**

- Static methods can't access non-static members **directly**.
    
- You can’t use `this` or `super` inside static context.
    
- `main()` is `static` because **JVM calls it directly without object** creation.
    