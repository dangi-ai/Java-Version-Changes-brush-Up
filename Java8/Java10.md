# Java 10 Notes

## Key Features
1. **Local Variable Type Inference (`var`)**
2. **Unmodifiable Collections Copy**
3. **Optional.orElseThrow() without arguments**
4. **Performance & Memory Improvements (Garbage Collector, Container Awareness)**

---

## 1. Local Variable Type Inference (`var`)

Java 10 introduced the `var` keyword for local variables with an initializer.

**Old Style (Before Java 10):**
```java
String message = "Hello";
List<String> list = new ArrayList<>();
```

**Java 10 Style:**
```java
var message = "Hello"; // Infers String
var list = new ArrayList<String>(); // Infers ArrayList<String>
```
💡 Still strongly typed — `var` is not dynamic typing.

---

## 2. Unmodifiable Collections Copy

**Old Style:**
```java
List<String> copy = Collections.unmodifiableList(originalList);
```

**Java 10 Style:**
```java
List<String> copy = List.copyOf(originalList);
```
If `originalList` is already unmodifiable, no new copy is created.

---

## 3. Optional.orElseThrow() without arguments

**Old Style (Java 8 & 9):**
```java
Optional<String> name = Optional.of("John");
String value = name.orElseThrow(() -> new IllegalArgumentException("Not found"));
```

**Java 10 Style:**
```java
Optional<String> name = Optional.of("John");
String value = name.orElseThrow(); // Throws NoSuchElementException if empty
```

---

## 4. Performance & Memory Improvements

- **Garbage Collector** improvements.
- **Container Awareness** — Java 10 detects CPU & memory limits when running in containers like Docker.

---

## Example Combining Features

```java
import java.util.*;

public class Demo {
    public static void main(String[] args) {
        var names = List.of("Alice", "Bob", "Charlie");
        var copy = List.copyOf(names);
        copy.forEach(System.out::println);

        var nameOpt = Optional.of("Java 10");
        System.out.println(nameOpt.orElseThrow());
    }
}
```

