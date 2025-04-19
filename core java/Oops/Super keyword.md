In Java, the `super` keyword is used to refer to the immediate parent class object. It has several important uses, particularly in the context of inheritance:

1. **Accessing Parent Class Members**:
   - `super` can be used to access variables, methods, and constructors of the parent class. This is especially useful when a subclass has members with the same name as those in the parent class, and you need to differentiate between them.

2. **Invoking Parent Class Constructor**:
   - `super()` is used to call the constructor of the parent class. This is often done in the constructor of the subclass to ensure that the parent class is properly initialized. If a subclass constructor does not explicitly call a parent class constructor using `super()`, the Java compiler automatically inserts a call to the no-argument constructor of the parent class.

3. **Accessing Overridden Methods**:
   - If a subclass overrides a method from its parent class, you can use `super` to call the overridden method in the parent class. This can be useful when you want to extend the functionality of the parent class method rather than completely replacing it.

Here are some examples to illustrate these uses:

### Example 1: Accessing Parent Class Members
```java
class Parent {
    int num = 100;
}

class Child extends Parent {
    int num = 110;

    void printNumber() {
        System.out.println("Child num: " + num);
        System.out.println("Parent num: " + super.num);
    }
}

public class Main {
    public static void main(String[] args) {
        Child child = new Child();
        child.printNumber();
    }
}
```
Output:
```
Child num: 110
Parent num: 100
```

### Example 2: Invoking Parent Class Constructor
```java
class Parent {
    Parent() {
        System.out.println("Parent Constructor");
    }
}

class Child extends Parent {
    Child() {
        super(); // Calls the constructor of Parent class
        System.out.println("Child Constructor");
    }
}

public class Main {
    public static void main(String[] args) {
        Child child = new Child();
    }
}
```
Output:
```
Parent Constructor
Child Constructor
```

### Example 3: Accessing Overridden Methods
```java
class Parent {
    void display() {
        System.out.println("Display method in Parent class");
    }
}

class Child extends Parent {
    @Override
    void display() {
        System.out.println("Display method in Child class");
    }

    void show() {
        display(); // Calls the overridden method in Child class
        super.display(); // Calls the overridden method in Parent class
    }
}

public class Main {
    public static void main(String[] args) {
        Child child = new Child();
        child.show();
    }
}
```
Output:
```
Display method in Child class
Display method in Parent class
```

In these examples, `super` is used to access members of the parent class, invoke the parent class constructor, and call overridden methods in the parent class. This helps in maintaining a clear and organized hierarchy in object-oriented programming.