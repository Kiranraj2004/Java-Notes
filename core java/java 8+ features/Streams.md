
# 📚 Java Stream  - Detailed Notes

---

## 🔥 1. What is  Stream?

- **Stream** is a **sequence of elements** obtained from a **collection** (like List, Set, etc.).
    
- After converting a collection into a stream, we can perform operations like **filtering**, **mapping**, **reducing**, etc., in a **declarative** and **functional programming style**.
    
- **Declarative Programming** = **What** to do, not **How** to do.
    
- **Functional Programming** = Passing functions (e.g., **Predicate**, **Function**) inside stream operations.
    

---

## 🔥 2. Why use Stream?

- To **work with collections** in a **cleaner, readable, flexible**, and **parallelizable** way.
    
- Advantages:
    
    - **Readability**: Code becomes shorter and more understandable.
        
    - **Flexibility**: Multiple operations (filter, map, reduce) can be chained easily.
        
    - **Parallelism**: Streams can be processed using multiple threads automatically.
        
    - **Encapsulation**: You don’t have to worry about loops, iteration, etc.
        

---

## 🔥 3. Imperative vs Declarative Style

**Imperative Style (Old Traditional Way)**

```java
List<Integer> list = Arrays.asList(1, 2, 3, 4, 5, 6);
int sum = 0;
for (int num : list) {
    if (num % 2 == 0) {
        sum += num;
    }
}
System.out.println("Sum of even numbers: " + sum);
```

✅ Output:

```
Sum of even numbers: 12
```

---

**Declarative Style (Using Stream API)**

```java
List<Integer> list = Arrays.asList(1, 2, 3, 4, 5, 6);

int sum = list.stream()
              .filter(num -> num % 2 == 0)
              .mapToInt(Integer::intValue)
              .sum();

System.out.println("Sum of even numbers: " + sum);
```

✅ Output:

```
Sum of even numbers: 12
```

---

Notice:

- Here `filter` automatically handles checking even numbers.
    
- `mapToInt` helps to convert from object stream to primitive stream for efficient sum.
    

---

## 🔥 4. How to Create Stream 

### 4.1 From a **List**

```java
List<String> names = Arrays.asList("Ram", "Shyam", "Mohan");

Stream<String> nameStream = names.stream();
```

---

### 4.2 From an **Array**

```java
String[] arr = {"Ram", "Shyam", "Mohan"};

Stream<String> arrStream = Arrays.stream(arr);
```

---

### 4.3 Directly using **Stream.of()**

```java
Stream<Integer> numStream = Stream.of(1, 2, 3, 4, 5);
```

---

### 4.4 Using **Stream.iterate()** (For sequence generation)

```java
Stream<Integer> numbers = Stream.iterate(0, n -> n + 1)
                                 .limit(10);

numbers.forEach(System.out::println);
```

✅ Output:

```
0
1
2
3
4
5
6
7
8
9
```

**Explanation:**

- `0` is the starting point.
    
- `n -> n + 1` is a **UnaryOperator** which adds 1 to the previous number.
    
- `limit(10)` ensures only 10 numbers are generated.
    

---

### 4.5 Using **Stream.generate()** (Infinite generation with Supplier)

```java
Stream<String> stream = Stream.generate(() -> "Hello")
                              .limit(5);

stream.forEach(System.out::println);
```

✅ Output:

```
Hello
Hello
Hello
Hello
Hello
```

---

✅ Another example: Generating random numbers

```java
Stream<Integer> randomNumbers = Stream.generate(() -> (int)(Math.random() * 100))
                                      .limit(5);

randomNumbers.forEach(System.out::println);
```

✅ Output: (Random output, sample)

```
45
3
78
12
91
```

---

## 🔥 5. Quick Summary: 5 Ways to Create Stream

|Way|Example|
|---|---|
|From List|`list.stream()`|
|From Array|`Arrays.stream(array)`|
|Using Stream.of()|`Stream.of(1, 2, 3, 4)`|
|Using Stream.iterate()|`Stream.iterate(0, n -> n + 1).limit(5)`|
|Using Stream.generate()|`Stream.generate(() -> "Hello").limit(5)`|

---

## 🔥 6. Important Concepts (Quick Revision)

