
## 🚀 Java Executor Framework – Part 3 Notes

### 🔁 `Runnable` vs `Callable`

|Feature|`Runnable`|`Callable`|
|---|---|---|
|Return Value|Does **not** return a value|**Returns** a value|
|Exception Handling|Cannot throw checked exceptions|Can **throw checked exceptions**|
|Method Name|`run()`|`call()`|
|Used with `submit()`|Yes|Yes|

---

### 🧪 Example: `Runnable` returns `null`

```java
ExecutorService executor = Executors.newFixedThreadPool(2);

Runnable task = () -> System.out.println("Runnable running");
Future<?> future = executor.submit(task);

System.out.println("Future result: " + future.get()); // Output: null
executor.shutdown();
```

> ✅ **Output**

```
Runnable running
Future result: null
```

---

### 🧪 Example: `Callable` returns value

```java
Callable<Integer> task = () -> 1 + 2;

ExecutorService executor = Executors.newFixedThreadPool(2);
Future<Integer> future = executor.submit(task);

System.out.println("Callable result: " + future.get()); // Output: 3
executor.shutdown();
```

> ✅ **Output**

```
Callable result: 3
```

---

### 🧠 Why Use `Callable`?

- If you **want a return value**, use `Callable`.
    
- If you need to **throw checked exceptions**, `Callable` supports that in `call()`.
    

---

### 🔥 `Future.get()` Blocks

```java
Future<Integer> future = executor.submit(() -> {
    Thread.sleep(1000);
    return 42;
});
System.out.println("Result: " + future.get());
```

> `get()` blocks the main thread until result is ready.

---

### 🔄 `isShutdown()` vs `isTerminated()`

```java
ExecutorService executor = Executors.newFixedThreadPool(2);

executor.submit(() -> System.out.println("Running..."));
executor.shutdown();

System.out.println("Is shutdown: " + executor.isShutdown());
System.out.println("Is terminated: " + executor.isTerminated());

Thread.sleep(1000); // Wait for task to complete
System.out.println("Is terminated after wait: " + executor.isTerminated());
```

> ✅ **Output**

```
Running...
Is shutdown: true
Is terminated: false
Is terminated after wait: true
```

---

### 🧪 Bonus: `Thread.sleep()` in `Runnable` vs `Callable`

- `Runnable`: Must handle exceptions with try-catch
    

```java
Runnable task = () -> {
    try {
        Thread.sleep(1000);
    } catch (InterruptedException e) {
        e.printStackTrace();
    }
};
```

- `Callable`: Can throw exception directly
    

```java
Callable<Integer> task = () -> {
    Thread.sleep(1000); // Allowed
    return 5;
};
```

---

### 📚 `submit(Runnable task, T result)` Example

```java
ExecutorService executor = Executors.newFixedThreadPool(2);
Runnable task = () -> System.out.println("Task with result");

Future<String> future = executor.submit(task, "Hello");

System.out.println("Result: " + future.get()); // Output: Hello
executor.shutdown();
```

---

### 🧩 `invokeAll()` – Running Multiple Callables

#### ✅ Code Example:

```java
ExecutorService executor = Executors.newFixedThreadPool(2);

Callable<String> task1 = () -> "Task 1";
Callable<String> task2 = () -> "Task 2";
Callable<String> task3 = () -> "Task 3";

List<Callable<String>> taskList = Arrays.asList(task1, task2, task3);

List<Future<String>> futures = executor.invokeAll(taskList);

for (Future<String> f : futures) {
    System.out.println("Result: " + f.get());
}

executor.shutdown();
```

> ✅ **Output (order may vary depending on thread scheduling):**

```
Result: Task 1
Result: Task 2
Result: Task 3
```

---

### 🔍 `invokeAll()` Summary

- Takes a **collection of `Callable` tasks**.
    
- Waits until **all tasks are completed**.
    
- Returns a **list of `Future` objects**, one for each task.
    
