
### **Bitwise Operators in Java**

#### **Overview:**

- **Purpose:** Understanding how to perform bitwise operations in Java.
- **Key Concepts:** Bitwise AND, OR, XOR, NOT, left shift, right shift, and unsigned right shift operators.
- **Data Storage:** Computers store data in binary form (0s and 1s).

#### **Binary Representation:**

- **Example:** `int a = 5;`
  - Binary representation of `5` is `101`.
  - Use `Integer.toBinaryString(a)` to get the binary string.

#### **Bitwise Operators:**

1. **AND (`&`):**
   - **Syntax:** `int c = a & b;`
   - **Operation:** Performs a bitwise AND operation.
   - **Example:** `5 & 4` results in `4` (binary: `100`).
   - **Explanation:** Each bit of the operands is ANDed.

2. **OR (`|`):**
   - **Syntax:** `int c = a | b;`
   - **Operation:** Performs a bitwise OR operation.
   - **Example:** `5 | 4` results in `5` (binary: `101`).
   - **Explanation:** Each bit of the operands is ORed.

3. **XOR (`^`):**
   - **Syntax:** `int c = a ^ b;`
   - **Operation:** Performs a bitwise XOR operation.
   - **Example:** `5 ^ 4` results in `1` (binary: `001`).
   - **Explanation:** Each bit of the operands is XORed.

4. **NOT (`~`):**
   - **Syntax:** `int c = ~a;`
   - **Operation:** Performs a bitwise NOT operation.
   - **Example:** `~5` results in `-6` (binary: `11111111111111111111111111111010`).
   - **Explanation:** Inverts all bits of the operand.

5. **Left Shift (`<<`):**
   - **Syntax:** `int c = a << n;`
   - **Operation:** Shifts the bits of the operand to the left by `n` positions.
   - **Example:** `5 << 1` results in `10` (binary: `1010`).
   - **Explanation:** Shifts bits to the left and fills the right with zeros.

6. **Right Shift (`>>`):**
   - **Syntax:** `int c = a >> n;`
   - **Operation:** Shifts the bits of the operand to the right by `n` positions.
   - **Example:** `5 >> 1` results in `2` (binary: `10`).
   - **Explanation:** Shifts bits to the right and fills the left with the sign bit.

7. **Unsigned Right Shift (`>>>`):**
   - **Syntax:** `int c = a >>> n;`
   - **Operation:** Shifts the bits of the operand to the right by `n` positions.
   - **Example:** `-5 >>> 1` results in a positive number.
   - **Explanation:** Shifts bits to the right and fills the left with zeros, regardless of the sign bit.

#### **Operator Precedence:**

- **Rules:**
  - Bitwise operators have lower precedence than arithmetic operators.
  - Operations with the same precedence are evaluated from left to right.

#### **Key Points:**

- **Binary Representation:** Data is stored in binary form.
- **Bitwise AND (`&`):** ANDs each bit of the operands.
- **Bitwise OR (`|`):** ORs each bit of the operands.
- **Bitwise XOR (`^`):** XORs each bit of the operands.
- **Bitwise NOT (`~`):** Inverts all bits of the operand.
- **Left Shift (`<<`):** Shifts bits to the left.
- **Right Shift (`>>`):** Shifts bits to the right, preserving the sign bit.
- **Unsigned Right Shift (`>>>`):** Shifts bits to the right, filling with zeros.
