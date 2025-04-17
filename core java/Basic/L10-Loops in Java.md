
#### **Overview:**

- **Purpose:** Understanding different types of loops in Java and their applications.
- **Key Concepts:** `while` loop, `do-while` loop, `for` loop, nested loops, `break`, and `continue` statements.
- **Applications:** Repeating tasks, iterating over data, and controlling flow in programs.

#### **Types of Loops:**

1. **`while` Loop:**
   - **Syntax:**
     ```java
     while (condition) {
         // code to execute repeatedly
     }
     ```
   - **Example:**
     ```java
     int i = 0;
     while (i < 10) {
         System.out.println("Hello, World!");
         i++;
     }
     ```
   - **Explanation:** The code inside the `while` loop executes repeatedly as long as the condition is `true`.

2. **`do-while` Loop:**
   - **Syntax:**
     ```java
     do {
         // code to execute repeatedly
     } while (condition);
     ```
   - **Example:**
     ```java
     int i = 0;
     do {
         System.out.println("Hello, World!");
         i++;
     } while (i < 10);
     ```
   - **Explanation:** The code inside the `do-while` loop executes at least once, and then repeatedly as long as the condition is `true`.

3. **`for` Loop:**
   - **Syntax:**
     ```java
     for (initialization; condition; update) {
         // code to execute repeatedly
     }
     ```
   - **Example:**
     ```java
     for (int i = 0; i < 10; i++) {
         System.out.println("Hello, World!");
     }
     ```
   - **Explanation:** The `for` loop combines initialization, condition checking, and updating in a single line.

#### **Nested Loops:**

- **Syntax:**
  ```java
  for (int i = 0; i < 10; i++) {
      for (int j = 0; j < 10; j++) {
          System.out.println("i = " + i + ", j = " + j);
      }
  }
  ```
- **Example:**
  ```java
  for (int i = 1; i <= 5; i++) {
      for (int j = 1; j <= i; j++) {
          System.out.print("* ");
      }
      System.out.println();
  }
  ```
- **Explanation:** Nested loops allow you to execute an inner loop for each iteration of an outer loop. Useful for generating patterns and matrices.

#### **Control Statements:**

1. **`break` Statement:**
   - **Syntax:** `break;`
   - **Usage:** Exits the nearest enclosing loop or switch statement.
   - **Example:**
     ```java
     for (int i = 0; i < 100; i++) {
         if (i == 50) {
             break;
         }
         System.out.println(i);
     }
     ```

2. **`continue` Statement:**
   - **Syntax:** `continue;`
   - **Usage:** Skips the current iteration and proceeds to the next iteration of the loop.
   - **Example:**
     ```java
     for (int i = 0; i < 10; i++) {
         if (i == 5) {
             continue;
         }
         System.out.println(i);
     }
     ```

#### **Key Points:**

- **Loops:** Used to repeat a block of code multiple times.
- **`while` Loop:** Executes as long as the condition is `true`.
- **`do-while` Loop:** Executes at least once and then as long as the condition is `true`.
- **`for` Loop:** Combines initialization, condition checking, and updating in one line.
- **Nested Loops:** Useful for iterating over multi-dimensional data structures.
- **`break` Statement:** Exits the nearest enclosing loop or switch statement.
- **`continue` Statement:** Skips the current iteration and proceeds to the next iteration.

