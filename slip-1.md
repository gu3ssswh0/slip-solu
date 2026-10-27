# Slip No. 1 — Java and Python Programming

## Q1 (A) Java: Display characters from A to Z

**Save as:** `DisplayAlphabet.java`

```java
public class DisplayAlphabet {
    public static void main(String[] args) {
        for (char ch = 'A'; ch <= 'Z'; ch++) {
            System.out.print(ch + " ");
        }
        System.out.println();
    }
}
```

**Run:**

```bash
javac DisplayAlphabet.java
java DisplayAlphabet
```

## Q1 (B) Java: Copy only non-numeric data from one file to another

This program removes digit characters (`0`–`9`) from the source text and writes the remaining characters to the destination file. Create `input.txt` first and enter the text to process.

**Save as:** `CopyNonNumericData.java`

```java
import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.Paths;

public class CopyNonNumericData {
    public static void main(String[] args) {
        Path source = Paths.get("input.txt");
        Path destination = Paths.get("output.txt");

        try {
            String content = Files.readString(source);
            String nonNumericContent = content.replaceAll("[0-9]", "");
            Files.writeString(destination, nonNumericContent);
            System.out.println("Non-numeric data copied to output.txt successfully.");
        } catch (IOException e) {
            System.out.println("File error: " + e.getMessage());
        }
    }
}
```

**Run:**

```bash
javac CopyNonNumericData.java
java CopyNonNumericData
```

## Q2 (A) Python: Accept n numbers and remove duplicates from a list

**Save as:** `remove_duplicates.py`

```python
n = int(input("How many numbers do you want to enter? "))
numbers = []

for i in range(n):
    numbers.append(int(input(f"Enter number {i + 1}: ")))

unique_numbers = list(dict.fromkeys(numbers))
print("List without duplicates:", unique_numbers)
```

**Run:**

```bash
python remove_duplicates.py
```

## Q2 (B) Python: Accept a birthdate and calculate age

Enter the date in `DD-MM-YYYY` format. The program accounts for whether the birthday has occurred this year.

**Save as:** `calculate_age.py`

```python
from datetime import date, datetime

birthdate_text = input("Enter your birthdate (DD-MM-YYYY): ")

try:
    birthdate = datetime.strptime(birthdate_text, "%d-%m-%Y").date()
    today = date.today()

    if birthdate > today:
        print("Birthdate cannot be in the future.")
    else:
        age = today.year - birthdate.year
        if (today.month, today.day) < (birthdate.month, birthdate.day):
            age -= 1
        print("Your age is:", age)
except ValueError:
    print("Invalid date. Please use DD-MM-YYYY.")
```

**Run:**

```bash
python calculate_age.py
```
