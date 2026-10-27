# Slip No. 11 — Java and Python Programming

## Q1 (A) Java: Menu-driven arithmetic using command-line arguments

Choose `1` for addition, `2` for subtraction, `3` for multiplication, or `4` for division. Supply the choice and two numbers as command-line arguments.

**Save as:** `MenuCalculator.java`

```java
public class MenuCalculator {
    public static void main(String[] args) {
        System.out.println("1 Addition | 2 Subtraction | 3 Multiplication | 4 Division");
        if (args.length != 3) {
            System.out.println("Usage: java MenuCalculator <1-4> <number1> <number2>");
            return;
        }

        try {
            int choice = Integer.parseInt(args[0]);
            double a = Double.parseDouble(args[1]);
            double b = Double.parseDouble(args[2]);
            double result;

            switch (choice) {
                case 1: result = a + b; break;
                case 2: result = a - b; break;
                case 3: result = a * b; break;
                case 4:
                    if (b == 0) {
                        System.out.println("Division by zero is not allowed.");
                        return;
                    }
                    result = a / b;
                    break;
                default:
                    System.out.println("Invalid choice. Choose 1, 2, 3 or 4.");
                    return;
            }
            System.out.println("Result: " + result);
        } catch (NumberFormatException e) {
            System.out.println("Enter a valid choice and numbers.");
        }
    }
}
```

**Run:**

```bash
javac MenuCalculator.java
java MenuCalculator 1 10 5
```

## Q1 (B) Java: Count vowels in a file

Pass the filename as a command-line argument.

**Save as:** `CountVowels.java`

```java
import java.io.IOException;
import java.nio.charset.StandardCharsets;
import java.nio.file.Files;
import java.nio.file.Paths;

public class CountVowels {
    public static void main(String[] args) throws IOException {
        if (args.length != 1) {
            System.out.println("Usage: java CountVowels <filename>");
            return;
        }

        String content = new String(Files.readAllBytes(Paths.get(args[0])), StandardCharsets.UTF_8);
        int count = 0;
        for (char ch : content.toLowerCase().toCharArray()) {
            if ("aeiou".indexOf(ch) >= 0) count++;
        }
        System.out.println("Number of vowels: " + count);
    }
}
```

**Run:**

```bash
javac CountVowels.java
java CountVowels input.txt
```

## Q2 (A) Python: Element-wise sum of tuples

**Save as:** `tuple_sum.py`

```python
t1 = (1, 2, 3, 4)
t2 = (3, 5, 2, 1)
t3 = (2, 2, 3, 1)
print(tuple(map(sum, zip(t1, t2, t3))))
```

**Output:**

```text
(6, 9, 8, 6)
```

## Q2 (B) Python: Find repeated tuple items and check membership

**Save as:** `tuple_repeated_membership.py`

```python
items = tuple(input("Enter tuple items separated by spaces: ").split())
repeated = list(dict.fromkeys(item for item in items if items.count(item) > 1))
print("Repeated items:", repeated)
value = input("Enter an item to search for: ")
print("Exists in tuple" if value in items else "Does not exist in tuple")
```

**Run:**

```bash
python tuple_repeated_membership.py
```
