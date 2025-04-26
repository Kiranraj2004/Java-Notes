

### 1. **What is a Comparator?**

- A **Comparator** is an **interface** in Java.
    
- It is used to define **custom ordering** for objects when sorting (instead of default natural ordering).
    
- It contains a method:
    
    ```java
    int compare(T o1, T o2);
    ```
    
- This method **compares two objects** of the same type and decides their order:
    
    - If **compare() returns a negative number**: `o1` comes **before** `o2`.
        
    - If **compare() returns 0**: `o1` and `o2` are **equal**.
        
    - If **compare() returns a positive number**: `o1` comes **after** `o2`.
        

---

### 2. **Example 1: Natural Ordering (Ascending by default)**

Suppose you have a list:

```java
List<String> words = Arrays.asList("l", "banana", "date");
words.sort(null); // passing null sorts it in natural ascending order
System.out.println(words);
```

**Output:**

```
[l, banana, date]
```

- Alphabetical (A → Z).
    

---

### 3. **Custom Sorting: Based on String Length**

If you want to **sort strings based on their length**, you need a **custom comparator**.

#### Step-by-step:

✅ Create a class implementing `Comparator<String>`.  
✅ Override `compare()` method with logic: compare based on **string lengths**.

**Code:**

```java
import java.util.*;

class StringLengthComparator implements Comparator<String> {
    @Override
    public int compare(String s1, String s2) {
        return s1.length() - s2.length(); // ascending order based on length
    }
}

public class Main {
    public static void main(String[] args) {
        List<String> words = Arrays.asList("l", "banana", "date");
        
        // Sort using our custom comparator
        words.sort(new StringLengthComparator());
        
        System.out.println(words);
    }
}
```

**Output:**

```
[l, date, banana]
```

- Shortest string first!
    

---

### 4. **Understanding Compare Logic (Important)**

|**Return value from compare()**|**Meaning**|
|:--|:--|
|Negative (e.g., -1)|`o1` comes **before** `o2`|
|Zero (0)|`o1` and `o2` are **equal**|
|Positive (e.g., +1)|`o1` comes **after** `o2`|

---

### 5. **Example 2: Sorting Integers in Descending Order**

Suppose you want integers sorted from high to low.

✅ Create a comparator for `Integer` type.  
✅ In descending order, **larger number comes first**.

**Code:**

```java
import java.util.*;

class MyComparator implements Comparator<Integer> {
    @Override
    public int compare(Integer o1, Integer o2) {
        return o2 - o1; // notice o2 - o1 for descending
    }
}

public class Main {
    public static void main(String[] args) {
        List<Integer> numbers = Arrays.asList(5, 3, 9, 1);
        
        numbers.sort(new MyComparator());
        
        System.out.println(numbers);
    }
}
```

**Output:**

```
[9, 5, 3, 1]
```

- Largest number first!
    

---

### 6. **Quick Tip for Writing compare():**

- **Ascending Order** (Small → Big):  
    `o1 - o2`
    
- **Descending Order** (Big → Small):  
    `o2 - o1`
    

---

### 7. **Example 3: String Length Sorting in Descending Order**

If you want to sort strings based on length, **but longest first**, modify the compare like this:

**Code:**

```java
import java.util.*;

class StringLengthDescendingComparator implements Comparator<String> {
    @Override
    public int compare(String s1, String s2) {
        return s2.length() - s1.length(); // descending by length
    }
}

public class Main {
    public static void main(String[] args) {
        List<String> words = Arrays.asList("l", "banana", "date");
        
        words.sort(new StringLengthDescendingComparator());
        
        System.out.println(words);
    }
}
```

**Output:**

```
[banana, date, l]
```

- Longest string first!
    

---

### 8. **Using Lambda Expressions (Shortcut)**

Instead of creating a separate class, you can use **lambda expressions** to write comparators quickly.

**Ascending order based on length:**

```java
List<String> words = Arrays.asList("l", "banana", "date");

words.sort((s1, s2) -> s1.length() - s2.length());

System.out.println(words);
```

**Descending order based on length:**

