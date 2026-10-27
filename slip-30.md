# Slip No. 30 — Java and Python Programming

## Q1 (A) Java: Handle zero, non-numeric input, and check a palindrome number

**Save as:** `NumberPalindrome.java`

```java
import java.math.BigInteger;
import java.util.Scanner;

public class NumberPalindrome {
    static class NumberIsZeroException extends Exception {
        NumberIsZeroException() { super("Number is Zero"); }
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.print("Enter a number: ");
        String input = sc.nextLine().trim();
        try {
            BigInteger number = new BigInteger(input);
            if (number.signum() == 0) throw new NumberIsZeroException();
            String value = number.toString();
            System.out.println(value.equals(new StringBuilder(value).reverse().toString()) ? "Palindrome" : "Not palindrome");
        } catch (NumberIsZeroException e) {
            System.out.println(e.getMessage());
        } catch (NumberFormatException e) {
            System.out.println("Number is Invalid");
        }
        sc.close();
    }
}
```

**Run:**

```bash
javac NumberPalindrome.java
java NumberPalindrome
```

## Q1 (B) Java Swing: Design the Personal Information form

**Save as:** `PersonalInformation.java`

```java
import javax.swing.*;
import java.awt.*;

public class PersonalInformation {
    public static void main(String[] args) {
        JFrame frame = new JFrame("Personal Information");
        JTextField first = new JTextField(), last = new JTextField(), address = new JTextField(), mobile = new JTextField();
        JRadioButton male = new JRadioButton("Male"), female = new JRadioButton("Female");
        ButtonGroup gender = new ButtonGroup();
        gender.add(male);
        gender.add(female);
        JPanel genders = new JPanel(new FlowLayout(FlowLayout.LEFT, 5, 0));
        genders.add(male);
        genders.add(female);
        JCheckBox computer = new JCheckBox("Computer"), sports = new JCheckBox("Sports"), music = new JCheckBox("Music");
        JPanel interests = new JPanel(new FlowLayout(FlowLayout.LEFT, 5, 0));
        interests.add(computer);
        interests.add(sports);
        interests.add(music);
        JPanel form = new JPanel(new GridLayout(0, 2, 5, 5));
        form.add(new JLabel("First Name:")); form.add(first);
        form.add(new JLabel("Last Name:")); form.add(last);
        form.add(new JLabel("Address:")); form.add(address);
        form.add(new JLabel("Mobile Number:")); form.add(mobile);
        form.add(new JLabel("Gender:")); form.add(genders);
        form.add(new JLabel("Your Interests:")); form.add(interests);
        JButton submit = new JButton("Submit"), reset = new JButton("Reset");
        JPanel buttons = new JPanel();
        buttons.add(submit);
        buttons.add(reset);
        submit.addActionListener(e -> JOptionPane.showMessageDialog(frame,
            "First Name: " + first.getText() + "\nLast Name: " + last.getText() + "\nAddress: " + address.getText() +
            "\nMobile Number: " + mobile.getText() + "\nGender: " + (male.isSelected() ? "Male" : female.isSelected() ? "Female" : "") +
            "\nInterests: " + (computer.isSelected() ? "Computer " : "") + (sports.isSelected() ? "Sports " : "") + (music.isSelected() ? "Music" : "")));
        reset.addActionListener(e -> {
            first.setText(""); last.setText(""); address.setText(""); mobile.setText("");
            gender.clearSelection(); computer.setSelected(false); sports.setSelected(false); music.setSelected(false);
        });
        frame.add(new JLabel("Personal Information", SwingConstants.CENTER), BorderLayout.NORTH);
        frame.add(form, BorderLayout.CENTER);
        frame.add(buttons, BorderLayout.SOUTH);
        frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        frame.setSize(500, 300);
        frame.setLocationRelativeTo(null);
        frame.setVisible(true);
    }
}
```

**Run:**

```bash
javac PersonalInformation.java
java PersonalInformation
```

## Q2 (A) Python: Count occurrences of a character in a string

**Save as:** `character_count.py`

```python
text = input("Enter a string: ")
char = input("Enter one character: ")
if len(char) != 1:
    print("Enter exactly one character.")
else:
    print("Occurrences:", text.count(char))
```

**Run:**

```bash
python character_count.py
```

## Q2 (B) Python: Validate and display a date using a user-defined exception

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
    except (ValueError, OverflowError):
        raise InvalidDateException("Invalid Date Exception")

def display_date(value):
    print("Date:", value.strftime("%d-%m-%Y"))

try:
    display_date(accept_date())
except InvalidDateException as e:
    print(e)
```

**Run:**

```bash
python validate_date.py
```
