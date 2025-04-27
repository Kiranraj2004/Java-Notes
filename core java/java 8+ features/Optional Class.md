

---

## 1. Problem Without Optional

- Suppose you have a method `getName(int id)` that fetches a **name** from a database using an **id**.
    
- Sometimes, the name might not exist for a given id → it may **return `null`**.
    
- If you **directly call `.toUpperCase()`** or any method on the returned value **without checking for null**, it will throw a **NullPointerException**.
    

---

### ❌ Problematic Code:

```java
private static String getName(int id) {
    return null; // Simulating name not found
}

public static void main(String[] args) {
    String name = getName(10);
    System.out.println(name.toUpperCase()); // Throws NullPointerException
}
```

---

## 2. Solution 1: Manual Null Check (but messy)

Before using `name`, always check if it's **not null**.

```java
if (name != null) {
    System.out.println(name.toUpperCase());
}
```

- ✅ Prevents exception.
    
- ❌ But doing this **everywhere manually** is tedious and error-prone.
    

---

## 3. Better Solution: Using **Optional**

- `Optional` is like a **box** that may **contain a value** or **be empty**.
    
- It forces you to **handle nullability properly**.
    

---

### How to Create Optional

|Case|Code|
|---|---|
|Value is guaranteed non-null|`Optional.of(value)`|
|Value might be null|`Optional.ofNullable(value)`|
|Empty optional|`Optional.empty()`|

---

### Example with `Optional`:

```java
private static Optional<String> getName(int id) {
    String name = null; // Simulating DB call
    return Optional.ofNullable(name);
}
```

**Now, while using it:**

```java
Optional<String> name = getName(10);

if (name.isPresent()) {
    System.out.println(name.get().toUpperCase());
}
```

OR better (Java 8+ way):

```java
name.ifPresent(n -> System.out.println(n.toUpperCase()));
```

---

## 4. Important Optional Methods

