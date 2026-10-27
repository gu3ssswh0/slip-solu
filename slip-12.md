# Slip No. 12 — Java and Python Programming

## Q1 (A) Java: Reverse each string in a string array

**Save as:** `ReverseStrings.java`

```java
import java.util.Scanner;

public class ReverseStrings {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.print("Enter number of strings: ");
        int n = sc.nextInt();
        sc.nextLine();
        String[] words = new String[n];
        for (int i = 0; i < n; i++) words[i] = sc.nextLine();
        for (String word : words) System.out.println(new StringBuilder(word).reverse());
        sc.close();
    }
}
```

**Run:**

```bash
javac ReverseStrings.java
java ReverseStrings
```

## Q1 (B) Java: Show a multiplication table in a list box on button click

**Save as:** `MultiplicationTable.java`

```java
import javax.swing.*;
import java.awt.*;

public class MultiplicationTable extends JFrame {
    private final JTextField number = new JTextField(8);
    private final DefaultListModel<String> model = new DefaultListModel<>();

    public MultiplicationTable() {
        setTitle("Multiplication Table");
        setLayout(new BorderLayout());
        JPanel top = new JPanel();
        top.add(new JLabel("Number:"));
        top.add(number);
        JButton show = new JButton("Show Table");
        top.add(show);
        add(top, BorderLayout.NORTH);
        add(new JScrollPane(new JList<>(model)), BorderLayout.CENTER);
        show.addActionListener(e -> {
            try {
                int n = Integer.parseInt(number.getText().trim());
                model.clear();
                for (int i = 1; i <= 10; i++) model.addElement(n + " x " + i + " = " + (n * i));
            } catch (NumberFormatException ex) {
                JOptionPane.showMessageDialog(this, "Enter a valid integer.");
            }
        });
        setSize(320, 340);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setLocationRelativeTo(null);
        setVisible(true);
    }

    public static void main(String[] args) {
        SwingUtilities.invokeLater(MultiplicationTable::new);
    }
}
```

**Run:**

```bash
javac MultiplicationTable.java
java MultiplicationTable
```

## Q2 (A) Python Flask: Check whether a submitted string is a palindrome

**Save as:** `app.py`

```python
from flask import Flask, request, render_template_string

app = Flask(__name__)
PAGE = """
<form method="post">
  <input name="text" required>
  <button type="submit">Check</button>
</form>
{% if result is not none %}<p>{{ result }}</p>{% endif %}
"""

@app.route("/", methods=["GET", "POST"])
def home():
    result = None
    if request.method == "POST":
        text = "".join(c.lower() for c in request.form["text"] if c.isalnum())
        result = "Palindrome" if text and text == text[::-1] else "Not a palindrome"
    return render_template_string(PAGE, result=result)

if __name__ == "__main__":
    app.run()
```

**Run:**

```bash
python -m pip install flask
python app.py
```

Open `http://127.0.0.1:5000`.

## Q2 (B) Python: Count repeated characters in the given string

**Save as:** `repeated_characters.py`

```python
from collections import Counter

text = "thequickbrownfoxjumpsoverthelazydog"
for char, count in sorted(Counter(text).items(), key=lambda item: (-item[1], item[0])):
    if count > 1:
        print(f"{char}-{count}")
```

**Run:**

```bash
python repeated_characters.py
```