|Concept|Meaning|
|---|---|
|Predicate|Function returning true/false. (Used in `filter`)|
|Function|Takes one argument, returns one result. (Used in `map`)|
|Supplier|Takes no argument, returns a value. (Used in `generate`)|
|Consumer|Takes one argument, returns nothing. (Used in `forEach`)|
|UnaryOperator|Takes and returns same type. (Used in `iterate`)|

---

# 🚀 Final Full Code Example

Let's combine everything into a complete runnable Java program:

```java
import java.util.*;
import java.util.stream.Stream;

public class StreamExample {
    public static void main(String[] args) {
        // 1. Creating Stream from List
        List<String> names = Arrays.asList("Ram", "Shyam", "Mohan");
        Stream<String> nameStream = names.stream();
        nameStream.forEach(System.out::println);
        
        // 2. Creating Stream from Array
        String[] arr = {"Ram", "Shyam", "Mohan"};
        Stream<String> arrStream = Arrays.stream(arr);
        arrStream.forEach(System.out::println);
        
        // 3. Stream.of() Example
        Stream<Integer> numStream = Stream.of(1, 2, 3, 4, 5);
        numStream.forEach(System.out::println);
        
        // 4. Stream.iterate() Example
        Stream<Integer> iteratedStream = Stream.iterate(0, n -> n + 1)
                                               .limit(10);
        iteratedStream.forEach(System.out::println);
        
        // 5. Stream.generate() Example
        Stream<String> generatedStream = Stream.generate(() -> "Hello")
                                               .limit(5);
        generatedStream.forEach(System.out::println);
        
        // 6. Random numbers using Stream.generate()
        Stream<Integer> randomNumbers = Stream.generate(() -> (int)(Math.random() * 100))
                                              .limit(5);
        randomNumbers.forEach(System.out::println);
    }
}
```

✅ Output: (sample)

```
Ram
Shyam
Mohan
Ram
Shyam
Mohan
1
2
3
4
5
0
1
2
3
4
5
6
7
8
9
Hello
Hello
Hello
Hello
Hello
23
45
67
89
12
```

---

# ✅ Conclusion:

- You can **convert any collection to Stream** easily.
    
- **Declarative** and **functional** style makes Java much cleaner.
    
- Streams can be created **directly** using `Stream.of()`, `Stream.iterate()`, `Stream.generate()`, etc.
    
- **Streams are powerful** when working with large data collections or parallel processing.



## 1. **Starting with a List**

You have a list like:

```java
List<Integer> list = Arrays.asList(1, 2, 3, 2, 1, 6, 1, 0, 2, 2);
```

We want to perform various operations using **Streams** instead of old traditional for-loops.

---

## 2. **Stream Basics**

- Convert a `List` into a `Stream` using `list.stream()`.
    
- Then perform a chain of operations like `filter`, `map`, etc.
    

---

## 3. **Filter Operation**

**Purpose:** Select only even numbers.

**Code:**

```java
List<Integer> filteredList = list.stream()
    .filter(x -> x % 2 == 0)
    .collect(Collectors.toList());

System.out.println(filteredList);
```

**Output:**

```
[2, 2, 6, 0, 2, 2]
```

> **filter** needs a **predicate** → (a condition returning true/false).

---

## 4. **Map Operation**

**Purpose:** After filtering, divide every element by 2.

**Code:**

```java
List<Integer> mappedList = filteredList.stream()
    .map(x -> x / 2)
    .collect(Collectors.toList());

System.out.println(mappedList);
```


```java
// if we dont write the collect(Collectors.toList()) it will return stream in order to get the list use the above one 
Stream<Integer> mappedList = filteredList.stream()
    .map(x -> x / 2)
    ;

System.out.println(mappedList);
```

**Output:**

```
[1, 1, 3, 0, 1, 1]
```

> **map** is used to **transform** each element.

---

## 5. **Distinct Operation**

**Purpose:** Remove duplicate elements.

**Code:**

```java
List<Integer> distinctList = mappedList.stream()
    .distinct()
    .collect(Collectors.toList());

System.out.println(distinctList);
```

**Output:**

```
[1, 3, 0]
```

---

## 6. **Sorted Operation**

**Ascending Sort:**

