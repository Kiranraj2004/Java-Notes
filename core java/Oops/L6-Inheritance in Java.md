
## 📘 **Inheritance in Java – Complete Notes**

---

### 🔹 What is Inheritance?

Inheritance is a mechanism where one class (child class) acquires the properties and behavior (methods and fields) of another class (parent class).

**Types of Inheritance in Java:**

1. **Single Inheritance** - One class inherits from another.
    
2. **Multilevel Inheritance** - A class inherits from a class, which is already a subclass of another class.
    
3. **Hierarchical Inheritance** - Multiple classes inherit from a single parent class.
    
4. **Multiple Inheritance (Not supported with classes)** – Java does **not** support multiple inheritance with classes to avoid ambiguity. It **is supported with interfaces.**
    

---

### 🔹 Method Overriding

- When a subclass provides a specific implementation of a method that is already defined in its superclass.
    
- Signature must be the same.
    

```java
class Animal {
    void sound() {
        System.out.println("Some sound");
    }
}

class Dog extends Animal {
    @Override
    void sound() {
        System.out.println("Bark");
    }
}
```

---

### 🔹 The `@Override` Annotation

- Notation to **ensure** the method is overriding the superclass method correctly.
    
- **Optional**, but using it is a **best practice**.
    
- If method is **not actually overriding**, it gives a **compile-time error**.
    

```java
@Override
void sound() {
    System.out.println("Bark");
}
```

---

### 🔹 The `super` Keyword

Used for:

1. Accessing the **parent class constructor**
    
2. Accessing **parent class methods**
    
3. Accessing **parent class fields** (only if not private)
    

```java
super();                 // Calls parent constructor
super.methodName();      // Calls parent method
super.fieldName;         // Accesses parent field (must not be private)
```

✅ You can use `super()` **anywhere** in the method body, **not just** in constructors.  
⛔ But `super()` must be the **first statement** in a constructor if used.

---

### 🔹 Constructor Chaining

- **When child constructor calls parent constructor**, and parent calls grandparent’s constructor.
    
- All constructors in the hierarchy are called when a child object is created.
    
- But **only one object is created** — that of the child class.
    

```java
class GrandParent {
    GrandParent(int age, String name) { ... }
}

class Parent extends GrandParent {
    Parent(int age, String name) {
        super(age, name);
    }
}

class Child extends Parent {
    Child(int age, String name) {
        super(age, name);
    }
}
```

---

### 🔹 Why can’t we access `private` fields of parent class using `super`?

- Private fields are not accessible outside their own class.
    
- To access them, you need **getters/setters** or make the field protected/public.
    

```java
class GrandParent {
    private int age;     // Not accessible with super.age
}
```

---

### 🔹 Memory Allocation with `new`

- The keyword `new` is used to create objects and dynamically allocate memory in the **heap** at **runtime**, not at compile time.
    
- When you create a child object, only **one object** is created — for the **child class**, and constructor chaining is performed to initialize parent parts.
    

```java
Child c = new Child(20, "Ram");   // Only Child object is created.
```

---

### 🔹 Multiple Inheritance – Why Not in Java (with Classes)?

**Java doesn’t support multiple inheritance with classes** due to the **Diamond Problem**.

#### 💡 Example:

```java
class Camera {
    void powerOn() {
        System.out.println("Camera On");
    }
}

class MusicPlayer {
    void powerOn() {
        System.out.println("Music Player On");
    }
}

class Smartphone extends Camera, MusicPlayer {   // ❌ Not allowed
}
```

- Ambiguity: Which `powerOn()` method should be called?
    
- This is **why Java doesn’t allow extending multiple classes.**
    

Instead, Java uses **Interfaces** to achieve **multiple inheritance** without ambiguity. Interfaces will be explained in future lectures.

---

## ✅ Summary of Key Concepts:

|Concept|Key Point|
|---|---|
|Inheritance|Child class gets properties/methods of parent|
|Method Overriding|Subclass redefines a method of parent class|
|`@Override`|Ensures correct overriding; compile-time error if not valid|
|`super()`|Used to call parent constructor/method/fields|
|Constructor Chaining|Calls constructors from parent → grandparent → etc.|
|Memory with `new`|Dynamic memory allocation on heap at runtime|
|Multiple Inheritance|Not supported with classes in Java to avoid ambiguity|
|Accessing Private Fields|Not possible directly using `super`|

## 🧠 Why Java **does NOT support multiple inheritance (with classes)**

### 🚫 First: What is **multiple inheritance**?

It means a class **inherits from more than one class**.

```cpp
// In C++, this is allowed
class A { };
class B { };
class C : public A, public B { }; // Multiple inheritance
```

But in Java, you **cannot** do this:

```java
class A { }
class B { }

// ❌ Error: Can't extend multiple classes
class C extends A, B { }
```

---

### 🤔 So... why not?

### 1. 💥 **Diamond Problem**

Let’s say both parent classes have a method with the same name. Now if the child class inherits from both — **which version should Java call?**

```java
class A {
    void show() { System.out.println("A"); }
}
class B {
    void show() { System.out.println("B"); }
}

// If C extends A and B, which show() runs?
```

This creates confusion → known as the **Diamond Problem**. Java designers wanted to avoid this confusion altogether.

---

### 2. 🛡️ **Simplicity and Safety**

Java keeps things **clean, simple, and predictable**. Supporting multiple inheritance increases complexity and bugs — so Java chose a safer, simpler path.

---

## ✅ But wait — what about **Interfaces**?

Java **does** support multiple inheritance **via interfaces**, because interfaces don’t carry state — just method **signatures** (until Java 8+, where `default` methods came in, but more on that later if you want 😄).

```java
interface A {
    void hello();
}

interface B {
    void hi();
}

class C implements A, B {
    public void hello() { System.out.println("Hello"); }
    public void hi() { System.out.println("Hi"); }
}
```

✅ No ambiguity  
✅ No state  
✅ Flexible design

---

## 📝 TL;DR

|Feature|Supports Multiple Inheritance?|Why/Why Not|
|---|---|---|
|Classes (`class`)|❌ No|To avoid ambiguity (diamond problem)|
|Interfaces (`interface`)|✅ Yes|Safe, no state, only method signatures|

