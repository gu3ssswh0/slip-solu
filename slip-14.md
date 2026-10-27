# Slip No. 14 — Java and Python Programming

## Q1 (A) Java: Calculate power using recursion

**Save as:** `PowerRecursion.java`

```java
import java.util.Scanner;

public class PowerRecursion {
    static double power(double base, int exponent) {
        if (exponent == 0) return 1;
        if (exponent < 0) return 1 / power(base, -exponent);
        return base * power(base, exponent - 1);
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.print("Enter base and integer exponent: ");
        double base = sc.nextDouble();
        int exponent = sc.nextInt();
        if (base == 0 && exponent < 0) System.out.println("Zero cannot have a negative exponent.");
        else System.out.println("Result: " + power(base, exponent));
        sc.close();
    }
}
```

**Run:**

```bash
javac PowerRecursion.java
java PowerRecursion
```

## Q1 (B) Java: Display employee details on the next frame using an event

**Save as:** `EmployeeFrames.java`

```java
import javax.swing.*;
import java.awt.*;

public class EmployeeFrames {
    public static void main(String[] args) {
        SwingUtilities.invokeLater(() -> {
            JFrame frame = new JFrame("Employee Details");
            frame.setLayout(new GridLayout(4, 2, 5, 5));
            JTextField eno = new JTextField(), name = new JTextField(), salary = new JTextField();
            frame.add(new JLabel("Employee Number:"));
            frame.add(eno);
            frame.add(new JLabel("Employee Name:"));
            frame.add(name);
            frame.add(new JLabel("Salary:"));
            frame.add(salary);
            JButton display = new JButton("Display");
            frame.add(display);
            frame.add(new JLabel());
            display.addActionListener(e -> {
                JFrame next = new JFrame("Employee Information");
                next.add(new JLabel("Eno: " + eno.getText() + " | EName: " + name.getText() + " | Sal: " + salary.getText()));
                next.setSize(500, 100);
                next.setLocationRelativeTo(frame);
                next.setDefaultCloseOperation(JFrame.DISPOSE_ON_CLOSE);
                next.setVisible(true);
            });
            frame.setSize(350, 200);
            frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
            frame.setLocationRelativeTo(null);
            frame.setVisible(true);
        });
    }
}
```

**Run:**

```bash
javac EmployeeFrames.java
java EmployeeFrames
```

## Q2 (A) Python: Calculate the surface area and volume of a cylinder

**Save as:** `cylinder.py`

```python
import math

radius = float(input("Enter radius: "))
height = float(input("Enter height: "))
print("Surface area:", 2 * math.pi * radius * (radius + height))
print("Volume:", math.pi * radius ** 2 * height)
```

**Run:**

```bash
python cylinder.py
```

## Q2 (B) Python: Display plaintext and Caesar-encrypted text

**Save as:** `caesar_cipher.py`

```python
def encrypt(text, shift):
    result = []
    for char in text:
        if char.isupper():
            result.append(chr((ord(char) - 65 + shift) % 26 + 65))
        elif char.islower():
            result.append(chr((ord(char) - 97 + shift) % 26 + 97))
        else:
            result.append(char)
    return "".join(result)

plain = input("Enter plaintext: ")
shift = int(input("Enter shift: ")) % 26
print("Plain text:", plain)
print("Cipher text:", encrypt(plain, shift))
```

**Run:**

```bash
python caesar_cipher.py
```