```java
List<Integer> sortedList = distinctList.stream()
    .sorted()
    .collect(Collectors.toList());

System.out.println(sortedList);
```

**Output:**

```
[0, 1, 3]
```

---

**Descending Sort:**

```java
List<Integer> sortedDescList = distinctList.stream()
    .sorted((a, b) -> b - a)
    .collect(Collectors.toList());

System.out.println(sortedDescList);
```

**Output:**

```
[3, 1, 0]
```

---

## 7. **Limit Operation**

**Purpose:** Get only first `N` elements.

```java
List<Integer> limitedList = sortedDescList.stream()
    .limit(2)
    .collect(Collectors.toList());

System.out.println(limitedList);
```

**Output:**

```
[3, 1]
```

---

## 8. **Skip Operation**

**Purpose:** Skip first `N` elements.

```java
List<Integer> skippedList = sortedDescList.stream()
    .skip(1)
    .collect(Collectors.toList());

System.out.println(skippedList);
```

**Output:**

```
[1, 0]
```

---

## 9. **Peek Operation**

**Purpose:** Just for debugging.  
It allows you to _see_ elements inside the stream at that point.

```java
List<Integer> peekedList = sortedDescList.stream()
	    .peek(x -> System.out.println("Element: " + x))
    .collect(Collectors.toList());
```

- It **prints elements** during streaming but **does not modify** anything.
    

---

## 10. **Generating Range using IntStream.range**

**Create 0 to 100 numbers:**

```java
List<Integer> rangeList = IntStream.range(0, 101)
    .boxed()
    .collect(Collectors.toList());

System.out.println(rangeList);
```

**Skip 0, start from 1:**

```java
List<Integer> oneToHundred = IntStream.range(0, 101)
    .skip(1)
    .boxed()
    .collect(Collectors.toList());

System.out.println(oneToHundred);
```

**Output:**  
`[1, 2, 3, ..., 100]`

---

## 11. **Terminal Operations**

Terminal operations are the final operations to produce a result.

### a) `count()`

```java
long count = oneToHundred.stream()
    .count();

System.out.println(count);
```

**Output:**

```
100
```

---

### b) `max()`

```java
Optional<Integer> maxElement = oneToHundred.stream()
    .max((a, b) -> a - b);

System.out.println(maxElement.get());
```

**Output:**

```
100
```

(Need `.get()` because `max` returns an `Optional`.)

---

### c) `min()` using `max()` with comparator tweak

If you reverse comparator `(b - a)` then you get minimum value instead of maximum.

---

## Full Code Combining Everything ✨

```java
import java.util.*;
import java.util.stream.*;

public class StreamExample {
    public static void main(String[] args) {
        
        List<Integer> list = Arrays.asList(1, 2, 3, 2, 1, 6, 1, 0, 2, 2);
        
        // Filter even numbers
        List<Integer> filteredList = list.stream()
            .filter(x -> x % 2 == 0)
            .collect(Collectors.toList());
        
        System.out.println("Filtered List: " + filteredList);
        
        // Map: divide by 2
        List<Integer> mappedList = filteredList.stream()
            .map(x -> x / 2)
            .collect(Collectors.toList());
        
        System.out.println("Mapped List: " + mappedList);
        
        // Distinct
        List<Integer> distinctList = mappedList.stream()
            .distinct()
            .collect(Collectors.toList());
        
        System.out.println("Distinct List: " + distinctList);
        
        // Sorted descending
        List<Integer> sortedDescList = distinctList.stream()
            .sorted((a, b) -> b - a)
            .collect(Collectors.toList());
        
        System.out.println("Sorted Descending List: " + sortedDescList);
        
        // Limit to 2 elements
        List<Integer> limitedList = sortedDescList.stream()
            .limit(2)
            .collect(Collectors.toList());
        
        System.out.println("Limited List: " + limitedList);
        
        // Skip 1 element
        List<Integer> skippedList = sortedDescList.stream()
            .skip(1)
            .collect(Collectors.toList());
        
        System.out.println("Skipped List: " + skippedList);
        
        // Range from 1 to 100
        List<Integer> oneToHundred = IntStream.range(0, 101)
            .skip(1)
            .boxed()
            .collect(Collectors.toList());
        
        System.out.println("One to Hundred List: " + oneToHundred);
        
        // Count
        long count = oneToHundred.stream()
            .count();
        
        System.out.println("Count: " + count);
        
        // Max
        Optional<Integer> maxElement = oneToHundred.stream()
            .max((a, b) -> a - b);
        
        System.out.println("Max Element: " + maxElement.get());
    }
}
```

