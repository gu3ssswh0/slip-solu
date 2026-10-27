# Slip No. 24 — Java and Python Programming

## Q1 (A) Java: Count digits, spaces, and characters in a file

**Save as:** `CountFileCharacters.java`

```java
import java.nio.file.Files;
import java.nio.file.Path;

public class CountFileCharacters {
    public static void main(String[] args) throws Exception {
        if (args.length != 1) {
            System.out.println("Usage: java CountFileCharacters <filename>");
            return;
        }
        String text = Files.readString(Path.of(args[0]));
        long digits = text.chars().filter(Character::isDigit).count();
        long spaces = text.chars().filter(c -> c == ' ').count();
        long other = text.length() - digits - spaces;
        System.out.println("Digits: " + digits);
        System.out.println("Spaces: " + spaces);
        System.out.println("Other characters: " + other);
        System.out.println("Total characters: " + text.length());
    }
}
```

**Run (Java 11 or later):**

```bash
javac CountFileCharacters.java
java CountFileCharacters input.txt
```

## Q1 (B) Java: Demonstrate concurrent bank transactions using synchronized methods

**Save as:** `BankSynchronization24.java`

```java
class Account24 {
    private int balance = 1000;

    synchronized void deposit(int amount) {
        balance += amount;
        System.out.println("Deposited " + amount + "; balance=" + balance);
    }

    synchronized void withdraw(int amount) {
        if (balance >= amount) {
            balance -= amount;
            System.out.println("Withdrew " + amount + "; balance=" + balance);
        } else {
            System.out.println("Insufficient balance");
        }
    }

    synchronized int getBalance() { return balance; }
}

public class BankSynchronization24 {
    public static void main(String[] args) throws InterruptedException {
        Account24 account = new Account24();
        Thread t1 = new Thread(() -> { account.deposit(500); account.withdraw(200); });
        Thread t2 = new Thread(() -> { account.withdraw(300); account.deposit(100); });
        t1.start();
        t2.start();
        t1.join();
        t2.join();
        System.out.println("Final balance: " + account.getBalance());
    }
}
```

**Run:**

```bash
javac BankSynchronization24.java
java BankSynchronization24
```

## Q2 (A) Python: Check whether a number is prime and calculate its factorial

**Save as:** `prime_factorial.py`

```python
def is_prime(n):
    return n >= 2 and all(n % i for i in range(2, int(n ** 0.5) + 1))

def factorial(n):
    result = 1
    for i in range(2, n + 1):
        result *= i
    return result

n = int(input("Enter a non-negative integer: "))
if n < 0:
    print("Enter a non-negative integer.")
else:
    print("Prime" if is_prime(n) else "Not prime")
    print("Factorial:", factorial(n))
```

**Run:**

```bash
python prime_factorial.py
```

## Q2 (B) Python NumPy: Analyze feedback ratings from 50 customers

**Save as:** `customer_feedback.py`

```python
import numpy as np
import matplotlib.pyplot as plt

np.random.seed(42)
ratings = np.random.randint(1, 6, 50)
frequency = np.bincount(ratings, minlength=6)[1:]

print("Ratings:", ratings.tolist())
print("Mean:", np.mean(ratings))
print("Median:", np.median(ratings))
print("Standard deviation:", np.std(ratings))
for rating, count in enumerate(frequency, start=1):
    print(f"Rating {rating}: {count}")

plt.bar(range(1, 6), frequency)
plt.xlabel("Rating")
plt.ylabel("Number of Customers")
plt.title("Customer Feedback Ratings")
plt.xticks(range(1, 6))
plt.tight_layout()
plt.show()
```

**Run:**

```bash
pip install numpy matplotlib
python customer_feedback.py
```
