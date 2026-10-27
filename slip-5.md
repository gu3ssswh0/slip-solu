# Slip No. 5 — Java and Python Programming

## Q1 (A) Java: Display the required number pattern

Expected pattern:

```text
5
45
345
2345
12345
```

**Save as:** `NumberPattern.java`

```java
public class NumberPattern {
    public static void main(String[] args) {
        for (int start = 5; start >= 1; start--) {
            for (int number = start; number <= 5; number++) {
                System.out.print(number);
            }
            System.out.println();
        }
    }
}
```

**Run:**

```bash
javac NumberPattern.java
java NumberPattern
```

## Q1 (B) Java: Add two 3 × 3 matrices

**Save as:** `MatrixAddition.java`

```java
import java.util.Scanner;

public class MatrixAddition {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int[][] first = new int[3][3];
        int[][] second = new int[3][3];
        int[][] sum = new int[3][3];

        System.out.println("Enter the elements of the first 3x3 matrix:");
        for (int i = 0; i < 3; i++) {
            for (int j = 0; j < 3; j++) {
                first[i][j] = sc.nextInt();
            }
        }

        System.out.println("Enter the elements of the second 3x3 matrix:");
        for (int i = 0; i < 3; i++) {
            for (int j = 0; j < 3; j++) {
                second[i][j] = sc.nextInt();
            }
        }

        for (int i = 0; i < 3; i++) {
            for (int j = 0; j < 3; j++) {
                sum[i][j] = first[i][j] + second[i][j];
            }
        }

        System.out.println("Resultant matrix:");
        for (int i = 0; i < 3; i++) {
            for (int j = 0; j < 3; j++) {
                System.out.print(sum[i][j] + "\t");
            }
            System.out.println();
        }
        sc.close();
    }
}
```

**Run:**

```bash
javac MatrixAddition.java
java MatrixAddition
```

## Q2 (A) Python: Calculate the area and perimeter of a circle using a package

Create this directory structure:

```text
circle_project/
├── main.py
└── circle_package/
    └── __init__.py
```

### File 1: `circle_package/__init__.py`

```python
import math


def area(radius):
    return math.pi * radius * radius


def perimeter(radius):
    return 2 * math.pi * radius
```

### File 2: `main.py`

```python
from circle_package import area, perimeter

try:
    radius = float(input("Enter the radius of the circle: "))
    if radius < 0:
        print("Radius cannot be negative.")
    else:
        print(f"Area of circle: {area(radius):.2f}")
        print(f"Perimeter of circle: {perimeter(radius):.2f}")
except ValueError:
    print("Please enter a valid number.")
```

**Run from inside `circle_project`:**

```bash
python main.py
```

## Q2 (B) Python: Generate Fibonacci terms using a generator function

The user enters how many terms to generate.

**Save as:** `fibonacci_generator.py`

```python
def fibonacci(count):
    first, second = 0, 1
    for _ in range(count):
        yield first
        first, second = second, first + second

try:
    terms = int(input("How many Fibonacci terms do you want? "))
    if terms < 0:
        print("Enter a non-negative number of terms.")
    else:
        print("Fibonacci terms:", *fibonacci(terms))
except ValueError:
    print("Please enter a valid integer.")
```

**Run:**

```bash
python fibonacci_generator.py
```
