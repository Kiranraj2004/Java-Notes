

#### **Overview:**

- **Purpose:** Understanding how to perform basic arithmetic operations in Java.
- **Operations Covered:** Addition, subtraction, multiplication, division, and modulus.
- **Key Concepts:** Operator precedence, type conversion, and compound assignment operators.

#### **Basic Arithmetic Operations:**

1. **Addition (`+`):**
   - Example: `int total = salary + bonus;`
   - Adds two numbers.

2. **Subtraction (`-`):**
   - Example: `int total = salary - deduction;`
   - Subtracts one number from another.

3. **Multiplication (`*`):**
   - Example: `int yearlyTotal = monthlyTotal * 12;`
   - Multiplies two numbers.

4. **Division (`/`):**
   - Example: `int perChild = yearlyTotal / 3;`
   - Divides one number by another.
   - **Note:** Division by zero will throw an `ArithmeticException`.

5. **Modulus (`%`):**
   - Example: `int remainder = a % b;`
   - Returns the remainder of the division.

#### **Type Conversion:**

- **Implicit Conversion (Widening):**
  - Automatically converts a smaller data type to a larger data type.
  - Example: `int + double` results in `double`.

- **Explicit Conversion (Narrowing):**
  - Manually converts a larger data type to a smaller data type.
  - Requires type casting.
  - Example: `int g = (int) f;`

#### **Operator Precedence:**

- **Rules:**
  - Parentheses `()` have the highest precedence.
  - Multiplication (`*`), division (`/`), and modulus (`%`) have higher precedence than addition (`+`) and subtraction (`-`).
  - Operations with the same precedence are evaluated from left to right.

- **Examples:**
  - `5 + 3 * 2` evaluates to `11` (multiplication first).
  - `(5 + 3) * 2` evaluates to `16` (parentheses first).

#### **Compound Assignment Operators:**

- **Syntax:** `variable op= expression;`
- **Examples:**
  - `a += 1;` is equivalent to `a = a + 1;`
  - `a -= 1;` is equivalent to `a = a - 1;`
  - `a *= 2;` is equivalent to `a = a * 2;`
  - `a /= 2;` is equivalent to `a = a / 2;`
  - `a %= 2;` is equivalent to `a = a % 2;`

#### **Increment and Decrement Operators:**

- **Increment (`++`):**
  - **Post-increment (`a++`):** Increments the value after the current operation.
  - **Pre-increment (`++a`):** Increments the value before the current operation.

- **Decrement (`--`):**
  - **Post-decrement (`a--`):** Decrements the value after the current operation.
  - **Pre-decrement (`--a`):** Decrements the value before the current operation.

- **Examples:**
  - `int b = a++;` (uses `a` then increments).
  - `int b = ++a;` (increments `a` then uses).

#### **Key Points:**

- **Arithmetic Operations:** Basic operations include addition, subtraction, multiplication, division, and modulus.
- **Type Conversion:** Implicit (widening) and explicit (narrowing) conversions.
- **Operator Precedence:** Rules for evaluating expressions.
- **Compound Assignment Operators:** Shorthand for combining an operation and assignment.
- **Increment and Decrement Operators:** Pre- and post-increment/decrement.

