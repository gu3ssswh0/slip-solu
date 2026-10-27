# Slip No. 6 — Java and Python Programming

## Q1 (A) Java: Count even and odd elements in an integer array

**Save as:** `CountEvenOdd.java`

```java
import java.util.Scanner;

public class CountEvenOdd {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.print("Enter number of elements: ");
        int n = sc.nextInt();
        int even = 0, odd = 0;

        for (int i = 0; i < n; i++) {
            int value = sc.nextInt();
            if (value % 2 == 0) even++;
            else odd++;
        }

        System.out.println("Even elements: " + even);
        System.out.println("Odd elements: " + odd);
        sc.close();
    }
}
```

**Run:**

```bash
javac CountEvenOdd.java
java CountEvenOdd
```

## Q1 (B) Java: Check whether a file exists

**Save as:** `CheckFile.java`

```java
import java.io.File;
import java.util.Scanner;

public class CheckFile {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.print("Enter filename: ");
        File file = new File(sc.nextLine());
        System.out.println(file.exists() ? "File exists." : "File does not exist.");
        sc.close();
    }
}
```

**Run:**

```bash
javac CheckFile.java
java CheckFile
```

## Q2 (A) Python: Calculate the area and volume of a cube and sphere using a package

Create this structure:

```text
geometry_project/
├── main.py
└── geometry/
    └── __init__.py
```

**File:** `geometry/__init__.py`

```python
import math

def cube_area(side):
    return 6 * side ** 2

def cube_volume(side):
    return side ** 3

def sphere_area(radius):
    return 4 * math.pi * radius ** 2

def sphere_volume(radius):
    return 4 * math.pi * radius ** 3 / 3
```

**File:** `main.py`

```python
from geometry import cube_area, cube_volume, sphere_area, sphere_volume

side = float(input("Enter cube side: "))
radius = float(input("Enter sphere radius: "))
if side < 0 or radius < 0:
    print("Dimensions cannot be negative.")
else:
    print(f"Cube area: {cube_area(side):.2f}")
    print(f"Cube volume: {cube_volume(side):.2f}")
    print(f"Sphere area: {sphere_area(radius):.2f}")
    print(f"Sphere volume: {sphere_volume(radius):.2f}")
```

**Run from `geometry_project`:**

```bash
python main.py
```

## Q2 (B) Python: Generate and analyze 100 customer ratings

Ratings range from 1 to 5. Ratings of 4 or 5 count as satisfied.

**Save as:** `customer_ratings.py`

```python
import random
from collections import Counter
from statistics import mean, median, pstdev
import matplotlib.pyplot as plt

ratings = [random.randint(1, 5) for _ in range(100)]
frequency = Counter(ratings)

print("Ratings:", ratings)
print("Mean:", mean(ratings))
print("Median:", median(ratings))
print("Standard deviation:", round(pstdev(ratings), 2))
print("Frequency:", {r: frequency[r] for r in range(1, 6)})
print("Satisfaction percentage:", sum(r >= 4 for r in ratings) / len(ratings) * 100, "%")

plt.bar(range(1, 6), [frequency[r] for r in range(1, 6)])
plt.xlabel("Rating")
plt.ylabel("Number of customers")
plt.title("Customer Rating Distribution")
plt.xticks(range(1, 6))
plt.show()
```

**Install and run:**

```bash
python -m pip install matplotlib
python customer_ratings.py
```
