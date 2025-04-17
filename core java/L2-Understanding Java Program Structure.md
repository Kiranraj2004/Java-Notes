
#### **Overview:**

- **Previous Video Recap:**
  - Created a "Hello, World!" program in Java.
  - Understood the flow: compilation (`.java` to bytecode) and interpretation (bytecode to machine code).
  - Learned about JDK, JVM, and JRE.

- **Current Video Focus:**
  - Understanding the structure and components of a Java program.
  - Keywords and concepts: `class`, `public`, `static`, `void`, `main`, `System.out.println`.

#### **Java Program Structure:**

1. **Class Definition:**
   - **Syntax:** `class Test { ... }`
   - **Explanation:**
     - `class`: Keyword to define a class.
     - `Test`: Name of the class.
     - In Java, all code must be written inside a class.
     - A class serves as a blueprint for creating objects (e.g., `Student`, `Car`, `Laptop`).
     - Properties and behaviors of objects are defined within the class.

2. **Main Method:**
   - **Syntax:** `public static void main(String[] args) { ... }`
   - **Explanation:**
     - **`public`**: Access modifier indicating that the method is accessible from outside the class.
     - **`static`**: Indicates that the method belongs to the class itself, not to instances of the class. It can be called without creating an object.
     - **`void`**: Specifies that the method does not return any value.
     - **`main`**: The name of the method. It is the entry point of the Java program.
     - **`String[] args`**: Parameter that accepts an array of strings (command-line arguments).

3. **Printing to the Console:**
   - **Syntax:** `System.out.println("Hello, World!");`
   - **Explanation:**
     - **`System`**: A final class in the `java.lang` package that provides access to system resources.
     - **`out`**: A static member of `System` that represents the standard output stream (console).
     - **`println`**: Method to print a line of text to the console.
     - **Semicolon (`;`)**: Marks the end of a statement in Java.

#### **Command-Line Arguments:**

- **Purpose:** Pass input to the program when it is run from the command line.
- **Accessing Arguments:**
  - The `args` array in the `main` method stores command-line arguments.
  - Example: `java Test one two`
    - `args[0]` will be `"one"`
    - `args[1]` will be `"two"`

#### **Example Walkthrough:**

1. **Compiling the Program:**
   - Command: `javac Test.java`
   - Generates `Test.class` (bytecode).

2. **Running the Program:**
   - Command: `java Test`
   - Output: `Hello, World!`

3. **Passing Command-Line Arguments:**
   - Command: `java Test Apple Mango`
   - Accessing arguments in the code:
     ```java
     System.out.println(args[0]); // Output: Apple
     System.out.println(args[1]); // Output: Mango
     ```

#### **Key Concepts:**

- **Class:** A blueprint for creating objects.
- **Object:** An instance of a class.
- **Method:** A block of code that performs a specific task.
- **Main Method:** The entry point of a Java program.
- **Access Modifiers:** Control the visibility of classes, methods, and variables (e.g., `public`, `private`).
- **Static:** Belongs to the class rather than instances of the class.
- **Command-Line Arguments:** Input passed to the program when it is run.
