
### 🧠 **Deadlock in Java - Notes**


#### ✅ **Definition**

Deadlock is a situation in multithreading where two or more threads are blocked forever, each waiting for the other to release a lock.

#### 💡 **Real-World Example Analogy**

- **Thread A** has a **pen**, needs **paper** to write.
    
- **Thread B** has **paper**, needs **pen** to write.
    
- Both are waiting for each other — results in **deadlock**.
    

---

### ⚠️ **Four Conditions for Deadlock**

1. **Mutual Exclusion** – Only one thread can hold a lock at a time.
    
2. **Hold and Wait** – Thread holding one lock is waiting for another.
    
3. **No Preemption** – Lock cannot be forcibly taken from a thread.
    
4. **Circular Wait** – Threads form a cycle, each waiting for the next.
    

---

### 🧪 **Code Demonstration of Deadlock**

```java
class Pen {
    synchronized void writeWithPenAndPaper(Paper paper) {
        System.out.println("Thread 1: Holding pen and waiting for paper...");
        try { Thread.sleep(1000); } catch (InterruptedException e) {}
        paper.finishWriting();
    }

    synchronized void finishWriting() {
        System.out.println("Thread 1: Finished writing with pen.");
    }
}

class Paper {
    synchronized void writeWithPaperAndPen(Pen pen) {
        System.out.println("Thread 2: Holding paper and waiting for pen...");
        try { Thread.sleep(1000); } catch (InterruptedException e) {}
        pen.finishWriting();
    }

    synchronized void finishWriting() {
        System.out.println("Thread 2: Finished writing with paper.");
    }
}

public class DeadlockExample {
    public static void main(String[] args) {
        Pen pen = new Pen();
        Paper paper = new Paper();

        Thread t1 = new Thread(() -> pen.writeWithPenAndPaper(paper));
        Thread t2 = new Thread(() -> paper.writeWithPaperAndPen(pen));

        t1.start();
        t2.start();
    }
}
```

#### 🛑 Output (Deadlock)

```
Thread 1: Holding pen and waiting for paper...
Thread 2: Holding paper and waiting for pen...
// Now both are stuck forever
```

---

### ✅ **Solution – Avoiding Deadlock with Consistent Lock Ordering**

```java
class Pen {
    void write(Paper paper) {
        synchronized (this) {
            System.out.println("Thread 1: Locked pen");
            try { Thread.sleep(50); } catch (InterruptedException e) {}
            synchronized (paper) {
                System.out.println("Thread 1: Locked paper");
                System.out.println("Thread 1: Writing...");
            }
        }
    }
}

class Paper {
    void write(Pen pen) {
        synchronized (pen) {
            System.out.println("Thread 2: Locked pen");
            try { Thread.sleep(50); } catch (InterruptedException e) {}
            synchronized (this) {
                System.out.println("Thread 2: Locked paper");
                System.out.println("Thread 2: Writing...");
            }
        }
    }
}

public class DeadlockResolved {
    public static void main(String[] args) {
        Pen pen = new Pen();
        Paper paper = new Paper();

        Thread t1 = new Thread(() -> pen.write(paper));
        Thread t2 = new Thread(() -> paper.write(pen));

        t1.start();
        t2.start();
    }
}
```

#### ✅ Output (Resolved)

```
Thread 1: Locked pen
Thread 1: Locked paper
Thread 1: Writing...
Thread 2: Locked pen
Thread 2: Locked paper
Thread 2: Writing...
```

---

### 📝 **Key Takeaway**

Always **acquire locks in a consistent order** to avoid deadlocks. If multiple threads need multiple locks, make sure they all acquire them in the **same sequence**.