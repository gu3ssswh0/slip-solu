# Slip No. 2 — Java and Python Programming

## Q1 (A) Java: Display all vowels in a given string

**Save as:** `DisplayVowels.java`

```java
import java.util.Scanner;

public class DisplayVowels {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.print("Enter a string: ");
        String text = sc.nextLine();

        System.out.print("Vowels: ");
        boolean found = false;
        for (int i = 0; i < text.length(); i++) {
            char ch = Character.toLowerCase(text.charAt(i));
            if (ch == 'a' || ch == 'e' || ch == 'i' || ch == 'o' || ch == 'u') {
                System.out.print(text.charAt(i) + " ");
                found = true;
            }
        }
        if (!found) {
            System.out.print("No vowels found");
        }
        System.out.println();
        sc.close();
    }
}
```

**Run:**

```bash
javac DisplayVowels.java
java DisplayVowels
```

## Q1 (B) Java: Arithmetic using command-line arguments

Use the argument order `number1 operator number2`, for example `java CommandLineArithmetic 12 + 4`.

**Save as:** `CommandLineArithmetic.java`

```java
public class CommandLineArithmetic {
    public static void main(String[] args) {
        if (args.length != 3) {
            System.out.println("Usage: java CommandLineArithmetic number1 operator number2");
            return;
        }

        try {
            double first = Double.parseDouble(args[0]);
            String operator = args[1];
            double second = Double.parseDouble(args[2]);
            double result;

            switch (operator) {
                case "+":
                    result = first + second;
                    break;
                case "-":
                    result = first - second;
                    break;
                case "*":
                    result = first * second;
                    break;
                case "/":
                    if (second == 0) {
                        System.out.println("Division by zero is not allowed.");
                        return;
                    }
                    result = first / second;
                    break;
                case "%":
                    if (second == 0) {
                        System.out.println("Modulo by zero is not allowed.");
                        return;
                    }
                    result = first % second;
                    break;
                default:
                    System.out.println("Invalid operator. Use +, -, *, / or %.");
                    return;
            }

            System.out.println("Result: " + result);
        } catch (NumberFormatException e) {
            System.out.println("Please provide valid numbers.");
        }
    }
}
```

**Run:**

```bash
javac CommandLineArithmetic.java
java CommandLineArithmetic 12 + 4
```

For multiplication, quote or escape `*` if your shell expands it: `java CommandLineArithmetic 12 '*' 4`.

## Q2 (A) Python: Count uppercase and lowercase letters

For `The quick Brown Fox`, the expected counts are 3 uppercase letters and 13 lowercase letters.

**Save as:** `count_case.py`

```python
def count_case(text):
    uppercase = sum(1 for ch in text if ch.isupper())
    lowercase = sum(1 for ch in text if ch.islower())
    return uppercase, lowercase

sample = input("Enter a string: ")
upper_count, lower_count = count_case(sample)
print("No. of Upper case characters:", upper_count)
print("No. of Lower case characters:", lower_count)
```

**Run:**

```bash
python count_case.py
```

## Q2 (B) Python Flask: Student registration using SQLite

The app creates a `registrations` table, saves submitted students, and displays all saved records in an HTML table.

**Save as:** `app.py`

```python
import sqlite3
from flask import Flask, request, redirect, url_for, render_template_string

app = Flask(__name__)
DATABASE = "students.db"


def get_connection():
    connection = sqlite3.connect(DATABASE)
    connection.row_factory = sqlite3.Row
    return connection


def initialize_database():
    with get_connection() as connection:
        connection.execute("""
            CREATE TABLE IF NOT EXISTS registrations (
                id INTEGER PRIMARY KEY AUTOINCREMENT,
                name TEXT NOT NULL,
                email TEXT NOT NULL,
                course TEXT NOT NULL,
                year TEXT NOT NULL
            )
        """)


PAGE = """
<!doctype html>
<html>
<head>
    <title>Student Registration</title>
    <style>
        body { font-family: Arial, sans-serif; margin: 30px; }
        input { display: block; margin: 8px 0 14px; padding: 8px; width: 280px; }
        button { padding: 8px 14px; }
        table { border-collapse: collapse; margin-top: 24px; width: 100%; }
        th, td { border: 1px solid #999; padding: 8px; text-align: left; }
        th { background: #eeeeee; }
    </style>
</head>
<body>
    <h1>Student Registration</h1>
    <form method="post">
        <label>Name</label><input name="name" required>
        <label>Email</label><input name="email" type="email" required>
        <label>Course</label><input name="course" required>
        <label>Year</label><input name="year" required>
        <button type="submit">Register</button>
    </form>
    <h2>Registered Students</h2>
    <table>
        <tr><th>ID</th><th>Name</th><th>Email</th><th>Course</th><th>Year</th></tr>
        {% for student in students %}
        <tr>
            <td>{{ student['id'] }}</td>
            <td>{{ student['name'] }}</td>
            <td>{{ student['email'] }}</td>
            <td>{{ student['course'] }}</td>
            <td>{{ student['year'] }}</td>
        </tr>
        {% endfor %}
    </table>
</body>
</html>
"""


@app.route("/", methods=["GET", "POST"])
def index():
    if request.method == "POST":
        name = request.form["name"].strip()
        email = request.form["email"].strip()
        course = request.form["course"].strip()
        year = request.form["year"].strip()

        with get_connection() as connection:
            connection.execute(
                "INSERT INTO registrations (name, email, course, year) VALUES (?, ?, ?, ?)",
                (name, email, course, year)
            )
        return redirect(url_for("index"))

    with get_connection() as connection:
        students = connection.execute(
            "SELECT id, name, email, course, year FROM registrations ORDER BY id DESC"
        ).fetchall()
    return render_template_string(PAGE, students=students)


if __name__ == "__main__":
    initialize_database()
    app.run(debug=True)
```

**Install and run:**

```bash
python -m pip install flask
python app.py
```

Open `http://127.0.0.1:5000` in a browser.
