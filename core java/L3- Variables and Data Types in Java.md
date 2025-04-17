
#### **Overview:**

- **Purpose of Variables:**
  - Variables are used to store data.
  - In Java, variables can store different types of data (e.g., integers, decimals, characters, booleans).

- **Primitive Data Types:**
  - Basic data types provided by Java.
  - Categories: Whole numbers, decimal numbers, characters, and booleans.

#### **Whole Numbers:**

1. **Data Types:**
   - `byte`
   - `short`
   - `int`
   - `long`

2. **Range and Capacity:**
   - **`byte`**: -128 to 127
   - **`short`**: -32,768 to 32,767
   - **`int`**: -2,147,483,648 to 2,147,483,647
   - **`long`**: -9,223,372,036,854,775,808 to 9,223,372,036,854,775,807

3. **Usage:**
   - Choose the data type based on the range of values you need to store.
   - Example: `int age = 20;`

4. **Wrapper Classes:**
   - Used to get the range of primitive data types.
   - Example: `Byte.MIN_VALUE` and `Byte.MAX_VALUE`

#### **Decimal Numbers:**

1. **Data Types:**
   - `float`
   - `double`

2. **Precision:**
   - **`float`**: Approximately 7 decimal digits of precision.
   - **`double`**: Approximately 15 decimal digits of precision.

3. **Usage:**
   - Use `float` for smaller decimal numbers.
   - Use `double` for larger decimal numbers or when more precision is needed.
   - Example: `float salary = 5000.75F;` (Note the `F` suffix for `float`).

4. **Scientific Notation:**
   - Large or small decimal numbers may be represented in scientific notation.
   - Example: `1.4E-45` (very small number).

#### **Characters:**

1. **Data Type:**
   - `char`

2. **Usage:**
   - Stores a single character, symbol, or number.
   - Enclosed in single quotes (`' '`).
   - Example: `char initial = 'A';`

3. **Unicode and ASCII:**
   - Characters are stored as numerical values (Unicode).
   - ASCII is a subset of Unicode (values from 0 to 127).
   - Example: `char heart = '\u2764';` (Unicode for heart symbol).

4. **Type Casting:**
   - Convert `char` to `int` to get the numerical value.
   - Example: `int num = (int) initial;`

#### **Booleans:**

1. **Data Type:**
   - `boolean`

2. **Usage:**
   - Stores `true` or `false`.
   - Used for conditions and flags.
   - Example: `boolean isEligible = true;`

#### **Type Conversion:**

1. **Widening Conversion (Implicit):**
   - Automatically converting a smaller data type to a larger data type.
   - Example: `long b = 10;` (`int` to `long`).

2. **Narrowing Conversion (Explicit):**
   - Manually converting a larger data type to a smaller data type.
   - Requires type casting.
   - Example: `int g = (int) f;` (`float` to `int`).

3. **Potential Data Loss:**
   - Narrowing conversion may result in data loss.
   - Example: Converting `long` to `int` may cause overflow.

#### **Key Concepts:**

- **Variables:** Containers for storing data values.
- **Data Types:** Define the type of data a variable can hold.
- **Type Casting:** Converting one data type to another.
- **Wrapper Classes:** Provide additional functionality for primitive data types.

