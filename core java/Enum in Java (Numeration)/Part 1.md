
## ✅ **Enum in Java (Numeration)**

### 🔹 **What is Numeration (Enum)?**

- **Enum (short for Enumeration)** is a special Java type used to define **a collection of constants**.
    
- Examples:
    
    - Days in a week (Sunday to Saturday)
        
    - Months in a year (January to December)
        
    - Departments in a college (CS, IT, Civil, etc.)
        

---

## 🔸 **Why use Enum instead of Strings?**

### ⚠️ Problem with Strings:

When we use string literals repeatedly like `"Monday"`, `"Tuesday"`, etc.:

```java
System.out.println("Monday");
System.out.println("Tuesday");
```

- 🔁 Repetition increases code redundancy.
    
- ❌ High chance of **spelling mistakes**, like `"mondy"` or `"MonDay"`.
    
- ⚠️ IDE warns: _"Duplicated string literals"_
    

### ✅ Better approach: Define constants

#### Approach 1: Using `public static final` constants

```java
public class DayConstants {
    public static final String SUNDAY = "Sunday";
    public static final String MONDAY = "Monday";
    public static final String TUESDAY = "Tuesday";
    // ...and so on
}
```

#### Usage:

```java
System.out.println(DayConstants.MONDAY);
```

#### Pros:

- Reduces redundancy
    
- Centralized definition
    
- Less chance of errors
    

#### Cons:

- Verbose code (need to write data types, equals signs, etc.)
    
- Not grouped logically beyond just strings
    
- Lacks advanced enum features (like ordering, switching, etc.)
    

---

## ✅ **Best Approach: Use `enum`**

### 🔹 Syntax:

```java
enum Day {
    SUNDAY, MONDAY, TUESDAY, WEDNESDAY, THURSDAY, FRIDAY, SATURDAY;
}
```

### 🔹 Usage:

```java
Day today = Day.MONDAY;
System.out.println(today);         // Output: MONDAY
System.out.println(today.name());  // Output: MONDAY
System.out.println(today.ordinal()); // Output: 1
```

---

## 🧠 **Internal Working of Enum**

### Compilation Output:

```java
public final class Day extends Enum<Day> {
    public static final Day SUNDAY = new Day("SUNDAY", 0);
    public static final Day MONDAY = new Day("MONDAY", 1);
    // and so on...

    private Day(String name, int ordinal) {
        super(name, ordinal);
    }
}
```

- **Each enum constant is a final instance of the enum class**
    
- Internally:
    
    ```java
    Day monday = Day.MONDAY;
    ```
    

---

## 📘 **Enum Fields and Methods**

|Method|Description|
|---|---|
|`.name()`|Returns the name of the enum constant|
|`.ordinal()`|Returns the index (starting from 0)|
|`.toString()`|Also returns the name (same as `.name()`)|
|`Enum.valueOf(String)`|Converts a string to enum constant (if exact match)|

---

## 🔄 **Enum vs Interface/Constants**

|Feature|Using Constants (`static final`)|Using `enum`|
|---|---|---|
|Code Size|Larger|Minimal|
|Type Safety|❌ No|✅ Yes|
|Reusability & Maintainability|❌ Poor|✅ Excellent|
|Compiler Support|❌ Weak (just strings)|✅ Strong (compile-time checks)|
|Methods Available|❌ None|✅ `.name()`, `.ordinal()`, etc.|
|Extendable|❌|❌ (enums are `final` classes)|

---

## 🔁 **Use Cases of Enums**

1. **Days of the week**
    
    ```java
    enum Day { SUNDAY, MONDAY, TUESDAY, ... }
    ```
    
2. **Months**
    
    ```java
    enum Month { JANUARY, FEBRUARY, MARCH, ... }
    ```
    
3. **Departments**
    
    ```java
    enum Department { CS, IT, CIVIL, MECHANICAL }
    ```
    

---

## 🧪 Example Code and Output

### Java Code:

```java
public class Main {
    enum Day {
        SUNDAY, MONDAY, TUESDAY, WEDNESDAY, THURSDAY, FRIDAY, SATURDAY;
    }

    public static void main(String[] args) {
        Day d = Day.MONDAY;
        System.out.println("Enum Constant: " + d);              // MONDAY
        System.out.println("Name: " + d.name());                // MONDAY
        System.out.println("Ordinal: " + d.ordinal());          // 1
        System.out.println("ToString: " + d.toString());        // MONDAY

        // Convert String to Enum
        String input = "TUESDAY";
        Day dayFromString = Day.valueOf(input);
        System.out.println("Converted from String: " + dayFromString); // TUESDAY
    }
}
```

### Output:

```
Enum Constant: MONDAY
Name: MONDAY
Ordinal: 1
ToString: MONDAY
Converted from String: TUESDAY
```

---

## 🚀 Summary

|Concept|Description|
|---|---|
|`enum`|Used to define a set of named constants|
|Benefits|Safer, more concise, and expressive than strings|
|Enum Constant|Internally: `public static final Day MONDAY = new Day("MONDAY", 1);`|
|`ordinal()`|Gives position of the constant (0-based)|
|`name()` / `toString()`|Returns the name of the constant as String|
|`valueOf("MONDAY")`|Converts string to enum constant (case-sensitive)|

---

Let me know if you'd like diagrams, UML, or questions based on this content for practice.