```java
List<String> words = Arrays.asList("l", "banana", "date");

words.sort((s1, s2) -> s2.length() - s1.length());

System.out.println(words);
```

---

# 🔥 Summary Shortcut (to Remember)

|**Type**|**What to return in compare()**|
|:--|:--|
|Ascending (Normal)|`o1 - o2`|
|Descending (Reverse)|`o2 - o1`|
|String length ascending|`s1.length() - s2.length()`|
|String length descending|`s2.length() - s1.length()`|

---

# 🧪 Final Combined Code Example (All Concepts)

```java
import java.util.*;

class StringLengthComparator implements Comparator<String> {
    @Override
    public int compare(String s1, String s2) {
        return s1.length() - s2.length(); // ascending by length
    }
}

class MyComparator implements Comparator<Integer> {
    @Override
    public int compare(Integer o1, Integer o2) {
        return o2 - o1; // descending order
    }
}

public class Main {
    public static void main(String[] args) {
        
        List<String> words = Arrays.asList("l", "banana", "date");
        List<Integer> numbers = Arrays.asList(5, 3, 9, 1);

        // 1. Default Natural Sorting
        words.sort(null);
        System.out.println("Natural order (words): " + words);

        // 2. Custom Sorting: String Length Ascending
        words = Arrays.asList("l", "banana", "date");
        words.sort(new StringLengthComparator());
        System.out.println("Sorted by length ascending: " + words);

        // 3. Integer Descending Sorting
        numbers.sort(new MyComparator());
        System.out.println("Numbers sorted descending: " + numbers);

        // 4. String Length Descending using Lambda
        words = Arrays.asList("l", "banana", "date");
        words.sort((s1, s2) -> s2.length() - s1.length());
        System.out.println("Sorted by length descending (Lambda): " + words);
    }
}
```

**Output:**

```
Natural order (words): [banana, date, l]
Sorted by length ascending: [l, date, banana]
Numbers sorted descending: [9, 5, 3, 1]
Sorted by length descending (Lambda): [banana, date, l]
```

---

# 📚 Notes: Sorting a Custom Class (`Student`) using Comparator and Lambda in Java

---

## 1. Problem

You have a class `Student` with attributes `name` and `gpa`. You want to **sort a list of students** based on:

- **GPA** (highest first)
    
- If GPA is the same, then **Name** (alphabetical order)
    

However, **`Student` does not have a natural ordering** (like `String` or `Integer`), so we must **provide a Comparator**.

---

## 2. Key Concepts

- **Natural Ordering**: Built-in types (Integer, String) have it (via `Comparable` interface), custom classes don't unless we implement `Comparable`.
    
- **Comparator**: External class/logic to define a sorting strategy.
    
- **Lambda Expressions**: Short way to write Comparator without creating full classes.
    
- **Method Reference** (`::`): Java 8+ feature to refer to methods cleanly.
    
- **Chaining Comparators**: Use `thenComparing()` to do secondary, tertiary sorting.
    
- **Reversing Order**: Using `reversed()` method.
    

---

## 3. Full Code Examples

### ➡ Basic Setup

```java
import java.util.*;

class Student {
    private String name;
    private double gpa;

    // Constructor
    public Student(String name, double gpa) {
        this.name = name;
        this.gpa = gpa;
    }

    // Getters
    public String getName() {
        return name;
    }

    public double getGpa() {
        return gpa;
    }

    @Override
    public String toString() {
        return "Student{name='" + name + "', gpa=" + gpa + '}';
    }
}
```

---

### ➡ Adding Students

```java
public class Main {
    public static void main(String[] args) {
        List<Student> students = new ArrayList<>();

        students.add(new Student("Alice", 3.5));
        students.add(new Student("Bob", 3.7));
        students.add(new Student("Charlie", 3.5));
        students.add(new Student("Akshit", 3.9));

        // Before Sorting
        System.out.println("Before Sorting:");
        for (Student s : students) {
            System.out.println(s);
        }
    }
}
```

---

### ➡ Sorting by GPA using Lambda Expression (Descending)

