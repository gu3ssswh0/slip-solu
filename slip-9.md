# Slip No. 9 — Java and Python Programming

## Q1 (A) Java: Calculate total, percentage and grade for five subjects

**Save as:** `StudentGrade.java`

```java
import java.util.Scanner;

public class StudentGrade {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int total = 0;

        for (int i = 1; i <= 5; i++) {
            System.out.print("Enter marks for subject " + i + ": ");
            total += sc.nextInt();
        }

        double percentage = total / 5.0;
        String grade = percentage >= 75 ? "Distinction"
                     : percentage >= 60 ? "First Class"
                     : percentage >= 50 ? "Second Class"
                     : percentage >= 40 ? "Pass" : "Fail";

        System.out.println("Total: " + total);
        System.out.println("Percentage: " + percentage + "%");
        System.out.println("Grade: " + grade);
        sc.close();
    }
}
```

**Run:**

```bash
javac StudentGrade.java
java StudentGrade
```

## Q1 (B) Java: Validate PAN and mobile number using a user-defined exception

**Save as:** `ValidateDetails.java`

```java
import java.util.Scanner;

class InvalidDataException extends Exception {
    InvalidDataException() {
        super("Invalid Data");
    }
}

public class ValidateDetails {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.print("Enter PAN: ");
        String pan = sc.next().toUpperCase();
        System.out.print("Enter mobile number: ");
        String mobile = sc.next();

        try {
            if (!pan.matches("[A-Z]{5}[0-9]{4}[A-Z]") || !mobile.matches("[6-9][0-9]{9}"))
                throw new InvalidDataException();
            System.out.println("PAN: " + pan);
            System.out.println("Mobile: " + mobile);
        } catch (InvalidDataException e) {
            System.out.println(e.getMessage());
        }
        sc.close();
    }
}
```

**Run:**

```bash
javac ValidateDetails.java
java ValidateDetails
```

## Q2 (A) Python: Reverse each word in a string

**Save as:** `reverse_words.py`

```python
text = input("Enter a string: ")
print(" ".join(word[::-1] for word in text.split()))
```

**Run:**

```bash
python reverse_words.py
```

## Q2 (B) Python: Check whether a number is prime, perfect or Armstrong

**Save as:** `number_checks.py`

```python
def is_prime(n):
    return n >= 2 and all(n % d for d in range(2, int(n ** 0.5) + 1))

def is_perfect(n):
    return n > 1 and sum(d for d in range(1, n) if n % d == 0) == n

def is_armstrong(n):
    if n < 0:
        return False
    digits = str(n)
    return sum(int(d) ** len(digits) for d in digits) == n

number = int(input("Enter a number: "))
print("Prime" if is_prime(number) else "Not prime")
print("Perfect" if is_perfect(number) else "Not perfect")
print("Armstrong" if is_armstrong(number) else "Not Armstrong")
```

**Run:**

```bash
python number_checks.py
```
