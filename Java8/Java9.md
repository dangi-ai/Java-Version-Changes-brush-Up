# Java 9 Notes

## Key Features
1. **Factory Methods for Immutable Collections** — `List.of()`, `Set.of()`, `Map.of()`
2. **Private Methods in Interfaces**
3. **Try-With-Resources Enhancement**
4. **JShell** — Interactive Java REPL for quick testing
5. **Stream API Improvements** — `takeWhile`, `dropWhile`, `iterate` enhancements
6. **Module System (Project Jigsaw)** — Organizing code into modules

---

## 1. Factory Methods for Immutable Collections

**Old Style (Before Java 9):**
```java
List<String> list = new ArrayList<>();
list.add("A");
list.add("B");
list = Collections.unmodifiableList(list);
```

**Java 9 Style:**
```java
List<String> list = List.of("A", "B");
Set<String> set = Set.of("X", "Y");
Map<Integer, String> map = Map.of(1, "One", 2, "Two");
```

---

## 2. Private Methods in Interfaces

**Java 9 allows** private methods inside interfaces for code reuse among default methods.

```java
interface MyInterface {
    default void method1() {
        log("method1");
    }
    default void method2() {
        log("method2");
    }
    private void log(String msg) {
        System.out.println("Logging: " + msg);
    }
}
```

---

## 3. Try-With-Resources Enhancement

**Old Style (Java 7 & 8):**
```java
BufferedReader br = new BufferedReader(new FileReader("file.txt"));
try (BufferedReader br1 = br) {
    System.out.println(br1.readLine());
}
```

**Java 9 Style:**
```java
BufferedReader br = new BufferedReader(new FileReader("file.txt"));
try (br) {
    System.out.println(br.readLine());
}
```
No need to re-declare the variable inside `try()`.

---

## 4. JShell

Run in terminal:
```
jshell
```
Example inside JShell:
```
jshell> int x = 5
x ==> 5

jshell> x + 10
$1 ==> 15
```

---

## 5. Stream API Improvements

### `takeWhile()`
```java
List<Integer> numbers = List.of(1, 2, 3, 4, 5, 1, 2);
List<Integer> result = numbers.stream()
                              .takeWhile(n -> n < 4)
                              .toList();
System.out.println(result); // [1, 2, 3]
```

### `dropWhile()`
```java
List<Integer> result = numbers.stream()
                              .dropWhile(n -> n < 4)
                              .toList();
System.out.println(result); // [4, 5, 1, 2]
```

### `iterate()` enhancement
```java
Stream.iterate(1, n -> n <= 5, n -> n + 1)
      .forEach(System.out::println);
```

---

## 6. Module System (Project Jigsaw)

**module-info.java**
```java
module com.example.myapp {
    requires java.base;
    exports com.example.myapp;
}
```

Used to group related code and control visibility between modules.
