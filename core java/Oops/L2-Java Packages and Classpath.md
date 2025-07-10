

#### **1. What is a Package?**

- A **package** in Java is essentially a folder or directory used to organize classes.
    
- Just as we organize files in folders on our computers, we organize Java classes in packages.
    
- A **package** helps avoid naming conflicts (e.g., having multiple classes named `Cat`).
    

#### **2. Why Use Packages?**

- Packages help avoid class name conflicts. For example:
    
    - You can have a class `Cat` in package `test` and another class `Cat` in package `test2`.
        
    - The JVM will differentiate between the two based on the package they belong to.
        

#### **3. How to Create and Use a Package**

- The package declaration is the first line in a Java class:
    
    ```java
    package test;
    ```
    
- If a class is in a package called `test`, it will be identified by its package name and class name, e.g., `test.Cat`.
    

#### **4. Importing Classes from Other Packages**

- To use classes from another package, **import** them:
    
    ```java
    import test2.Cat;
    ```
    
- Once imported, you can instantiate classes as needed:
    
    ```java
    Cat myCat = new Cat();  // From test2 package
    ```
    

#### **5. Package Naming Convention**

- Java follows a **naming convention** for packages:
    
    - Typically, the package name is written in **lowercase** and follows a domain name structure in reverse.
        
    - Example: `com.companyname.projectname`
        
- For example:
    
    ```java
    package com.engineeringdigest.corejava.animals;
    ```
    

#### **6. Classpath and Package Structure**

- **Classpath** is the directory path that the JVM uses to locate classes and packages.
    
- When running a Java program, you specify the classpath using:
    
    ```bash
    java -cp <path> <class name>
    ```
    
- If the class is within a package, you specify the full path:
    
    ```bash
    java com.engineeringdigest.corejava.test.TestClass
    ```
    
- This tells the JVM where to search for the `TestClass`.

lets say you have created the test package in the src folder inside test package you have  demo class which print hello world in that program first line will be package test;
this tells the class demo is inside the test package  . now you opened the cmd with directory src/test .now compile the demo class using javac demo.java . now if you run the command java demo you will get error`ClassNotFoundException because jvm will not be able to find demo class .as the first line is about the package it tells first go for test then find but we are already in the test directory  .. solution is go to src directory in cmd by doing cd .. then you do java demo  you will get out put  
    

#### **7. Access Modifiers and Visibility**

- A class can be `public` or have **package-private** (default) visibility.
    
- **Public classes** must be named the same as the `.java` file.
    
- Classes that are not `public` (package-private) are visible only within their package.
    

#### **8. Multiple Classes in a Single File**

- Java allows multiple classes in the same `.java` file.
    
- The **public class** must be the same name as the file.
    
- Other classes in the file are **package-private** and accessible only within the same package.
    

#### **9. Inner Classes (Nested Classes)**

- A **nested class** (or inner class) is defined within another class.
    
- You can create an instance of a nested class only after instantiating the enclosing class.
    
    ```java
    OuterClass outer = new OuterClass();
    OuterClass.InnerClass inner = outer.new InnerClass();
    ```
    

#### **10. Practical Example**

- Let’s assume we have a project named `corejava` with packages like `animals` and `vehicles`. Inside `vehicles`, we can have a `Car` class and a `Cycle` class.
    
- The `Cycle` class can be **public** or **package-private**. If it is package-private, it will not be accessible outside its package unless explicitly imported.
    

#### **11. Common Errors**

- **Package Structure and File Name**: If you define a public class, its name must match the file name:
    
    - If the class is named `Car`, the file must be named `Car.java`.
        
    - Otherwise, you will get a compilation error.
        
- **Classpath Error**: When running a program, ensure the classpath is set correctly. If not, the JVM will fail to find the class, resulting in an error like `ClassNotFoundException`.
    