```java
// Sorting by GPA (highest GPA first)
students.sort((o1, o2) -> {
    if (o2.getGpa() > o1.getGpa()) return 1;
    else if (o2.getGpa() < o1.getGpa()) return -1;
    else return 0;
});
```

✅ **Output after sorting by GPA descending**:

```
Student{name='Akshit', gpa=3.9}
Student{name='Bob', gpa=3.7}
Student{name='Alice', gpa=3.5}
Student{name='Charlie', gpa=3.5}
```

---

### ➡ Handling Tie: Then sort by Name (Lexical Order)

```java
students.sort((o1, o2) -> {
    if (o2.getGpa() > o1.getGpa()) return 1;
    else if (o2.getGpa() < o1.getGpa()) return -1;
    else {
        return o1.getName().compareTo(o2.getName());
    }
});
```

✅ **Output**:

```
Student{name='Akshit', gpa=3.9}
Student{name='Bob', gpa=3.7}
Student{name='Alice', gpa=3.5}
Student{name='Charlie', gpa=3.5}
```

(Notice Alice appears before Charlie because of name sorting.)

---

### ➡ **Cleaner Java 8+ Version** using Comparator.comparing and Method References

```java
import java.util.Comparator;

// Comparator using method reference and chaining
Comparator<Student> studentComparator = Comparator
    .comparing(Student::getGpa)
    .reversed()
    .thenComparing(Student::getName);

students.sort(studentComparator);
```

✅ **Output will be same** as above.

---

## 4. Important Learnings

|Concept|Meaning|
|:--|:--|
|`Comparator.comparing()`|Comparator based on a method.|
|`reversed()`|Reverse the Comparator's logic.|
|`thenComparing()`|Used for secondary sorting if primary sort is equal.|
|`Method Reference (::)`|Shorter way of writing lambdas like `student -> student.getGpa()` becomes `Student::getGpa`.|

---

## 5. Bonus: Alternative with `Collections.sort()`

Instead of `students.sort(...)`, you can also use:

```java
Collections.sort(students, studentComparator);
```

Both ways work!

---

# 🚀 Full Working Code Together

```java
import java.util.*;

class Student {
    private String name;
    private double gpa;

    public Student(String name, double gpa) {
        this.name = name;
        this.gpa = gpa;
    }

    public String getName() {
        return name;
    }

    public double getGpa() {
        return gpa;
    }

    @Override
    public String toString() {
        return "Student{name='" + name + "', gpa=" + gpa + '}';
    }
}

public class Main {
    public static void main(String[] args) {
        List<Student> students = new ArrayList<>();

        students.add(new Student("Alice", 3.5));
        students.add(new Student("Bob", 3.7));
        students.add(new Student("Charlie", 3.5));
        students.add(new Student("Akshit", 3.9));

        System.out.println("Before Sorting:");
        for (Student s : students) {
            System.out.println(s);
        }

        // Comparator using method reference and chaining
        Comparator<Student> studentComparator = Comparator
            .comparing(Student::getGpa)
            .reversed()
            .thenComparing(Student::getName);

        students.sort(studentComparator);

        System.out.println("\nAfter Sorting:");
        for (Student s : students) {
            System.out.println(s);
        }
    }
}
```

✅ **Output:**

```
Before Sorting:
Student{name='Alice', gpa=3.5}
Student{name='Bob', gpa=3.7}
Student{name='Charlie', gpa=3.5}
Student{name='Akshit', gpa=3.9}

After Sorting:
Student{name='Akshit', gpa=3.9}
Student{name='Bob', gpa=3.7}
Student{name='Alice', gpa=3.5}
Student{name='Charlie', gpa=3.5}
```

---

# 🎯 Summary:

- Custom class needs a Comparator for sorting.
    
- Use lambda for quick logic.
    
- Use `Comparator.comparing`, `reversed()`, and `thenComparing()` for cleaner and powerful sorting.
    
- Understand method references (`::`) for Java 8+ coding.
    

---

Would you also like me to give a small **visual flow diagram** 🎨 showing how sorting happens step-by-step (for even easier memory)? 🚀  
(It's very helpful!)  
Just say "yes"! ✅