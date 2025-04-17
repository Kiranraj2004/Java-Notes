

#### **Overview:**

- **Purpose:** Understanding various methods available for the `String` class in Java.
- **Key Concepts:** Length, character access, equality checks, substrings, case conversions, trimming, replacing, and more.

#### **Basic String Methods:**

1. **Length:**
   - **Syntax:** `int length = string.length();`
   - **Explanation:** Returns the number of characters in the string.
   - **Example:**
     ```java
     String name = "Ram";
     int length = name.length(); // Output: 3
     ```

2. **Character Access (`charAt`):**
   - **Syntax:** `char ch = string.charAt(index);`
   - **Explanation:** Returns the character at the specified index.
   - **Example:**
     ```java
     String name = "Akshit";
     char ch = name.charAt(5); // Output: 't'
     ```
   - **Note:** Index starts from 0. Throws `StringIndexOutOfBoundsException` if the index is out of range.

3. **Equality Check (`equals`):**
   - **Syntax:** `boolean isEqual = string1.equals(string2);`
   - **Explanation:** Compares the content of two strings.
   - **Example:**
     ```java
     String name1 = "Akshit";
     String name2 = "Akshit";
     boolean isEqual = name1.equals(name2); // Output: true
     ```

4. **Case-Insensitive Equality Check (`equalsIgnoreCase`):**
   - **Syntax:** `boolean isEqual = string1.equalsIgnoreCase(string2);`
   - **Explanation:** Compares the content of two strings, ignoring case differences.
   - **Example:**
     ```java
     String name1 = "Akshit";
     String name2 = "akshit";
     boolean isEqual = name1.equalsIgnoreCase(name2); // Output: true
     ```

5. **Lexicographical Comparison (`compareTo`):**
   - **Syntax:** `int result = string1.compareTo(string2);`
   - **Explanation:** Compares two strings lexicographically.
   - **Example:**
     ```java
     String str1 = "remote";
     String str2 = "car";
     int result = str1.compareTo(str2); // Output: 15
     ```
   - **Note:** Returns a positive number if `str1` is lexicographically greater, a negative number if `str1` is lexicographically smaller, and 0 if they are equal.

6. **Substring:**
   - **Syntax:** `String sub = string.substring(beginIndex, endIndex);`
   - **Explanation:** Returns a new string that is a substring of the original string.
   - **Example:**
     ```java
     String name = "Amar Panchal";
     String sub = name.substring(5); // Output: "Panchal"
     ```
   - **Note:** `endIndex` is exclusive.

7. **Case Conversion:**
   - **To Upper Case:** `String upper = string.toUpperCase();`
   - **To Lower Case:** `String lower = string.toLowerCase();`
   - **Example:**
     ```java
     String name = "Amar Panchal";
     String upper = name.toUpperCase(); // Output: "AMAR PANCHAL"
     String lower = name.toLowerCase(); // Output: "amar panchal"
     ```

8. **Trimming Whitespace (`trim`):**
   - **Syntax:** `String trimmed = string.trim();`
   - **Explanation:** Removes leading and trailing whitespace.
   - **Example:**
     ```java
     String name = "  Amar Panchal  ";
     String trimmed = name.trim(); // Output: "Amar Panchal"
     ```

9. **Replacing Characters/Substrings (`replace`):**
   - **Syntax:** `String newString = string.replace(oldChar, newChar);`
   - **Explanation:** Returns a new string with all occurrences of `oldChar` replaced by `newChar`.
   - **Example:**
     ```java
     String name = "Amar Panchal";
     String newName = name.replace("Panchal", "Sharma"); // Output: "Amar Sharma"
     ```

10. **Checking for Substrings (`contains`):**
    - **Syntax:** `boolean contains = string.contains(substring);`
    - **Explanation:** Checks if the string contains the specified substring.
    - **Example:**
      ```java
      String name = "Amar Panchal";
      boolean contains = name.contains("Paan"); // Output: true
      ```

11. **Checking Prefix and Suffix:**
    - **Starts With:** `boolean startsWith = string.startsWith(prefix);`
    - **Ends With:** `boolean endsWith = string.endsWith(suffix);`
    - **Example:**
      ```java
      String name = "Amar Panchal";
      boolean startsWith = name.startsWith("Am"); // Output: true
      boolean endsWith = name.endsWith("al"); // Output: true
      ```

12. **Checking for Empty String (`isEmpty`):**
    - **Syntax:** `boolean isEmpty = string.isEmpty();`
    - **Explanation:** Checks if the string is empty.
    - **Example:**
      ```java
      String name = "";
      boolean isEmpty = name.isEmpty(); // Output: true
      ```

13. **Index Of:**
    - **Syntax:** `int index = string.indexOf(char);`
    - **Explanation:** Returns the index of the first occurrence of the specified character.
    - **Example:**
      ```java
      String name = "Amar Panchal";
      int index = name.indexOf('a'); // Output: 5
      ```

14. **Last Index Of:**
    - **Syntax:** `int index = string.lastIndexOf(char);`
    - **Explanation:** Returns the index of the last occurrence of the specified character.
    - **Example:**
      ```java
      String name = "Amar Panchal";
      int index = name.lastIndexOf('a'); // Output: 10
      ```

15. **Value Of:**
    - **Syntax:** `String str = String.valueOf(object);`
    - **Explanation:** Converts various data types to string.
    - **Example:**
      ```java
      int number = 123;
      String str = String.valueOf(number); // Output: "123"
      ```

16. **Format:**
    - **Syntax:** `String formatted = String.format(format, args);`
    - **Explanation:** Returns a formatted string using the specified format string and arguments.
    - **Example:**
      ```java
      String name = "John";
      int age = 30;
      String formatted = String.format("My name is %s and I am %d years old.", name, age);
      // Output: "My name is John and I am 30 years old."
      ```

#### **Key Points:**

- **String Class:** Strings are objects of the `String` class.
- **String Pool:** Optimizes memory usage for string literals.
- **Immutability:** String methods return new strings; the original string remains unchanged.
- **Common Methods:** `length`, `charAt`, `equals`, `equalsIgnoreCase`, `compareTo`, `substring`, `toUpperCase`, `toLowerCase`, `trim`, `replace`, `contains`, `startsWith`, `endsWith`, `isEmpty`, `indexOf`, `lastIndexOf`, `valueOf`, `format`.

