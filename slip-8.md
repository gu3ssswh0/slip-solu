# Slip No. 8 — Java and Python Programming

## Q1 (A) Java: Throw `InvalidAgeException` if age is below 18

**Save as:** `AgeValidation.java`

```java
import java.util.Scanner;

class InvalidAgeException extends Exception {
    InvalidAgeException(String message) {
        super(message);
    }
}

public class AgeValidation {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.print("Enter age: ");
        int age = sc.nextInt();

        try {
            if (age < 18) throw new InvalidAgeException("Invalid age: must be at least 18.");
            System.out.println("Valid age.");
        } catch (InvalidAgeException e) {
            System.out.println(e.getMessage());
        }
        sc.close();
    }
}
```

**Run:**

```bash
javac AgeValidation.java
java AgeValidation
```

## Q1 (B) Java: Display `.txt` files in a directory

**Save as:** `ListTextFiles.java`

```java
import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.Paths;

public class ListTextFiles {
    public static void main(String[] args) throws IOException {
        Path directory = Paths.get(args.length > 0 ? args[0] : ".");
        try (java.util.stream.Stream<Path> files = Files.list(directory)) {
            files.filter(Files::isRegularFile)
                 .filter(p -> p.getFileName().toString().toLowerCase().endsWith(".txt"))
                 .forEach(p -> System.out.println(p.getFileName()));
        }
    }
}
```

**Run:**

```bash
javac ListTextFiles.java
java ListTextFiles path/to/directory
```

Omit the directory argument to search the current directory.

## Q2 (A) Python: Find repeated items in a tuple

**Save as:** `repeated_tuple_items.py`

```python
items = tuple(input("Enter tuple items separated by spaces: ").split())
repeated = list(dict.fromkeys(item for item in items if items.count(item) > 1))
print("Repeated items:", repeated)
```

**Run:**

```bash
python repeated_tuple_items.py
```

## Q2 (B) Python: Read integers, characters and floats from `test.txt` using exceptions

Create `test.txt` with content such as:

```text
10 A 3.14 25 -7 0.5 Z
```

**Save as:** `read_test_file.py`

```python
with open("test.txt", encoding="utf-8") as file:
    for value in file.read().split():
        try:
            int(value)
            print(value, "is an integer")
        except ValueError:
            try:
                float(value)
                print(value, "is a float")
            except ValueError:
                print(value, "is a character" if len(value) == 1 else "is text")
```

**Run:**

```bash
python read_test_file.py
```
