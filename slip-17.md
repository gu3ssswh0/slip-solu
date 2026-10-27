# Slip No. 17 — Java and Python Programming

## Q1 (A) Java: Store command-line Armstrong numbers in an array

**Save as:** `ArmstrongArgs.java`

```java
import java.util.Arrays;

public class ArmstrongArgs {
    static boolean isArmstrong(int n) {
        if (n < 0) return false;
        int digits = String.valueOf(n).length(), value = n;
        long sum = 0;
        do {
            int digit = value % 10;
            long power = 1;
            for (int i = 0; i < digits; i++) power *= digit;
            sum += power;
            value /= 10;
        } while (value > 0);
        return sum == n;
    }

    public static void main(String[] args) {
        int[] armstrong = new int[args.length];
        int count = 0;
        try {
            for (String arg : args) {
                int n = Integer.parseInt(arg);
                if (isArmstrong(n)) armstrong[count++] = n;
            }
            System.out.println(Arrays.toString(Arrays.copyOf(armstrong, count)));
        } catch (NumberFormatException e) {
            System.out.println("Provide integers as command-line arguments.");
        }
    }
}
```

**Run:**

```bash
javac ArmstrongArgs.java
java ArmstrongArgs 0 1 12 153 370 9474
```

## Q1 (B) Java Swing: Store patient details in an SQLite database

**Save as:** `PatientDatabase.java`

```java
import javax.swing.*;
import java.awt.GridLayout;
import java.sql.*;

public class PatientDatabase extends JFrame {
    private final JTextField pid = new JTextField();
    private final JTextField name = new JTextField();
    private final JTextField disease = new JTextField();
    private final JTextField address = new JTextField();

    public PatientDatabase() {
        setTitle("Patient Details");
        setLayout(new GridLayout(5, 2, 5, 5));
        add(new JLabel("PID:")); add(pid);
        add(new JLabel("PName:")); add(name);
        add(new JLabel("Disease:")); add(disease);
        add(new JLabel("Address:")); add(address);
        JButton save = new JButton("Save");
        add(save); add(new JLabel());
        save.addActionListener(e -> savePatient());
        try (Connection con = DriverManager.getConnection("jdbc:sqlite:patients.db");
             Statement st = con.createStatement()) {
            st.executeUpdate("CREATE TABLE IF NOT EXISTS patients (pid TEXT PRIMARY KEY, pname TEXT NOT NULL, disease TEXT NOT NULL, address TEXT NOT NULL)");
        } catch (SQLException e) {
            JOptionPane.showMessageDialog(this, e.getMessage(), "Database Error", JOptionPane.ERROR_MESSAGE);
        }
        setSize(360, 240);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setLocationRelativeTo(null);
        setVisible(true);
    }

    private void savePatient() {
        String sql = "INSERT INTO patients(pid, pname, disease, address) VALUES(?, ?, ?, ?)";
        try (Connection con = DriverManager.getConnection("jdbc:sqlite:patients.db");
             PreparedStatement ps = con.prepareStatement(sql)) {
            ps.setString(1, pid.getText().trim());
            ps.setString(2, name.getText().trim());
            ps.setString(3, disease.getText().trim());
            ps.setString(4, address.getText().trim());
            ps.executeUpdate();
            JOptionPane.showMessageDialog(this, "Patient saved.");
        } catch (SQLException e) {
            JOptionPane.showMessageDialog(this, e.getMessage(), "Database Error", JOptionPane.ERROR_MESSAGE);
        }
    }

    public static void main(String[] args) {
        SwingUtilities.invokeLater(PatientDatabase::new);
    }
}
```

**Dependency:** Place the SQLite JDBC driver JAR named `sqlite-jdbc.jar` beside the file. Driver project: https://github.com/xerial/sqlite-jdbc

**Compile and run on Linux:**

```bash
javac -cp ".:sqlite-jdbc.jar" PatientDatabase.java
java -cp ".:sqlite-jdbc.jar" PatientDatabase
```

## Q2 (A) Python: Convert input text to uppercase when a button is pressed

**Save as:** `uppercase_button.py`

```python
import tkinter as tk

root = tk.Tk()
root.title("Uppercase Text")
entry = tk.Entry(root, width=30)
entry.pack(padx=10, pady=10)
result = tk.Label(root)
result.pack(padx=10, pady=5)
tk.Button(root, text="Convert to Uppercase", command=lambda: result.config(text=entry.get().upper())).pack(pady=10)
root.mainloop()
```

**Run:**

```bash
python uppercase_button.py
```

## Q2 (B) Python: Validate a date using a user-defined Invalid Date Exception

**Save as:** `validate_date.py`

```python
from datetime import date

class InvalidDateException(Exception):
    pass

def accept_date():
    try:
        day = int(input("Day: "))
        month = int(input("Month: "))
        year = int(input("Year: "))
        return date(year, month, day)
    except (ValueError, OverflowError) as error:
        raise InvalidDateException("Invalid Date Exception") from error

def display_date(value):
    print("Date:", value.strftime("%d-%m-%Y"))

try:
    display_date(accept_date())
except InvalidDateException as error:
    print(error)
```

**Run:**

```bash
python validate_date.py
```