|Method|Purpose|
|---|---|
|`isPresent()`|Checks if value is present.|
|`ifPresent(Consumer)`|Executes logic if value is present.|
|`get()`|Gets the value inside (be careful: don't use without `isPresent` check).|
|`orElse(default)`|Returns value if present, else returns the provided default.|
|`orElseGet(Supplier)`|Lazily computes default if not present.|
|`orElseThrow()`|Throws an exception if value is not present.|

---

### Example: Default Value Using `orElse`

```java
Optional<String> name = getName(10);

String finalName = name.orElse("Default Name");
System.out.println(finalName); 
```

Output:

```
Default Name
```

---

## 5. Summary of Steps

1. **Change** your method return type to `Optional<Type>`.
    
2. **Wrap** returned value using `Optional.of()` or `Optional.ofNullable()`.
    
3. **Handle** it properly using `ifPresent`, `isPresent`, `orElse`, etc.
    
4. **Avoid direct get()** without checking `isPresent()`.
    

---

# 📜 Full Java Code Example from Transcript

```java
import java.util.Optional;

public class OptionalExample {

    private static Optional<String> getName(int id) {
        // Simulate database fetch
        if (id == 1) {
            return Optional.of("Ram"); // Name found
        } else {
            return Optional.ofNullable(null); // Name not found
        }
    }

    public static void main(String[] args) {

        int id = 2; // Try changing to 1 and 2
        Optional<String> name = getName(id);

        // Using ifPresent with Lambda
        name.ifPresent(n -> System.out.println(n.toUpperCase()));

        // Using Method Reference
        name.ifPresent(System.out::println);

        // Using orElse to provide a default value
        String finalName = name.orElse("Default Name");
        System.out.println("Final Name: " + finalName);

        // Using isPresent and get (not recommended, but for learning)
        if (name.isPresent()) {
            System.out.println("Name is: " + name.get());
        } else {
            System.out.println("Name not found!");
        }

        // Bonus: Using orElseGet (Supplier)
        String finalName2 = name.orElseGet(() -> "Generated Default Name");
        System.out.println("Final Name using orElseGet: " + finalName2);
    }
}
```

---

# 🎯 Outputs

If `id = 1` (name exists):

```
RAM
Ram
Final Name: Ram
Name is: Ram
Final Name using orElseGet: Ram
```

If `id = 2` (name does not exist):

```
Final Name: Default Name
Name not found!
Final Name using orElseGet: Generated Default Name
```

---

# ⚡ Quick Revision Flashcards

|Term|Meaning|
|---|---|
|`Optional.of()`|When you know value is NOT null.|
|`Optional.ofNullable()`|When value MIGHT be null.|
|`Optional.empty()`|Create empty optional.|
|`ifPresent()`|If value is present, do something.|
|`orElse()`|Provide default if value missing.|




---


## Accessing Values from Optional

### 1. `isPresent()`

- Check if a value is present.
    
    ```java
    if (optionalName.isPresent()) {
        System.out.println(optionalName.get());
    }
    ```
    

### 2. `ifPresent(Consumer action)`

- Execute an action if a value is present.
    
    ```java
    optionalName.ifPresent(name -> System.out.println(name.toUpperCase()));
    ```
    
    or using method reference:
    
    ```java
    optionalName.ifPresent(System.out::println);
    ```
    

---

## Providing Default Values

### 3. `orElse(defaultValue)`

- Returns the value if present, otherwise returns the provided `defaultValue`.
    
    ```java
    String result = optionalName.orElse("Default Name");
    ```
    

### 4. `orElseGet(Supplier)`

- Returns the value if present, otherwise executes the supplier and returns its result.
    
    ```java
    String result = optionalName.orElseGet(() -> "Generated Default Name");
    ```
    

### 5. `orElseThrow(Supplier<Exception>)`

- Returns the value if present, otherwise throws an exception supplied by the supplier.
    
    ```java
    String result = optionalName.orElseThrow(() -> new NoSuchElementException("Name not found"));
    ```
    

---

## Transforming Values inside Optional

### 6. `map(Function)`

- Apply a function to the value inside the optional without unwrapping it.
    
    ```java
    Optional<String> upperCaseName = optionalName.map(String::toUpperCase);
    ```
    
- Example of chaining:
    
    ```java
    Optional<Integer> nameLength = optionalName.map(String::length);
    ```
    

---

## 🚀 Full Code Example Based on the Transcript

```java
import java.util.Optional;
import java.util.NoSuchElementException;

public class OptionalDemo {

    public static void main(String[] args) {

        // Example 1: Simple getName simulation
        Optional<String> name = getName(1); // Simulating a DB call

        // 1. Print name if present
        name.ifPresent(System.out::println); // prints Ram

        // 2. Using orElse
        String finalName = name.orElse("Default Name");
        System.out.println(finalName); // prints Ram

        // 3. Using orElseGet
        String anotherName = name.orElseGet(() -> "Generated Default Name");
        System.out.println(anotherName); // prints Ram

        // 4. Using orElseThrow
        String safeName = name.orElseThrow(() -> new NoSuchElementException("Name not found"));
        System.out.println(safeName); // prints Ram

        // 5. Using map to transform inside Optional
        Optional<String> upperCaseName = name.map(String::toUpperCase);
        upperCaseName.ifPresent(System.out::println); // prints RAM

        // 6. Using map to get the length of the name
        Optional<Integer> nameLength = name.map(String::length);
        nameLength.ifPresent(System.out::println); // prints 3

        // Example 2: Simulating null returned from DB
        Optional<String> missingName = getName(2); // Simulate no record

        // 7. Using orElse when no name found
        String defaultedName = missingName.orElse("Default Name Because None Found");
        System.out.println(defaultedName); // prints Default Name Because None Found

        // 8. Using orElseThrow
        try {
            String errorName = missingName.orElseThrow(() -> new NoSuchElementException("No name found for given ID"));
            System.out.println(errorName);
        } catch (Exception e) {
            System.out.println(e.getMessage()); // prints No name found for given ID
        }
    }

    // Simulating a database call
    private static Optional<String> getName(int id) {
        if (id == 1) {
            return Optional.of("Ram");
        } else {
            return Optional.empty(); // No value found
        }
    }
}
```

---

# ✅ Output of this program:

```
Ram
Ram
Ram
Ram
RAM
3
Default Name Because None Found
No name found for given ID
```

---

# 🧠 Quick Summary

|Concept|Code Example|
|---|---|
|Create Optional|`Optional.of(value)` / `Optional.ofNullable(value)` / `Optional.empty()`|
|Check presence|`optional.isPresent()` or `optional.ifPresent()`|
|Provide Default Value|`orElse("default")`, `orElseGet(() -> "default")`|
|Throw Exception if Empty|`orElseThrow(() -> new Exception())`|
|Transform value|`optional.map(function)`|

