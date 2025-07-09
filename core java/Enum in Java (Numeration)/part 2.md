
## ✅ Java Enums – Advanced Concepts

---

### 🔹 1. **Enum.valueOf(String) Method**

- Converts a string to an enum constant.
    

#### ✅ Example:

```java
Day day = Day.valueOf("MONDAY");
System.out.println(day); // Output: MONDAY
```

#### ⚠️ Case-Sensitive:

```java
Day day = Day.valueOf("monday"); // ❌ Error: No enum constant
```

#### 🔍 Internally:

- `valueOf()` loops through all constants.
    
- If it finds a match (case-sensitive), it returns the enum constant.
    
- If no match, it throws `IllegalArgumentException`.
    

---

### 🔹 2. **Printing an Enum Constant**

- Enums override `toString()` to return the name of the constant.
    

```java
System.out.println(Day.MONDAY);      // MONDAY
System.out.println(Day.MONDAY.name()); // MONDAY
```

---

### 🔹 3. **Day.values(): Getting All Enum Constants**

- Returns all enum constants as an array.
    

#### ✅ Example:

```java
for (Day d : Day.values()) {
    System.out.println(d);
}
```

#### 🔍 Output:

```
SUNDAY
MONDAY
TUESDAY
WEDNESDAY
THURSDAY
FRIDAY
SATURDAY
```

---

### 🔹 4. **Adding Methods and Fields to Enum**

#### ✅ Example:

```java
enum Day {
    SUNDAY("Sunday"),
    MONDAY("Monday"),
    //...

    private String lower;

    Day(String lower) {
        this.lower = lower;
    }

    public void display() {
        System.out.println("Today is: " + this.lower);
    }

    public String getLower() {
        return lower;
    }
}
```

#### 🧠 Key Points:

- Enum constants must be declared first.
    
- Custom fields and constructors are allowed **after** constants.
    
- Constructors in enums are always **private or default**.
    
- Each constant calls the constructor once.
    

#### Usage:

```java
Day.MONDAY.display(); // Today is: Monday
System.out.println(Day.MONDAY.getLower()); // Monday
```

---

### 🔹 5. **Custom Enum Fields with Multiple Parameters**

#### ✅ Example:

```java
enum Day {
    MONDAY("monday", "सोमवार"),
    //...

    private String lower;
    private String hindi;

    Day(String lower, String hindi) {
        this.lower = lower;
        this.hindi = hindi;
    }

    public String getHindi() { return hindi; }
}
```

#### Usage:

```java
System.out.println(Day.MONDAY.getHindi()); // सोमवार
```

---

### 🔹 6. **Enum Constructor Behavior**

- All constants are initialized when the class is loaded.
    
- Constructor is called once for each constant.
    

#### Example Output:

```
Constructor called
Constructor called
...
(7 times for 7 days)
```

---

### 🔹 7. **Using Enums in `switch` Statements**

#### ✅ Old Switch Syntax:

```java
Day today = Day.MONDAY;

switch (today) {
    case MONDAY:
        System.out.println("Today is Monday");
        break;
    case TUESDAY:
        System.out.println("Today is Tuesday");
        break;
    default:
        System.out.println("Weekend!");
}
```

#### ✅ New Switch Syntax (Java 12+):

```java
Day today = Day.MONDAY;
String result = switch (today) {
    case MONDAY -> "M";
    case TUESDAY -> "T";
    default -> "Weekend";
};
System.out.println(result);
```

#### ⚠️ Note:

- New switch expression returns a value.
    
- All cases must be handled or a `default` must be provided.
    
- No need for `break` statements.
    

---

### 🔹 8. **Enums Inside a Class**

#### ✅ Example:

```java
public class Main {
    enum Month {
        JANUARY, FEBRUARY, MARCH
    }

    public static void main(String[] args) {
        System.out.println(Month.JANUARY);
    }
}
```

#### 🔸 Key Points:

- You can declare enums inside classes.
    
- `enum` members are implicitly `static`, so `static` keyword is redundant.
    

---

## ✅ Summary Table

|Feature|Description|
|---|---|
|`valueOf("MONDAY")`|Converts string to enum constant|
|`values()`|Returns array of all constants|
|`.name()`|Returns enum constant name|
|`.ordinal()`|Returns enum constant index|
|Custom Fields|You can define fields like `lower`, `hindi`, etc.|
|Constructors in Enums|Called once per constant; private by default|
|Enum in `switch`|Can be used in traditional and new (arrow) switch cases|
|Enums Inside Classes|Fully supported, usually declared as static|
