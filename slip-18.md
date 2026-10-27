# Slip No. 18 — Java and Python Programming

## Q1 (A) Java: Calculate areas using method overloading

**Save as:** `AreaOverloading.java`

```java
import java.util.Scanner;

public class AreaOverloading {
    static double area(double r) { return Math.PI * r * r; }
    static double area(double b, double h) { return b * h / 2; }
    static int area(int l, int w) { return l * w; }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.print("Circle radius: ");
        double r = sc.nextDouble();
        System.out.print("Triangle base and height: ");
        double b = sc.nextDouble(), h = sc.nextDouble();
        System.out.print("Rectangle length and width: ");
        int l = sc.nextInt(), w = sc.nextInt();
        System.out.printf("Circle: %.2f%nTriangle: %.2f%nRectangle: %d%n", area(r), area(b, h), area(l, w));
        sc.close();
    }
}
```

**Run:**

```bash
javac AreaOverloading.java
java AreaOverloading
```

## Q1 (B) Java: Remove students whose names start with S

**Save as:** `RemoveSStudents.java`

```java
import java.util.*;

public class RemoveSStudents {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.print("Number of students: ");
        int n = Integer.parseInt(sc.nextLine());
        List<String> names = new ArrayList<>();
        for (int i = 0; i < n; i++) names.add(sc.nextLine().trim());
        names.removeIf(name -> name.toUpperCase(Locale.ROOT).startsWith("S"));
        System.out.println("Remaining students: " + names);
        sc.close();
    }
}
```

**Run:**

```bash
javac RemoveSStudents.java
java RemoveSStudents
```

Enter the number of students, then enter one name per line.

## Q2 (A) Python: Display list elements less than 5

**Save as:** `less_than_five.py`

```python
a = [1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89]
print([x for x in a if x < 5])
```

**Run:**

```bash
python less_than_five.py
```

## Q2 (B) Python Flask: Store and display a to-do list using SQLite

**Save as:** `todo_app.py`

```python
from flask import Flask, request, redirect, url_for, render_template_string
import sqlite3

app = Flask(__name__)
DB = "tasks.db"
PAGE = """
<form method="post"><input name="task" required><button>Add task</button></form>
<ol>{% for task in tasks %}<li>{{ task[0] }}</li>{% endfor %}</ol>
"""

with sqlite3.connect(DB) as con:
    con.execute("CREATE TABLE IF NOT EXISTS tasks (id INTEGER PRIMARY KEY AUTOINCREMENT, task TEXT NOT NULL)")

@app.route("/", methods=["GET", "POST"])
def home():
    if request.method == "POST":
        task = request.form.get("task", "").strip()
        if task:
            with sqlite3.connect(DB) as con:
                con.execute("INSERT INTO tasks(task) VALUES (?)", (task,))
        return redirect(url_for("home"))
    with sqlite3.connect(DB) as con:
        tasks = con.execute("SELECT task FROM tasks ORDER BY id").fetchall()
    return render_template_string(PAGE, tasks=tasks)

if __name__ == "__main__":
    app.run(debug=True)
```

**Run:**

```bash
pip install flask
python todo_app.py
```

Open `http://127.0.0.1:5000`.