---

# ✨ OUTPUT:

```text
Filtered List: [2, 2, 6, 0, 2, 2]
Mapped List: [1, 1, 3, 0, 1, 1]
Distinct List: [1, 3, 0]
Sorted Descending List: [3, 1, 0]
Limited List: [3, 1]
Skipped List: [1, 0]
One to Hundred List: [1, 2, 3, ..., 100]
Count: 100
Max Element: 100
```

---

# 🎯 Summary:

|Operation|Meaning|
|---|---|
|filter()|Condition checking|
|map()|Transformation|
|distinct()|Remove duplicates|
|sorted()|Ascending/Descending sort|
|limit()|Get first N elements|
|skip()|Skip first N elements|
|peek()|Debugging/logging|
|collect()|Gather into List/Set/Map|
|max()/min()|Find max/min using comparator|
|count()|Count the number of elements|



## 1. **Introduction to Stream (Sarita)**

- **Stream** is a sequence of elements supporting sequential and parallel aggregate operations.
    
- **Why Stream?**
    
    - To perform complex operations like _filtering_, _mapping_, _reducing_, etc., **declaratively**.
        
    - We avoid _for loops_ and write clean, readable code.
        

---

## 2. **Creating a Stream**

- From a **List**:
    
    ```java
    List<Integer> list = Arrays.asList(1, 2, 3, 4, 5);
    Stream<Integer> stream = list.stream(); // sequential stream
    ```
    
- From an **Array**:
    
    ```java
    int[] arr = {1, 2, 3};
    Arrays.stream(arr);
    ```
    

---

## 3. **Common Stream Operations**

### a) **Filter**

_Select elements based on a condition (predicate)_

```java
List<Integer> evenNumbers = list.stream()
    .filter(x -> x % 2 == 0)
    .collect(Collectors.toList());
System.out.println(evenNumbers);
```

🖨 Output:

```
[2, 4]
```

---

### b) **Map**

_Transform each element._

```java
List<Integer> squares = list.stream()
    .map(x -> x * x)
    .collect(Collectors.toList());
System.out.println(squares);
```

🖨 Output:

```
[1, 4, 9, 16, 25]
```

---

### c) **Distinct**

_Remove duplicate elements._

```java
List<Integer> distinctList = Arrays.asList(1, 2, 2, 3, 3, 4).stream()
    .distinct()
    .collect(Collectors.toList());
System.out.println(distinctList);
```

🖨 Output:

```
[1, 2, 3, 4]
```

---

### d) **Sorted**

- Ascending (default):
    
    ```java
    List<Integer> sortedList = list.stream()
        .sorted()
        .collect(Collectors.toList());
    System.out.println(sortedList);
    ```
    
- Descending:
    
    ```java
    List<Integer> sortedDesc = list.stream()
        .sorted((a, b) -> b - a)
        .collect(Collectors.toList());
    System.out.println(sortedDesc);
    ```
    

🖨 Output (descending):

```
[5, 4, 3, 2, 1]
```

---

### e) **Limit and Skip**

- **Limit**: take only the first N elements
    
- **Skip**: skip first N elements
    

```java
List<Integer> limited = list.stream()
    .limit(3)
    .collect(Collectors.toList());
System.out.println(limited);  // [1, 2, 3]

List<Integer> skipped = list.stream()
    .skip(2)
    .collect(Collectors.toList());
System.out.println(skipped);  // [3, 4, 5]
```

---

### f) **Peek**

- Intermediate operation to **perform action on elements** (usually for debugging)
    

```java
list.stream()
    .peek(x -> System.out.println("Processing: " + x))
    .collect(Collectors.toList());
```

- Doesn't change the data, only **"peeks"** at it.
    

---

### g) **Collect**

- Terminal operation to **collect** the results into a List, Set, Map, etc.
    

```java
List<Integer> collected = list.stream()
    .collect(Collectors.toList());
```

---

### h) **Max, Min, Count**

