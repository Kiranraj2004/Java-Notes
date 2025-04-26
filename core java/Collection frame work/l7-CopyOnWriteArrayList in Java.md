
## 1. **Problem Statement**

- **ArrayList** and **LinkedList** are **not thread-safe**.  
    ➔ If multiple threads modify them concurrently, **inconsistent results** or **exceptions** occur.
    
- **Vector** and **Stack** are thread-safe (**synchronized**) but they **lock** the entire structure, reducing performance.
    

---

## 2. **Solution: CopyOnWriteArrayList**

- Java provides **`CopyOnWriteArrayList`** to handle concurrent modifications safely **without locking the entire list**.
    

---

## 3. **Meaning of "CopyOnWrite"**

- **"Copy On Write"** means:  
    ➔ **During a write operation** (add, remove, set):
    
    - A **new copy** of the list is created.
        
    - Changes are made to the **new copy**.
        
    - Meanwhile, **readers** continue reading the **original list** **without being affected**.
        

---

## 4. **Behavior Overview**

|Operation Type|Behavior|
|:--|:--|
|**Read**|Very fast; reads from the current snapshot|
|**Write**|Slower; makes a new copy of the entire list|

---

## 5. **Important Point**

- **Use CopyOnWriteArrayList when:**
    
    - Reads are frequent.
        
    - Writes (modifications) are rare.
        
- **Not good** if many writes occur ➔ **Memory overhead** due to frequent copying.
    

---

# ✍ Example 1: Modification during Iteration

### Without CopyOnWriteArrayList (Fails)

```java
import java.util.ArrayList;
import java.util.List;

public class ListDemo {
    public static void main(String[] args) {
        List<String> shoppingList = new ArrayList<>();
        shoppingList.add("Milk");
        shoppingList.add("Eggs");
        shoppingList.add("Bread");

        for (String item : shoppingList) {
            if (item.equals("Eggs")) {
                shoppingList.add("Butter");  // Modifying during iteration
            }
            System.out.println(item);
        }
    }
}
```

### Output:

```
Exception in thread "main" java.util.ConcurrentModificationException
```

---

### With CopyOnWriteArrayList (Works)

```java
import java.util.List;
import java.util.concurrent.CopyOnWriteArrayList;

public class CopyOnWriteArrayListDemo {
    public static void main(String[] args) {
        List<String> shoppingList = new CopyOnWriteArrayList<>();
        shoppingList.add("Milk");
        shoppingList.add("Eggs");
        shoppingList.add("Bread");

        for (String item : shoppingList) {
            if (item.equals("Eggs")) {
                shoppingList.add("Butter");  // Safe modification
            }
            System.out.println(item);
        }

        System.out.println("Updated Shopping List: " + shoppingList);
    }
}
```

### Output:

```
Milk
Eggs
Bread
Updated Shopping List: [Milk, Eggs, Bread, Butter]
```

✅ No Exception.  
✅ "Butter" is added successfully after "Eggs".

---

# ✍ Example 2: Multi-Threaded Environment

### Without CopyOnWriteArrayList (Fails)

```java
import java.util.ArrayList;
import java.util.List;

public class MultiThreadListDemo {
    public static void main(String[] args) {
        List<Integer> list = new ArrayList<>();
        list.add(1);
        list.add(2);
        list.add(3);

        Thread reader = new Thread(() -> {
            for (Integer num : list) {
                System.out.println("Reader reads: " + num);
                try {
                    Thread.sleep(1000);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
        });

        Thread writer = new Thread(() -> {
            try {
                Thread.sleep(2000);
                list.add(4);  // Modify during reading
                System.out.println("Writer added 4");
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        });

        reader.start();
        writer.start();
    }
}
```

### Output:

```
Reader reads: 1
Reader reads: 2
Exception in thread "Thread-0" java.util.ConcurrentModificationException
```

---

### With CopyOnWriteArrayList (Works)

```java
import java.util.List;
import java.util.concurrent.CopyOnWriteArrayList;

public class MultiThreadCopyOnWriteDemo {
    public static void main(String[] args) {
        List<Integer> list = new CopyOnWriteArrayList<>();
        list.add(1);
        list.add(2);
        list.add(3);

        Thread reader = new Thread(() -> {
            for (Integer num : list) {
                System.out.println("Reader reads: " + num);
                try {
                    Thread.sleep(1000);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
        });

        Thread writer = new Thread(() -> {
            try {
                Thread.sleep(2000);
                list.add(4);  // Safe modification
                System.out.println("Writer added 4");
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        });

        reader.start();
        writer.start();
    }
}
```

### Output:

```
Reader reads: 1
Reader reads: 2
Writer added 4
Reader reads: 3
```

✅ No Exception.  
✅ Writer safely added 4 while reader was reading.

---

# ⚡ Key Internal Working

- When you start reading (iteration):
    
    - A **snapshot** (photo) of the list is given to you.
        
- If a thread **modifies** during the read:
    
    - A **new copy** of the list is created with modifications.
        
- **After the loop ends**:
    
    - The **reference** is updated to the new list.
        

✔ Readers **continue reading** old snapshot safely.  
✔ Writers **work** on new copy without disturbing readers.

---

# 🔥 Conclusion

- **CopyOnWriteArrayList** is **very useful** when:
    
    - You have many readers.
        
    - Few writers.
        
- **Downside**:
    
    - Every write operation makes a copy ➔ more **memory** and **CPU** usage.
        

