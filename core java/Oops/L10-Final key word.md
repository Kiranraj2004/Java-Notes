
### 🔒 **The `final` Keyword in Java**

#### ✅ **Where You Can Use It**

|Place Used|Meaning|
|---|---|
|Variable|Value **can’t be changed** (makes it a constant).|
|Method|Method **can’t be overridden** in child classes.|
|Class|Class **can’t be inherited** (no subclassing).|

---

### 📌 **Final Variables**

- Once assigned, **cannot be reassigned**.
    
- Must be initialized **at declaration**, **in constructor**, or **in static block** (if static).
    

#### 🔧 Example:

```java
public final int speedLimit = 200; // Constant instance variable

public static final double PI = 3.14159; // Constant shared across all objects
```

If you try to change it:

```java
PI = 2.34; // ❌ Error: Cannot assign a value to final variable
```

#### 🧠 Smart Tip:

- IntelliJ won’t even show a **setter** for final fields — that’s how smart it is!
    
- Final + Static = **Constant** (Like `public static final double PI = ...`)
    

---

### 🧱 **Final Methods**

- Used to **prevent overriding** by subclasses.
    

#### Example:

```java
public final void airBags() {
    System.out.println("4 Airbags for safety.");
}
```

If a subclass tries to override:

```java
@Override
public void airBags() {
    // ❌ Error: Cannot override final method
}
```

> 👨‍🏭 Use case: Company doesn’t want child classes to **mess with safety features** like airbags.

---

### 🚫 **Final Classes**

- A final class **can’t be extended**.
    

#### Example:

```java
public final class Car {
    // No one can inherit from this class
}
```

Trying to extend:

```java
public class EVCar extends Car {
    // ❌ Error: Cannot inherit from final class
}
```

> 👑 Use case: Premium car brands don’t want anyone to modify or extend their base class.

---

### ❌ **Can Constructors Be Final?**

No! Here’s why:

- **Constructors aren’t inherited**.
    
- You **can’t override** a constructor, so there's **no point** in marking it final.
    
- Trying it results in: `modifier final not allowed here`.
    

---

### 📚 Summary

|Keyword Used On|Prevents|
|---|---|
|Variable|Reassignment|
|Method|Overriding|
|Class|Inheritance|
|Constructor|❌ Not applicable|

---

Would you like a quick quiz or mini-challenges on this to lock it in?