# Slip No. 29 — Java and Python Programming

## Q1 (A) Java: Check voting eligibility and handle exceptions

**Save as:** `VotingEligibility.java`

```java
import java.util.Scanner;

class InvalidAgeException extends Exception {
    InvalidAgeException(String message) { super(message); }
}

public class VotingEligibility {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        try {
            System.out.print("Enter age: ");
            int age = Integer.parseInt(sc.nextLine().trim());
            if (age < 0) throw new InvalidAgeException("Invalid age.");
            System.out.println(age >= 18 ? "Eligible to vote" : "Not eligible to vote");
        } catch (InvalidAgeException e) {
            System.out.println(e.getMessage());
        } catch (NumberFormatException e) {
            System.out.println("Please enter a valid integer age.");
        }
        sc.close();
    }
}
```

**Run:**

```bash
javac VotingEligibility.java
java VotingEligibility
```

## Q1 (B) Java: Classify characters read from a file

**Save as:** `ClassifyFileCharacters.java`

```java
import java.nio.file.Files;
import java.nio.file.Path;

public class ClassifyFileCharacters {
    static String show(char c) {
        if (c == ' ') return "<space>";
        if (c == '\t') return "<tab>";
        if (c == '\n') return "<newline>";
        if (c == '\r') return "<carriage return>";
        return String.valueOf(c);
    }

    public static void main(String[] args) throws Exception {
        if (args.length != 1) {
            System.out.println("Usage: java ClassifyFileCharacters <filename>");
            return;
        }
        String text = Files.readString(Path.of(args[0]));
        String[] names = {"Uppercase letter", "Lowercase letter", "Digit", "Whitespace", "Special symbol"};
        int[] counts = new int[5];
        for (char c : text.toCharArray()) {
            int type = Character.isUpperCase(c) ? 0 : Character.isLowerCase(c) ? 1 : Character.isDigit(c) ? 2 : Character.isWhitespace(c) ? 3 : 4;
            counts[type]++;
            System.out.println(show(c) + " -> " + names[type]);
        }
        for (int i = 0; i < names.length; i++) System.out.println(names[i] + ": " + counts[i]);
    }
}
```

**Run:**

```bash
javac ClassifyFileCharacters.java
java ClassifyFileCharacters input.txt
```

Replace `input.txt` with the file to read.

## Q2 (A) Python: Calculate the volume of a sphere

**Save as:** `sphere_volume.py`

```python
import math

r = float(input("Enter radius: "))
if r < 0:
    print("Radius cannot be negative.")
else:
    print("Volume:", (4 / 3) * math.pi * r ** 3)
```

**Run:**

```bash
python sphere_volume.py
```

## Q2 (B) Python: Analyze marks of 15 students using NumPy

**Install:** `python -m pip install numpy`

**Save as:** `student_marks.py`

```python
import numpy as np

marks = np.array([78, 85, 62, 90, 56, 73, 88, 69, 95, 81, 47, 76, 84, 59, 92])
average = marks.mean()

print("Total students:", marks.size)
print("Average marks:", round(average, 2))
print("Highest marks:", marks.max())
print("Lowest marks:", marks.min())
print("Students above average:", [(i + 1, int(mark)) for i, mark in enumerate(marks) if mark > average])
print("Top 3 scores:", np.sort(marks)[-3:][::-1].tolist())
```

**Run:**

```bash
python student_marks.py
```
