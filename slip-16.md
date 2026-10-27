# Slip No. 16 — Java and Python Programming

## Q1 (A) Java: Calculate the sum of digits using recursion

**Save as:** `SumDigits.java`

```java
import java.util.Scanner;

public class SumDigits {
    static int sumDigits(int n) {
        n = Math.abs(n);
        return n < 10 ? n : n % 10 + sumDigits(n / 10);
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.print("Enter an integer: ");
        System.out.println("Sum of digits: " + sumDigits(sc.nextInt()));
        sc.close();
    }
}
```

**Run:**

```bash
javac SumDigits.java
java SumDigits
```

## Q1 (B) Java: Sort employee names in ascending order using an object array and static method

**Save as:** `SortEmployees.java`

```java
import java.util.Arrays;
import java.util.Scanner;

class Employee {
    String name;
    Employee(String name) { this.name = name; }
}

public class SortEmployees {
    static void sortEmployees(Employee[] employees) {
        Arrays.sort(employees, (a, b) -> a.name.compareToIgnoreCase(b.name));
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.print("Enter number of employees: ");
        int n = Integer.parseInt(sc.nextLine());
        Employee[] employees = new Employee[n];
        for (int i = 0; i < n; i++) {
            System.out.print("Enter employee name: ");
            employees[i] = new Employee(sc.nextLine());
        }
        sortEmployees(employees);
        for (Employee employee : employees) System.out.println(employee.name);
        sc.close();
    }
}
```

**Run:**

```bash
javac SortEmployees.java
java SortEmployees
```

## Q2 (A) Python Flask: Pass a number to a template and display Pass or Fail

**Save as:** `app.py`

```python
from flask import Flask, request, render_template_string

app = Flask(__name__)
PAGE = """
<form method="post">
  <input type="number" name="marks" required>
  <button type="submit">Check</button>
</form>
{% if marks is not none %}<p>{{ 'Pass' if marks >= 40 else 'Fail' }}</p>{% endif %}
"""

@app.route("/", methods=["GET", "POST"])
def home():
    marks = int(request.form["marks"]) if request.method == "POST" else None
    return render_template_string(PAGE, marks=marks)

if __name__ == "__main__":
    app.run()
```

**Run:**

```bash
python -m pip install flask
python app.py
```

Open `http://127.0.0.1:5000`.

## Q2 (B) Python: Use a user-defined package to calculate cylinder and cuboid area and volume

Create this structure:

```text
slip16/
├── main.py
└── geometry/
    ├── __init__.py
    └── solids.py
```

**Save as:** `geometry/solids.py`

```python
import math

def cylinder(radius, height):
    return 2 * math.pi * radius * (radius + height), math.pi * radius ** 2 * height

def cuboid(length, width, height):
    return 2 * (length * width + length * height + width * height), length * width * height
```

**Save as:** `geometry/__init__.py`

```python
from .solids import cylinder, cuboid
```

**Save as:** `main.py`

```python
from geometry import cylinder, cuboid

r = float(input("Cylinder radius: "))
h = float(input("Cylinder height: "))
area, volume = cylinder(r, h)
print("Cylinder surface area:", area)
print("Cylinder volume:", volume)

l = float(input("Cuboid length: "))
w = float(input("Cuboid width: "))
h = float(input("Cuboid height: "))
area, volume = cuboid(l, w, h)
print("Cuboid surface area:", area)
print("Cuboid volume:", volume)
```

**Run from the `slip16` directory:**

```bash
python main.py
```
