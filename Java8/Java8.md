# Java 8 Notes

## Key Features
1. **Lambda Expressions** — Functional-style code for short anonymous functions.
2. **Functional Interfaces** — `@FunctionalInterface` with a single abstract method.
3. **Streams API** — Process collections in a functional way.
4. **Default & Static Methods in Interfaces** — Methods in interfaces with a body.
5. **Method References** — Shortcut to call methods in lambdas.
6. **Optional** — Avoid null checks.
7. **New Date & Time API (java.time)** — Better than old `Date` and `Calendar`.

---

## 1. Lambda Expressions

**Old Style (Before Java 8):**
```java
List<String> names = Arrays.asList("John", "Alice", "Bob");

Collections.sort(names, new Comparator<String>() {
    @Override
    public int compare(String a, String b) {
        return a.compareTo(b);
    }
});
```

**Java 8 Style:**
```java
List<String> names = Arrays.asList("John", "Alice", "Bob");
names.sort((a, b) -> a.compareTo(b));
```

---

## 2. Functional Interfaces

```java
@FunctionalInterface
interface MyPrinter {
    void print(String msg);
}

public class Demo {
    public static void main(String[] args) {
        MyPrinter p = (msg) -> System.out.println(msg);
        p.print("Hello Java 8");
    }
}
```

---

## 3. Streams API

**Old Style:**
```java
List<String> names = Arrays.asList("John", "Alice", "Bob");
List<String> filtered = new ArrayList<>();
for (String name : names) {
    if (name.startsWith("A")) {
        filtered.add(name);
    }
}
```

**Java 8 Style:**
```java
List<String> filtered = names.stream()
                             .filter(name -> name.startsWith("A"))
                             .collect(Collectors.toList());
```

**Practice Example:**
```java
List<Integer> nums = Arrays.asList(1, 2, 3, 4, 5);
List<Integer> evenNums = nums.stream()
                             .filter(n -> n % 2 == 0)
                             .collect(Collectors.toList());
```

---

## 4. Optional

**Old Style:**
```java
String name = getName();
if (name != null) {
    System.out.println(name.toUpperCase());
}
```

**Java 8 Style:**
```java
Optional<String> name = Optional.ofNullable(getName());
name.ifPresent(n -> System.out.println(n.toUpperCase()));
```

With default value:
```java
String upper = Optional.ofNullable(getName())
                       .orElse("Default Name")
                       .toUpperCase();
System.out.println(upper);
```

---

## 5. New Date & Time API (java.time)

**Old Style:**
```java
Date date = new Date();
System.out.println(date);
```

**Java 8 Style:**
```java
LocalDate today = LocalDate.now();
LocalDate tomorrow = today.plusDays(1);
System.out.println("Today: " + today);
System.out.println("Tomorrow: " + tomorrow);
```

With formatting:
```java
LocalDateTime now = LocalDateTime.now();
DateTimeFormatter formatter = DateTimeFormatter.ofPattern("dd-MM-yyyy HH:mm");
System.out.println(now.format(formatter));
```

**Practice Example:**
```java
LocalDate today = LocalDate.now();
LocalDate nextMonth = today.plusMonths(1);
System.out.println(nextMonth);
```