```java
Optional<Integer> max = list.stream().max((a, b) -> a - b);
System.out.println(max.get()); // 5

long count = list.stream().count();
System.out.println(count); // 5
```

---

## 4. **Parallel Stream**

- Parallel processing using multiple threads automatically
    
- Create using:
    
    ```java
    list.parallelStream()
    ```
    
- ⚡ **Use when** the list is very big.
    
- ⚡ **Not recommended for small lists** → overhead of splitting into threads makes it slower!
    

---

## 5. **Putting All Together: Full Code Example**

```java
import java.util.*;
import java.util.stream.*;

public class StreamExample {
    public static void main(String[] args) {
        
        List<Integer> list = Arrays.asList(1, 2, 3, 2, 1, 6, 1, 0, 2, 2);
        
        // Step 1: Filter even numbers
        List<Integer> evenList = list.stream()
            .filter(x -> x % 2 == 0)
            .collect(Collectors.toList());
        System.out.println("Filtered Even List: " + evenList);
        
        // Step 2: Map - divide each by 2
        List<Integer> mappedList = evenList.stream()
            .map(x -> x / 2)
            .collect(Collectors.toList());
        System.out.println("Mapped List (Divided by 2): " + mappedList);

        // Step 3: Distinct
        List<Integer> distinctList = mappedList.stream()
            .distinct()
            .collect(Collectors.toList());
        System.out.println("Distinct List: " + distinctList);

        // Step 4: Sorted (Descending)
        List<Integer> sortedDesc = distinctList.stream()
            .sorted((a, b) -> b - a)
            .collect(Collectors.toList());
        System.out.println("Sorted Descending: " + sortedDesc);

        // Step 5: Limit to first 4 elements
        List<Integer> limitedList = sortedDesc.stream()
            .limit(4)
            .collect(Collectors.toList());
        System.out.println("Limited List (First 4 Elements): " + limitedList);

        // Step 6: Skip first element
        List<Integer> skippedList = limitedList.stream()
            .skip(1)
            .collect(Collectors.toList());
        System.out.println("Skipped First Element: " + skippedList);

        // Step 7: Max Value
        Integer maxValue = skippedList.stream()
            .max((a, b) -> a - b)
            .get();
        System.out.println("Max Value: " + maxValue);

        // Step 8: Count
        long count = skippedList.stream()
            .count();
        System.out.println("Count: " + count);
    }
}
```

### ✅ Output:

```
Filtered Even List: [2, 2, 6, 0, 2, 2]
Mapped List (Divided by 2): [1, 1, 3, 0, 1, 1]
Distinct List: [1, 3, 0]
Sorted Descending: [3, 1, 0]
Limited List (First 4 Elements): [3, 1, 0]
Skipped First Element: [1, 0]
Max Value: 1
Count: 2
```

---

# 🎯 **Summary of Stream Methods Covered**

|Method|Purpose|
|---|---|
|`.filter()`|Keep elements that match condition|
|`.map()`|Transform elements|
|`.distinct()`|Remove duplicates|
|`.sorted()`|Sort the elements|
|`.limit(n)`|Take first `n` elements|
|`.skip(n)`|Skip first `n` elements|
|`.peek()`|Debug/observe elements|
|`.collect()`|Gather result into List/Set/Map|
|`.max()`|Find maximum element|
|`.count()`|Find number of elements|
|`.parallelStream()`|Use multithreading automatically|

---

# ⚡ Bonus Example: Parallel Stream

```java
List<Integer> bigList = new ArrayList<>();
for (int i = 0; i < 1_000_000; i++) {
    bigList.add(i);
}

// Parallel processing
long count = bigList.parallelStream()
    .filter(x -> x % 2 == 0)
    .count();

System.out.println("Even number count: " + count);
```

✅ Output:

```
Even number count: 500000
```

---

# 🎁 **Key Tips**

- Use **normal `.stream()`** for small to medium size collections.
    
- Use **`.parallelStream()`** for large collections.
    
- Always close your stream operations with a **terminal operation** like `.collect()`, `.count()`, `.max()`, etc.
    

---

Would you also like me to give a **small diagram** showing **Stream pipeline flow** visually (input -> operations -> output)? 🚀  
It will make it even easier to remember!  
Shall I send it? 🎨