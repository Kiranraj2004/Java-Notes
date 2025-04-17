
#### **Overview:**

- **Purpose:** Understanding the `String` data type in Java.
- **Key Concepts:** Strings as sequences of characters, string literals, string pool, and reference comparison.

#### **String Basics:**

- **Definition:** A `String` is a sequence of characters.
- **Syntax:** `String name = "Vipul";`
- **Usage:** Used to store and manipulate text.

#### **String as a Class:**

- **String Class:** `String` is not a primitive data type; it is a class in Java.
- **Example:** `String name = new String("Vipul");`
- **Explanation:** Strings are objects of the `String` class.

#### **Creating Strings:**

1. **Using `new` Keyword:**
   - **Syntax:** `String name = new String("Vipul");`
   - **Explanation:** Creates a new `String` object in the heap memory.

2. **Using String Literals:**
   - **Syntax:** `String name = "Vipul";`
   - **Explanation:** Java optimizes string literals by storing them in a string pool.

#### **String Pool:**

- **Definition:** A special memory region in the heap where string literals are stored.
- **Purpose:** To optimize memory usage by reusing string literals.
- **Example:**
  ```java
  String a = "Ram";
  String b = "Ram";
  ```
  - Both `a` and `b` refer to the same memory location in the string pool.

#### **Reference Comparison:**

- **Using `==` Operator:**
  - **Syntax:** `if (a == b)`
  - **Explanation:** Compares the memory addresses of the strings, not their content.
  - **Example:**
    ```java
    String a = new String("Ram");
    String b = new String("Ram");
    System.out.println(a == b); // Output: false
    ```
  - **Reason:** `a` and `b` refer to different memory locations.

- **Using String Literals:**
  - **Example:**
    ```java
    String c = "Ram";
    String d = "Ram";
    System.out.println(c == d); // Output: true
    ```
  - **Reason:** `c` and `d` refer to the same memory location in the string pool.

#### **Key Points:**

- **String Class:** Strings are objects of the `String` class.
- **String Pool:** Optimizes memory usage for string literals.
- **Reference Comparison:** Use `==` to compare memory addresses, not content.
- **String Literals:** Reused from the string pool for efficiency.

