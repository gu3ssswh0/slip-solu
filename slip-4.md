# Slip No. 4 — Java and Python Programming

## Q1 (A) Java: Display alternate characters from a string

This program displays characters at positions 1, 3, 5, and so on.

**Save as:** `AlternateCharacters.java`

```java
import java.util.Scanner;

public class AlternateCharacters {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.print("Enter a string: ");
        String text = sc.nextLine();

        System.out.print("Alternate characters: ");
        for (int i = 0; i < text.length(); i += 2) {
            System.out.print(text.charAt(i));
        }
        System.out.println();
        sc.close();
    }
}
```

**Run:**

```bash
javac AlternateCharacters.java
java AlternateCharacters
```

## Q1 (B) Java: Check whether a number is positive, negative, or zero

**Save as:** `NumberSign.java`

```java
import java.util.Scanner;

public class NumberSign {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.print("Enter an integer: ");
        int number = sc.nextInt();

        if (number > 0) {
            System.out.println("The number is positive.");
        } else if (number < 0) {
            System.out.println("The number is negative.");
        } else {
            System.out.println("The number is zero.");
        }
        sc.close();
    }
}
```

**Run:**

```bash
javac NumberSign.java
java NumberSign
```

## Q2 (A) Python Flask: Display a page with changing background colors

The color buttons reload the page with the selected background color.

**Save as:** `app.py`

```python
from flask import Flask, request, render_template_string

app = Flask(__name__)
COLORS = {
    "white": "#ffffff",
    "lightblue": "#add8e6",
    "lightgreen": "#90ee90",
    "lightpink": "#ffb6c1",
    "lightyellow": "#ffffe0"
}

PAGE = """
<!doctype html>
<html>
<head>
    <title>Changing Background Colors</title>
    <style>
        body { font-family: Arial, sans-serif; text-align: center; padding: 50px; }
        button { margin: 8px; padding: 10px 16px; cursor: pointer; }
    </style>
</head>
<body style="background-color: {{ background }};">
    <h1>Change Background Color</h1>
    <form method="get">
        <button name="color" value="white" type="submit">White</button>
        <button name="color" value="lightblue" type="submit">Light Blue</button>
        <button name="color" value="lightgreen" type="submit">Light Green</button>
        <button name="color" value="lightpink" type="submit">Light Pink</button>
        <button name="color" value="lightyellow" type="submit">Light Yellow</button>
    </form>
</body>
</html>
"""


@app.route("/")
def index():
    selected = request.args.get("color", "white")
    background = COLORS.get(selected, COLORS["white"])
    return render_template_string(PAGE, background=background)


if __name__ == "__main__":
    app.run(debug=True)
```

**Install and run:**

```bash
python -m pip install flask
python app.py
```

Open `http://127.0.0.1:5000` in a browser.

## Q2 (B) Python: Display Fibonacci terms up to n

This program prints Fibonacci values that are less than or equal to the entered limit `n`.

**Save as:** `fibonacci_till_n.py`

```python
n = int(input("Enter the limit n: "))
first, second = 0, 1

print("Fibonacci terms:", end=" ")
while first <= n:
    print(first, end=" ")
    first, second = second, first + second
print()
```

**Run:**

```bash
python fibonacci_till_n.py
```
