
### **Methods in Java**

**Introduction:**
- Methods in Java help in organizing code and avoiding repetition.
- Example: Finding the sum of two numbers without a method requires repeating the code.

**Structure of a Method:**
1. **Access Modifier:** Defines the visibility of the method (e.g., `public`, `private`).
2. **Return Type:** Specifies what the method returns (e.g., `void` for no return, `int` for integer return).
3. **Method Name:** The name of the method.
4. **Parameters:** Inputs to the method, enclosed in parentheses.
5. **Method Body:** The code to be executed, enclosed in curly braces `{}`.

**Example of a Method:**
```java
public static void sumOfArray(int[] arr) {
    int sum = 0;
    for (int num : arr) {
        sum += num;
    }
    System.out.println("Sum: " + sum);
}
```

**Advantages of Methods:**
- Reusability: Write once, use multiple times.
- Maintainability: Easy to update and debug.

**Method Overloading:**
- Allows multiple methods with the same name but different parameters.
- Example:
  ```java
  public static int sum(int a, int b) {
      return a + b;
  }

  public static int sum(int a, int b, int c) {
      return a + b + c;
  }
  ```

**Method Signature:**
- Consists of the method name and the parameter list.
- Does not include the return type.

**Passing Parameters:**
- **Primitive Types:** Passed by value (a copy is made).
- **Objects:** Passed by reference (the reference is copied).

**Example of Passing Objects:**
```java
public static Cat makeCatNameUpperCase(Cat cat) {
    cat.setName(cat.getName().toUpperCase());
    return cat;
}
```

**Variable Arguments (Varargs):**
- Allows a method to accept any number of arguments.
- Syntax: `type... parameterName`
- Example:
  ```java
  public static int sum(int... numbers) {
      int sum = 0;
      for (int num : numbers) {
          sum += num;
      }
      return sum;
  }
  ```

**Command Line Arguments:**
- Passed to the `main` method as an array of strings.
- Example:
  ```java
  public static void main(String[] args) {
      for (String arg : args) {
          System.out.println(arg);
      }
  }
  ```

**Conclusion:**
- Methods help in organizing and reusing code.
- Understanding method overloading, passing parameters, and variable arguments is crucial.
- Command line arguments allow passing inputs to the program from the command line.

---