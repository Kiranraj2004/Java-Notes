
---

### 🧠 **1. CPU (Central Processing Unit)**

- The **brain of the computer** – where all computations take place.
    
- Whatever code or logic we write (like `if-else`, arithmetic) runs **inside the CPU**.
    

---

### 🧩 **2. Core**

- A **core** is an **individual processing unit** inside a CPU.
    
- Earlier CPUs had a **single core**, now we have **multi-core** CPUs (like dual-core, quad-core, octa-core).
    
- More cores → more tasks can be handled **simultaneously**.
    
    - Example: One core plays music, one edits a document, another runs background tasks, etc.
        

---

### 📜 **3. Program**

- A **set of instructions** to perform a task.
    
- Examples: Microsoft Word, OBS Studio, Chrome – all are **programs**.
    

---

### 🧩 **4. Process**

- When a **program runs**, it becomes a **process**.
    
- The **Operating System (OS)** starts a new process for each running program.
    
    - Example: Opening Word starts the Word process.
        

---

### 🧵 **5. Thread**

- A **smaller unit** inside a process.
    
- A process can have **multiple threads** that share resources but can run **independently**.
    
    - Example: In MS Word:
        
        - One thread handles typing
            
        - Another does spell check
            
        - Another saves automatically
            

---

### 🔁 **6. Multitasking**

- The **OS runs multiple processes at the same time**.
    
- On **single-core CPUs**, this is done via **rapid switching** (time-sharing).
    
- On **multi-core CPUs**, **true parallel execution** is possible.
    
- The **scheduler** in the OS decides which core runs which task.
    

---

### 🧵+🧵 = 🚀 **7. Multithreading**

- If **multitasking = multiple processes running**,  
    then **multithreading = multiple threads inside a single process running**.
    
- Makes a program **faster and more responsive**.
    
    - Example: A browser uses multithreading:
        
        - One thread renders the page
            
        - Another runs JavaScript
            
        - Another handles user inputs
            

---

### ⚙️ **How Multithreading Boosts Efficiency**

- Breaks tasks into **smaller threads**
    
- Threads can be executed **in parallel**, especially on multi-core CPUs
    
- Leads to **better CPU usage** and **smoother multitasking**
    

