

Object-Oriented Programming (OOP) is a programming paradigm based on the concept of "objects." It is a way of structuring programs using classes and objects, which encapsulate both data and behavior.

#### **1. Class and Object**

- **Class:** A blueprint or template to create objects. A class defines the properties (attributes) and behaviors (methods) of the objects created from it.
    
- **Object:** An instance of a class. Once a class is defined, objects can be created, each having its own state (values for properties) and can execute behaviors (methods).
    

Example:

- **Car Class (Blueprint)** might have properties like brand, color, model, and methods like `accelerate()` and `brake()`.
    

```java
class Car {
    String brand;
    String model;
    int speed;

    void accelerate() {
        speed += 10; // Increase speed by 10
    }

    void brake() {
        speed -= 10; // Decrease speed by 10
    }
}
```

#### **2. Properties and Behavior**

- **Properties:** Characteristics of an object (e.g., color, brand, model).
    
- **Behavior:** Actions or methods an object can perform (e.g., accelerate, brake).
    

#### **Creating Objects from Classes:**

- In Java, we create objects using the `new` keyword.
    

Example:

```java
Car myCar = new Car();
myCar.brand = "Tesla";
myCar.model = "Model S";
myCar.speed = 0;
myCar.accelerate();
System.out.println(myCar.speed); // 10
```

---

### **Four Principles (Pillars) of OOP**

1. **Encapsulation**
    
    - **Definition:** Encapsulation is the bundling of data (attributes) and methods (behaviors) into a single unit called a class. It also restricts direct access to some of the object's components, which is often done by making attributes `private`.
        
    - **Purpose:** It hides the internal implementation details and protects the integrity of the data by controlling access via methods (getters and setters).
        
    - **Private vs Public:** Private fields can be accessed or modified only via public methods (getters and setters).
        
    - **Example:** If we don't want external users to modify the car's `year` directly, we make it private and provide a method to set it safely.
        
    
    ```java
    class Car {
        private int year; // Private field
        
        public int getYear() { return year; } // Getter
        public void setYear(int year) { this.year = year; } // Setter
    }
    ```
    
2. **Inheritance**
    
    - **Definition:** Inheritance allows one class (child class) to inherit the attributes and methods of another class (parent class). This promotes code reuse.
        
    - **Example:** If we have an `Animal` class with a method `makeSound()`, both a `Dog` and a `Cat` class can inherit this method and override it with their specific sounds.
        
    
    ```java
    class Animal {
        String name;
        int age;
        
        void makeSound() {
            System.out.println("Some sound");
        }
    }
    
    class Dog extends Animal {
        void makeSound() {
            System.out.println("Woof");
        }
    }
    
    class Cat extends Animal {
        void makeSound() {
            System.out.println("Meow");
        }
    }
    ```
    
3. **Polymorphism**
    
    - **Definition:** Polymorphism allows objects of different classes to be treated as objects of a common parent class. The most common use is when a subclass overrides a method of the superclass, and the correct method is called based on the actual object type.
        
    - **Example:** Even though we declare the reference variable as type `Animal`, the method `makeSound()` will be called based on whether the object is a `Dog` or `Cat`.
        
    
    ```java
    Animal animal1 = new Dog();
    animal1.makeSound(); // Woof
    
    Animal animal2 = new Cat();
    animal2.makeSound(); // Meow
    ```
    
4. **Abstraction**
    
    - **Definition:** Abstraction is the concept of hiding the complex implementation details of a system and exposing only the essential features. The idea is to simplify interactions with the system.
        
    - **Real-life example:** A TV remote is an abstraction. We use the remote without needing to know how the TV works internally.
        
    - **In programming:** Abstraction is achieved through abstract classes or interfaces that declare methods without implementing them. Subclasses are expected to implement the behavior.
        
    
    ```java
    abstract class Animal {
        abstract void makeSound();
    }
    
    class Dog extends Animal {
        void makeSound() {
            System.out.println("Woof");
        }
    }
    ```
    

---

### **Summary of OOP Concepts**

- **OOP** is a paradigm where we deal with classes (blueprints) and objects (instances of classes).
    
- **Class:** A blueprint that defines properties and behaviors.
    
- **Object:** An instance of a class.
    
- **Methods:** Define behaviors (e.g., accelerate, brake).
    
- **Encapsulation:** Bundling of data and methods, with data hiding to protect integrity (using `private` and controlling access with getters and setters).
    
- **Inheritance:** A mechanism to reuse code from a parent class in a child class.
    
- **Polymorphism:** The ability to treat objects of different classes as instances of a common superclass and call the appropriate method based on the object type.
    
- **Abstraction:** Hiding complex implementation details and providing only the necessary interfaces.
    

---

