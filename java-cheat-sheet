# ☕ The Ultimate Java Interview Cheat Sheet

**For Campus Placements · SDE Internships · New Grad Roles**

> Built for fast, high-yield revision — tables and bullets over essays, so you can scan it the night before (or the hour before) an interview.

## Table of Contents

1. [Java Interview Roadmap](#1-java-interview-roadmap-by-frequency)
2. [Java Fundamentals](#2-java-fundamentals)
3. [Object-Oriented Programming](#3-object-oriented-programming-)
4. [Java Memory Management](#4-java-memory-management)
5. [Exception Handling](#5-exception-handling)
6. [Collections Framework](#6-collections-framework-)
7. [Multithreading](#7-multithreading)
8. [Java 8+ Features](#8-java-8-features-)
9. [File Handling & Serialization](#9-file-handling--serialization)
10. [Important Keywords](#10-important-keywords-quick-table)
11. [Master Comparison Table Index](#11-master-comparison-table-index)
12. [Time Complexity Cheat Table](#12-time-complexity-cheat-table)
13. [Top Interview Questions](#13-top-interview-questions-high-yield-set)
14. [Coding Patterns & Templates](#1415-coding-patterns--templates-quick-reference)
15. [Company-Specific Focus](#16-company-specific-focus)
16. [Common Interview Traps](#17-common-interview-traps-top-20)
17. [One-Page Last-Minute Revision](#18-one-page-last-minute-revision)

---

## 1. Java Interview Roadmap (by Frequency)

| Priority | Topics |
|---|---|
| ⭐⭐⭐⭐⭐ Must Know | OOP (all 4 pillars), Collections (ArrayList/HashMap internals), Exception Handling, `==` vs `equals()`, `String` immutability, Multithreading basics, JVM memory areas, Static/Final |
| ⭐⭐⭐⭐ Frequently Asked | Java 8 (Streams, Lambdas, Optional), Overloading vs Overriding, Abstract vs Interface, Garbage Collection, `hashCode()` contract, Generics, `Comparable` vs `Comparator` |
| ⭐⭐⭐ Good to Know | Executor Framework, `volatile`, Serialization, Design Patterns (Singleton, Factory), Immutable classes, Inner classes |
| ⭐⭐ Rarely Asked | `strictfp`, `native`, custom classloaders, JMM internals in depth, RMI |

---

## 2. Java Fundamentals

### JDK vs JRE vs JVM
- **JVM**: Runs bytecode, platform-dependent implementation, platform-independent spec. Gives Java "write once, run anywhere."
- **JRE**: JVM + libraries needed to *run* Java apps (no compiler).
- **JDK**: JRE + development tools (`javac`, debugger, etc.) needed to *build* Java apps.
- **30-sec answer**: "JDK is for developers (write+run), JRE is for end users (run only), JVM is the engine that actually executes bytecode."

### Execution Flow
```text
.java file → javac (compiler) → .class file (bytecode)
→ ClassLoader loads bytecode → Bytecode Verifier checks it
→ JIT/Interpreter → Machine code → Execution on OS
```

### Compilation vs Interpretation
Java is **both**: source → bytecode (compiled), then bytecode → machine code (interpreted line-by-line by JVM, with **JIT** compiling hot code paths to native code for speed). This hybrid model is why Java is "compiled and interpreted."

### Key Features Interviewers Probe
Platform independence (via bytecode), Object-oriented, Automatic memory management (GC), Multithreaded, Robust (exception handling + strong typing), Secure (no explicit pointers, sandboxing).

### Strings — High-Yield
- Strings are **immutable** — once created, the character sequence can't change. Any "modification" creates a new object.
- **Why immutable?** Security (used in classloading, network connections), thread-safety (shared without sync), caching of hashcode, and **String Pool** works only if strings are immutable.
- **String Pool**: `String s = "abc"` → checks pool first, reuses if exists. `new String("abc")` → forces a new heap object outside the pool.
```java
String a = "hello";
String b = "hello";
String c = new String("hello");

System.out.println(a == b);       // true  (same pool reference)
System.out.println(a == c);       // false (different heap object)
System.out.println(a.equals(c));  // true  (same content)
```
- **StringBuilder** (not thread-safe, fast) vs **StringBuffer** (thread-safe via synchronized methods, slower). Use `StringBuilder` unless multiple threads mutate the same object.

### Wrapper Classes, Autoboxing/Unboxing
- Wrapper classes (`Integer`, `Double`, etc.) let primitives be used where Objects are required (e.g., in Collections).
- **Autoboxing**: primitive → wrapper automatically (`Integer i = 5;`).
- **Unboxing**: wrapper → primitive automatically (`int x = i;`).
- **Classic trap — Integer caching**:
```java
Integer a = 127, b = 127;
System.out.println(a == b); // true  — cached (-128 to 127)

Integer c = 200, d = 200;
System.out.println(c == d); // false — outside cache range, new objects
```
> **Interview tip**: Always mention the `-128 to 127` Integer cache pool — this is a very common trick question.

---

## 3. Object-Oriented Programming ⭐⭐⭐⭐⭐

| Pillar | Definition | Real-world Analogy | Java Mechanism |
|---|---|---|---|
| **Encapsulation** | Bundling data + methods, hiding internal state | Capsule/medicine — hides ingredients, exposes effect | private fields + public getters/setters |
| **Abstraction** | Hiding implementation, showing only functionality | Car steering wheel — you don't see the mechanics | `abstract` class, `interface` |
| **Inheritance** | Acquiring properties of another class | Child inherits traits from parent | `extends`, `implements` |
| **Polymorphism** | One interface, many implementations | A person acts differently as employee/parent/friend | Overloading (compile-time) & Overriding (runtime) |

### Overloading vs Overriding
| Aspect | Overloading | Overriding |
|---|---|---|
| Binding | Compile-time (static) | Runtime (dynamic) |
| Class | Same class | Parent-child (inheritance) |
| Signature | Must differ (params) | Must be same |
| Return type | Can differ | Same or covariant |
| Private/static/final methods | Can be overloaded | **Cannot** be overridden |

```java
class Animal {
    void sound() { System.out.println("Some sound"); }
}
class Dog extends Animal {
    @Override
    void sound() { System.out.println("Bark"); } // runtime polymorphism
}
Animal a = new Dog();
a.sound(); // "Bark" — decided at runtime based on actual object
```

### Constructors, `this`, `super`
- Constructor: special method, same name as class, no return type, called on `new`.
- `this`: refers to current object — resolves field/parameter naming conflicts, chains constructors (`this(...)`).
- `super`: refers to parent class — calls parent constructor (`super(...)`, must be first line) or parent method (`super.method()`).

### static vs final vs Access Modifiers
- **static**: belongs to class, not instance — shared across all objects, loaded once at class loading.
- **final**: variable → constant; method → can't be overridden; class → can't be extended (e.g., `String`, `Integer`).
- **Access modifiers**: `private` (class only) < *default/package-private* (package only) < `protected` (package + subclasses) < `public` (everywhere).

### Abstract Class vs Interface
| Aspect | Abstract Class | Interface |
|---|---|---|
| Methods | Abstract + concrete | Abstract, default, static (Java 8+) |
| Fields | Any type | `public static final` only |
| Multiple inheritance | No (single class) | Yes (implement many) |
| Constructor | Yes | No |
| When to use | "IS-A" with shared code | Contract/capability (e.g., `Comparable`) |

> **Interview tip**: "Use abstract class when classes share common code/state; use interface when unrelated classes need to guarantee the same behavior."

---

## 4. Java Memory Management

```text
                JVM MEMORY LAYOUT
 ┌──────────────────────────────────────────┐
 │                  HEAP                     │  ← Objects, instance vars
 │   ┌─────────┐  ┌─────────┐  ┌─────────┐   │     (Shared across threads)
 │   │  Young   │  │  Young   │ │   Old    │  │
 │   │  (Eden,  │  │(Survivor)│ │ (Tenured)│  │
 │   │  S0,S1)  │  │          │ │          │  │
 │   └─────────┘  └─────────┘  └─────────┘   │
 └──────────────────────────────────────────┘
 ┌──────────────┐  ┌───────────────────────┐
 │  STACK        │  │  METASPACE (Java 8+)  │  ← class metadata
 │  (per thread) │  │  replaced PermGen      │
 │  local vars,  │  └───────────────────────┘
 │  method calls │
 └──────────────┘
 ┌──────────────────────┐
 │  STRING POOL          │  ← Inside Heap (Java 7+)
 └──────────────────────┘
```

| Area | Stores | Scope |
|---|---|---|
| Heap | Objects, instance variables | Shared, GC-managed |
| Stack | Local vars, method frames, references | Per-thread |
| Method Area/Metaspace | Class metadata, static vars, bytecode | Shared |
| String Pool | Interned string literals | Inside Heap |

### Garbage Collection
- Automatically reclaims memory of unreachable objects. Generational: **Young Gen** (Eden + 2 Survivor spaces, minor GC, frequent) → promoted to **Old Gen** (major/full GC, less frequent).
- Common collectors: Serial, Parallel, **G1** (default modern), ZGC (low latency).
- `System.gc()` is only a *request*, not a guarantee.

### Common Errors
- **StackOverflowError**: stack exhausted — typically infinite/too-deep recursion.
- **OutOfMemoryError**: heap exhausted — memory leak (objects unintentionally still referenced) or genuinely too much data.
- **Memory Leak in Java**: happens via static collections holding references, unclosed resources, listeners not deregistered.

### Reference Types (for GC)
Strong (default, never GC'd while reachable) → Soft (GC'd only if memory needed) → Weak (GC'd on next GC cycle) → Phantom (post-finalization cleanup, `PhantomReference`).

---

## 5. Exception Handling

```text
                 Throwable
              /            \
          Error            Exception
      (OutOfMemory,     /              \
       StackOverflow)  IOException    RuntimeException
      -- unchecked --  (checked)     (NullPointer,
                                       ArrayIndexOOB,
                                       ArithmeticException)
                                      -- unchecked --
```

| Type | Checked by compiler? | Examples | Must handle? |
|---|---|---|---|
| **Checked** | Yes | `IOException`, `SQLException` | Yes — try/catch or `throws` |
| **Unchecked (RuntimeException)** | No | `NullPointerException`, `ArithmeticException` | Optional |
| **Error** | No | `OutOfMemoryError`, `StackOverflowError` | Not recoverable, don't catch |

```java
try {
    int x = 5 / 0;
} catch (ArithmeticException e) {
    System.out.println("Caught: " + e.getMessage());
} finally {
    System.out.println("Always runs (even with return in try)");
}
```
- `throw` → actually throws one exception instance. `throws` → declares a method *might* throw (in signature).
- **Custom Exception**: extend `Exception` (checked) or `RuntimeException` (unchecked).
- **Best practices**: catch specific exceptions (not generic `Exception`), never swallow silently, close resources with try-with-resources, don't use exceptions for normal control flow.
```java
try (BufferedReader br = new BufferedReader(new FileReader("f.txt"))) {
    // auto-closed even on exception
}
```

---

## 6. Collections Framework ⭐⭐⭐⭐⭐

### Hierarchy (mental map)
```text
Collection ─┬─ List (ordered, duplicates) ── ArrayList, LinkedList, Vector, Stack
            ├─ Set  (unique)  ── HashSet, LinkedHashSet, TreeSet
            └─ Queue (FIFO)   ── PriorityQueue, ArrayDeque, LinkedList

Map (key-value, NOT a Collection) ── HashMap, LinkedHashMap, TreeMap, Hashtable
```

### List Comparison
| | ArrayList | LinkedList | Vector |
|---|---|---|---|
| Structure | Dynamic array | Doubly linked list | Dynamic array |
| Access `get(i)` | O(1) | O(n) | O(1) |
| Insert/Delete (middle) | O(n) | O(1)* (once positioned) | O(n) |
| Thread-safe | No | No | Yes (synchronized, legacy) |
| Use case | Frequent reads | Frequent insert/delete | Legacy thread-safe needs |

### HashMap — Deep Dive (very frequently asked)
- Stores key-value pairs using an **array of buckets**; bucket index = `hash(key) & (capacity - 1)`.
- On collision (same bucket): stores as a **linked list**; converts to a **Red-Black Tree** if a bucket has ≥8 entries and table capacity ≥64 (Java 8+ optimization, O(n)→O(log n) worst case).
- Default capacity 16, load factor 0.75 → resizes (doubles) when `size > capacity * loadFactor`.
- `null` key allowed (only one), `null` values allowed.
- **Not thread-safe** — use `ConcurrentHashMap` for concurrent access.
```java
Map<String, Integer> map = new HashMap<>();
map.put("a", 1);
map.put("b", 2);
for (Map.Entry<String, Integer> e : map.entrySet()) {
    System.out.println(e.getKey() + "=" + e.getValue());
}
```

### Map Comparison
| | HashMap | LinkedHashMap | TreeMap | Hashtable |
|---|---|---|---|---|
| Order | No guarantee | Insertion order | Sorted (natural/comparator) | No guarantee |
| Null key | 1 allowed | 1 allowed | Not allowed (throws NPE) | Not allowed |
| Thread-safe | No | No | No | Yes (synchronized) |
| Time complexity | O(1) avg | O(1) avg | O(log n) | O(1) avg |
| Backing structure | Array + LL/Tree | HashMap + LL | Red-Black Tree | Array + LL |

### Set Comparison
| | HashSet | LinkedHashSet | TreeSet |
|---|---|---|---|
| Backing | HashMap | LinkedHashMap | TreeMap |
| Order | None | Insertion order | Sorted |
| Duplicates | No | No | No |
| Null | 1 allowed | 1 allowed | Not allowed |

### `equals()` and `hashCode()` Contract (⭐⭐⭐⭐⭐ trap topic)
- If `a.equals(b)` is true, `a.hashCode() == b.hashCode()` **must** be true.
- Reverse is NOT required (different objects can share a hashcode — collision).
- **Rule**: always override both together, or neither. Overriding only `equals()` breaks HashMap/HashSet behavior — objects that are "equal" may land in different buckets and duplicates sneak into a Set.

### Comparable vs Comparator
| | Comparable | Comparator |
|---|---|---|
| Method | `compareTo(T o)` | `compare(T o1, T o2)` |
| Location | Inside the class itself | Separate class/lambda |
| Sorts | Natural/default ordering | Custom ordering, multiple ways |
| Use | `Collections.sort(list)` | `Collections.sort(list, comparator)` |

```java
// Comparable — natural order
class Emp implements Comparable<Emp> {
    int salary;
    public int compareTo(Emp o) { return this.salary - o.salary; }
}

// Comparator — custom order (Java 8 style)
list.sort(Comparator.comparing(Emp::getSalary).reversed());
```

### Iterator vs Iterable
`Iterable` — top interface with `iterator()` method, enables for-each loop. `Iterator` — object returned that has `hasNext()`, `next()`, `remove()`. Use `Iterator.remove()` to safely remove while iterating (avoids `ConcurrentModificationException`).

---

## 7. Multithreading

### Thread Lifecycle
```
NEW → RUNNABLE → RUNNING → (BLOCKED/WAITING/TIMED_WAITING) → TERMINATED
```
- Create via `extends Thread` (single inheritance used up) or `implements Runnable` (preferred — allows extending other classes).
```java
class MyRunnable implements Runnable {
    public void run() { System.out.println("Running"); }
}
new Thread(new MyRunnable()).start(); // start(), NOT run() directly!
```
> **Trap**: calling `run()` directly executes on the *current* thread — no new thread is created. Always call `start()`.

### Key Concepts
| Concept | What it does |
|---|---|
| `synchronized` | Only one thread can execute the block/method on that object at a time — prevents race conditions |
| `volatile` | Guarantees visibility of updates across threads (no caching in thread-local memory), does NOT guarantee atomicity |
| Deadlock | Two+ threads waiting on each other's locks forever |
| Race Condition | Multiple threads modify shared data concurrently → unpredictable result |
| `Executor` framework | Manages thread pools instead of manually creating threads (`ExecutorService`) |
| `Callable` | Like `Runnable` but returns a value and can throw checked exceptions |
| `Future` | Represents result of an async computation (`get()` blocks till done) |

```java
ExecutorService pool = Executors.newFixedThreadPool(4);
Future<Integer> result = pool.submit(() -> 5 + 5);
System.out.println(result.get()); // 10
pool.shutdown();
```

---

## 8. Java 8+ Features ⭐⭐⭐⭐

### Lambda & Functional Interfaces
- Functional interface = exactly one abstract method (`@FunctionalInterface`). Lambda gives it a body inline.
```java
Runnable r = () -> System.out.println("Hi");
Comparator<Integer> c = (a, b) -> a - b;
```

### Streams API
- Sequence of elements supporting functional operations: `filter`, `map`, `reduce`, `collect` — pipeline is lazy until a terminal op runs.
```java
List<Integer> nums = List.of(1,2,3,4,5,6);
List<Integer> evenSquares = nums.stream()
    .filter(n -> n % 2 == 0)
    .map(n -> n * n)
    .collect(Collectors.toList()); // [4, 16, 36]

int sum = nums.stream().mapToInt(Integer::intValue).sum();
```
- `Collectors.toList()`, `toMap()`, `groupingBy()`, `joining()` are the most-asked.

### Optional
Avoids `NullPointerException` by wrapping a possibly-null value explicitly.
```java
Optional<String> opt = Optional.ofNullable(getName());
String name = opt.orElse("Default");
```

### Method References
`ClassName::methodName` — shorthand for a lambda that just calls one method: `list.forEach(System.out::println)`.

### Default & Static Methods in Interfaces
Java 8 allowed interfaces to have method bodies (`default`) — enables adding methods to interfaces without breaking existing implementers.

---

## 9. File Handling & Serialization
- `File` — represents path (not content). `FileReader`/`FileWriter` — char streams. `BufferedReader`/`BufferedWriter` — wrap them for efficient buffered I/O.
- **Serialization**: converting an object to a byte stream (implement `Serializable`) — e.g., to save to disk or send over network.
- **`transient`** keyword: excludes a field from serialization (e.g., passwords, derived data).
- **`serialVersionUID`**: version control for serialized classes — interviewers ask why it matters (mismatch → `InvalidClassException` on deserialization).

---

## 10. Important Keywords Quick Table

| Keyword | Meaning |
|---|---|
| `static` | Belongs to class, not instance |
| `final` | Constant / non-overridable / non-extendable |
| `finally` | Block that always executes after try/catch |
| `finalize()` | Called by GC before object destruction (deprecated, unreliable — avoid relying on it) |
| `transient` | Field skipped during serialization |
| `volatile` | Ensures visibility of variable across threads |
| `native` | Method implemented in another language (e.g., C via JNI) |
| `strictfp` | Forces consistent floating-point results across platforms |
| `abstract` | Class/method without full implementation |
| `synchronized` | Restricts access to one thread at a time |
| `default` | Interface method with a body (Java 8+) |

---

## 11. Master Comparison Table Index
*(All comparisons above are cross-referenced here for a 30-second scan)*

| Comparison | Where to find it |
|---|---|
| JDK vs JRE vs JVM | Section 2 |
| Array vs ArrayList | Array = fixed size, primitives OK; ArrayList = dynamic, objects only |
| ArrayList vs LinkedList | Section 6 |
| HashMap vs Hashtable / TreeMap | Section 6 |
| HashSet vs TreeSet | Section 6 |
| String vs StringBuilder vs StringBuffer | Section 2 |
| Overloading vs Overriding | Section 3 |
| Abstract Class vs Interface | Section 3 |
| Checked vs Unchecked Exception | Section 5 |
| Heap vs Stack | Section 4 |
| `==` vs `equals()` | Section 2 (Strings) & below |
| `equals()` vs `hashCode()` | Section 6 |
| Comparable vs Comparator | Section 6 |
| Thread vs Runnable | Section 7 |
| `throw` vs `throws` | Section 5 |

**`==` vs `equals()`**: `==` compares references (memory address) for objects, or values for primitives. `.equals()` compares logical/content equality (as defined by the class) — default `Object.equals()` is reference equality unless overridden (like `String` does).

**Composition vs Inheritance**: Inheritance = "IS-A" (tight coupling, compile-time). Composition = "HAS-A" (loose coupling, flexible at runtime) — **"favor composition over inheritance"** is a classic design-principle answer.

**Process vs Thread**: Process = independent execution unit with its own memory space. Thread = lightweight sub-unit within a process, shares memory with sibling threads.

---

## 12. Time Complexity Cheat Table

| Structure | Access | Search | Insert | Delete |
|---|---|---|---|---|
| ArrayList | O(1) | O(n) | O(n) worst / O(1) amortized end | O(n) |
| LinkedList | O(n) | O(n) | O(1)* | O(1)* |
| HashMap/HashSet | — | O(1) avg, O(n) worst | O(1) avg | O(1) avg |
| TreeMap/TreeSet | — | O(log n) | O(log n) | O(log n) |
| PriorityQueue | — | O(n) | O(log n) | O(log n) |
| Stack (array) | O(1) top | O(n) | O(1) push | O(1) pop |

**Sorting algorithms** (know these cold for MCQs):
| Algorithm | Best | Average | Worst | Space | Stable? |
|---|---|---|---|---|---|
| Bubble/Insertion Sort | O(n) | O(n²) | O(n²) | O(1) | Yes |
| Merge Sort | O(n log n) | O(n log n) | O(n log n) | O(n) | Yes |
| Quick Sort | O(n log n) | O(n log n) | O(n²) | O(log n) | No |
| Heap Sort | O(n log n) | O(n log n) | O(n log n) | O(1) | No |
| `Collections.sort()` (Java) | uses **TimSort** (hybrid merge+insertion), O(n log n) | | | | Yes |

---

## 13. Top Interview Questions (High-Yield Set)

### Beginner-level (rapid fire — know the one-liner)
1. **Why is Java platform-independent?** → Bytecode runs on any JVM.
2. **Why no multiple inheritance with classes?** → Avoids the Diamond Problem; interfaces solve it safely via default methods (Java resolves ambiguity by forcing explicit override).
3. **Can we override `static` methods?** → No, static methods are hidden, not overridden (no runtime polymorphism for them).
4. **Can constructors be inherited?** → No, but can be invoked via `super()`.
5. **Difference between `length`, `length()`, `size()`?** → Array property, String method, Collection method respectively.
6. **Is Java "pass by value" or "pass by reference"?** → Always **pass by value** — for objects, the *value of the reference* is passed (so you can mutate the object, but reassigning the parameter doesn't affect the caller's reference).
7. **What is the diamond problem and how does Java 8 handle it in interfaces?** → If two interfaces have the same default method, implementing class MUST override it explicitly.
8. **Why is `main` static?** → So JVM can call it without creating an object of the class first.

### Intermediate-level
9. **How does HashMap handle collisions?** → Section 6 (linked list → tree conversion at 8 entries).
10. **What happens if you don't override `hashCode()`?** → Default is based on memory address — logically equal objects may go to different buckets, breaking Set/Map uniqueness.
11. **Why are Strings immutable in Java?** → Security, String pool reuse, thread-safety, safe hashcode caching.
12. **Difference between `ClassNotFoundException` and `NoClassDefFoundError`?** → Former: class not found by classloader at runtime lookup (checked exception). Latter: class WAS available at compile time but missing at runtime (an Error).
13. **What is a memory leak in Java despite having GC?** → Objects still reachable via references (e.g., static collections, unclosed listeners) that are never removed — GC can't collect *reachable* objects.
14. **Explain `ConcurrentModificationException`.** → Thrown when a collection is structurally modified while iterating with a normal iterator; use `Iterator.remove()` or `ConcurrentHashMap`/`CopyOnWriteArrayList` instead.

### Advanced-level
15. **How does `ConcurrentHashMap` achieve thread safety without locking the whole map?** → Segments/bucket-level locking (Java 8+ uses CAS + synchronized on bins), allowing concurrent reads and higher write throughput than `Hashtable`.
16. **Explain the Java Memory Model (JMM) and happens-before.** → Defines how threads interact through memory; `volatile`, `synchronized`, and thread `start()`/`join()` establish happens-before relationships guaranteeing visibility/ordering.
17. **How would you design a thread-safe Singleton?** → Double-checked locking with `volatile`, or the **Bill Pugh / static inner class** approach (lazy + thread-safe without synchronization overhead), or an `enum` singleton.
```java
class Singleton {
    private Singleton() {}
    private static class Holder {
        static final Singleton INSTANCE = new Singleton();
    }
    public static Singleton getInstance() { return Holder.INSTANCE; }
}
```

---

## 14–15. Coding Patterns & Templates (Quick Reference)

**Two Pointer**
```java
int l = 0, r = arr.length - 1;
while (l < r) { /* logic */ l++; r--; }
```

**Sliding Window**
```java
int windowSum = 0, start = 0;
for (int end = 0; end < arr.length; end++) {
    windowSum += arr[end];
    if (end - start + 1 > k) { windowSum -= arr[start]; start++; }
}
```

**Binary Search**
```java
int lo = 0, hi = arr.length - 1;
while (lo <= hi) {
    int mid = lo + (hi - lo) / 2;
    if (arr[mid] == target) return mid;
    else if (arr[mid] < target) lo = mid + 1;
    else hi = mid - 1;
}
```

**BFS (graph/tree)**
```java
Queue<Node> q = new LinkedList<>();
q.add(root);
while (!q.isEmpty()) {
    Node cur = q.poll();
    for (Node nb : cur.neighbors) q.add(nb);
}
```

**DFS (recursive)**
```java
void dfs(Node node, Set<Node> visited) {
    if (node == null || visited.contains(node)) return;
    visited.add(node);
    for (Node nb : node.neighbors) dfs(nb, visited);
}
```

**HashMap Frequency Count**
```java
Map<Character, Integer> freq = new HashMap<>();
for (char c : s.toCharArray()) freq.merge(c, 1, Integer::sum);
```

**Fast Input (competitive)**
```java
BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
int n = Integer.parseInt(br.readLine().trim());
```

---

## 16. Company-Specific Focus

| Company | What they emphasize |
|---|---|
| **UBS / JPMorgan / Goldman Sachs** (finance) | Strong CS fundamentals MCQs (OOP, DBMS, OS, CN, DSA), Collections internals, Multithreading, low-level design, SQL, some aptitude+reasoning rounds |
| **TCS / Infosys / Accenture / Capgemini / Cognizant** | Core Java basics, OOP, simple coding, aptitude-heavy overall test |
| **IBM / Oracle** | Java fundamentals + DB (since Oracle owns Java + DB products) |
| **Amazon / Microsoft / Google / Adobe** (product-based) | DSA-heavy, LLD/HLD, less rote Java trivia, more problem-solving depth |

> Since you're prepping for **UBS**, prioritize: OOP theory, Collections internals (HashMap especially), Exception hierarchy, Multithreading basics, plus your CN/OS/DBMS/DSA MCQ fundamentals and aptitude/reasoning speed.

---

## 17. Common Interview Traps (Top 20)

1. Saying Java is "pass by reference" — it's pass by value (of the reference).
2. Confusing `String` immutability with `final` — a `final String` reference can't be reassigned, but immutability is a property of the object itself.
3. Forgetting `equals()`+`hashCode()` must be overridden together.
4. Thinking `finally` doesn't run if there's a `return` in `try` — it does (unless `System.exit()` is called).
5. Calling `run()` instead of `start()` on a Thread.
6. Assuming `HashMap` maintains insertion order (it doesn't — use `LinkedHashMap`).
7. Not knowing `TreeMap`/`TreeSet` disallow `null` (throws NPE on `null` comparison).
8. Confusing `Comparable` (internal, one way to sort) with `Comparator` (external, many ways).
9. Thinking `static` methods can be overridden — they're hidden, not overridden.
10. Forgetting `private`/`static`/`final` methods can't be overridden.
11. Mixing up checked vs unchecked exceptions when writing `throws`.
12. Assuming `ArrayList` is thread-safe (it's not — `Vector`/`Collections.synchronizedList` are).
13. Not knowing why multiple inheritance is disallowed for classes but allowed for interfaces.
14. Confusing abstraction (hiding complexity) with encapsulation (hiding data).
15. Believing `System.gc()` guarantees garbage collection — it's only a hint.
16. Forgetting Integer caching (`-128 to 127`) causes `==` surprises.
17. Not knowing `String` concatenation with `+` in a loop is inefficient — use `StringBuilder`.
18. Confusing `throw` (statement, throws one exception) with `throws` (declaration in signature).
19. Thinking interfaces can have instance fields — they can only have `public static final` constants.
20. Not being able to explain **why** `HashMap` isn't thread-safe but not mentioning `ConcurrentHashMap` as the fix.

---

## 18. One-Page Last-Minute Revision

**OOP**: Encapsulation (hide data) • Abstraction (hide implementation) • Inheritance (`extends`/`implements`, IS-A) • Polymorphism (Overloading=compile-time, Overriding=runtime)

**Memory**: Heap (objects, shared) • Stack (locals, per-thread) • Metaspace (class metadata) • GC is generational (Young→Old)

**Exceptions**: `Throwable` → `Error` (fatal) / `Exception` → Checked (compile-time enforced) / Unchecked (`RuntimeException`, optional)

**Collections quick-pick**:
- Need order + duplicates + fast random access → `ArrayList`
- Need fast insert/delete in middle → `LinkedList`
- Need key-value, fast lookup → `HashMap`
- Need key-value, sorted → `TreeMap`
- Need unique elements, fast → `HashSet`
- Need unique elements, sorted → `TreeSet`

**Java 8**: Lambda (anonymous function) • Stream (`filter`→`map`→`collect`) • Optional (avoid NPE) • Method refs (`Class::method`)

**Keywords**: `static`=class-level • `final`=immutable/no-override/no-extend • `volatile`=visibility across threads • `synchronized`=mutual exclusion • `transient`=skip serialization

**`== ` vs `.equals()`**: reference vs content equality — always override both `equals()` & `hashCode()` together.

**Threading**: `start()` not `run()` • `Runnable` preferred over `extends Thread` • Use `ExecutorService` over manual thread creation • `volatile` ≠ atomic

**Time Complexity memory hook**: *"Hash = O(1) average, Tree = O(log n), Array-shift = O(n)"*

---

*Good luck with the UBS assessment — focus your remaining time on Sections 6 (Collections/HashMap), 3 (OOP), 5 (Exceptions), and 7 (Multithreading), since those are the highest-yield for finance-sector campus placements.*
