
#### **Overview:**

- **Purpose:** Understanding conditional statements, relational operators, and logical operators in Java.
- **Key Concepts:** `if`, `if-else`, `if-else if` (ladder), `switch-case` statements.
- **Applications:** Making decisions based on conditions in your code.

#### **Relational Operators:**

1. **Greater Than (`>`):**
   - **Example:** `a > b`
   - **Explanation:** Checks if `a` is greater than `b`.

2. **Less Than (`<`):**
   - **Example:** `a < b`
   - **Explanation:** Checks if `a` is less than `b`.

3. **Greater Than or Equal To (`>=`):**
   - **Example:** `a >= b`
   - **Explanation:** Checks if `a` is greater than or equal to `b`.

4. **Less Than or Equal To (`<=`):**
   - **Example:** `a <= b`
   - **Explanation:** Checks if `a` is less than or equal to `b`.

5. **Equality (`==`):**
   - **Example:** `a == b`
   - **Explanation:** Checks if `a` is equal to `b`.

6. **Not Equal To (`!=`):**
   - **Example:** `a != b`
   - **Explanation:** Checks if `a` is not equal to `b`.

- **Usage:**
  - Relational operators return a boolean value (`true` or `false`).
  - Can be used with numbers, characters, and strings.
  - **Example:**
    ```java
    int a = 5;
    int b = 10;
    boolean result = a < b; // true
    ```

#### **Logical Operators:**

1. **Logical AND (`&&`):**
   - **Example:** `condition1 && condition2`
   - **Explanation:** Returns `true` if both conditions are `true`.

2. **Logical OR (`||`):**
   - **Example:** `condition1 || condition2`
   - **Explanation:** Returns `true` if at least one condition is `true`.

3. **Logical NOT (`!`):**
   - **Example:** `!condition`
   - **Explanation:** Returns `true` if the condition is `false`.

- **Usage:**
  - Logical operators are used to combine multiple boolean expressions.
  - **Example:**
    ```java
    boolean cond1 = (a > b);
    boolean cond2 = (a < b);
    boolean result = cond1 && cond2; // false
    ```

#### **Conditional Statements:**

1. **`if` Statement:**
   - **Syntax:**
     ```java
     if (condition) {
         // code to execute if condition is true
     }
     ```
   - **Example:**
     ```java
     int age = 20;
     if (age >= 18) {
         System.out.println("You are an adult.");
     }
     ```

2. **`if-else` Statement:**
   - **Syntax:**
     ```java
     if (condition) {
         // code to execute if condition is true
     } else {
         // code to execute if condition is false
     }
     ```
   - **Example:**
     ```java
     int age = 2;
     if (age >= 18) {
         System.out.println("You are an adult.");
     } else {
         System.out.println("You are a child.");
     }
     ```

3. **`if-else if` Ladder:**
   - **Syntax:**
     ```java
     if (condition1) {
         // code to execute if condition1 is true
     } else if (condition2) {
         // code to execute if condition2 is true
     } else {
         // code to execute if none of the conditions are true
     }
     ```
   - **Example:**
     ```java
     int marks = 75;
     if (marks >= 90) {
         System.out.println("Grade A");
     } else if (marks >= 75) {
         System.out.println("Grade B");
     } else if (marks >= 60) {
         System.out.println("Grade C");
     } else {
         System.out.println("Grade D");
     }
     ```

4. **`switch-case` Statement:**
   - **Syntax:**
     ```java
     switch (variable) {
         case value1:
             // code to execute if variable is value1
             break;
         case value2:
             // code to execute if variable is value2
             break;
         default:
             // code to execute if variable does not match any case
     }
     ```
   - **Example:**
     ```java
     int day = 3;
     switch (day) {
         case 1:
             System.out.println("Monday");
             break;
         case 2:
             System.out.println("Tuesday");
             break;
         case 3:
             System.out.println("Wednesday");
             break;
         default:
             System.out.println("Invalid day");
     }
     ```

#### **Key Points:**

- **Relational Operators:** Used to compare values and return boolean results.
- **Logical Operators:** Used to combine multiple boolean expressions.
- **Conditional Statements:** Used to execute code based on conditions.
  - `if`: Executes code if a condition is true.
  - `if-else`: Executes code if a condition is true, else executes alternative code.
  - `if-else if` Ladder: Executes code based on multiple conditions.
  - `switch-case`: Executes code based on the value of a variable.

