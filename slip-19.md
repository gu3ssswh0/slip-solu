# Slip No. 19 — Java and Python Programming

## Q1 (A) Java: Display Fibonacci series using a function

**Save as:** `FibonacciFunction.java`

```java
import java.util.Scanner;

public class FibonacciFunction {
    static void display(int n) {
        long a = 0, b = 1;
        for (int i = 0; i < n; i++) {
            System.out.print(a + (i == n - 1 ? "\n" : " "));
            long next = a + b;
            a = b;
            b = next;
        }
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.print("Number of terms: ");
        int n = sc.nextInt();
        if (n < 0) System.out.println("Enter a non-negative number.");
        else display(n);
        sc.close();
    }
}
```

**Run:**

```bash
javac FibonacciFunction.java
java FibonacciFunction
```

## Q1 (B) Java: Demonstrate concurrent bank transactions with synchronized methods

**Save as:** `BankSynchronization.java`

```java
class Account {
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

public class BankSynchronization {
    public static void main(String[] args) throws InterruptedException {
        Account account = new Account();
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
javac BankSynchronization.java
java BankSynchronization
```

## Q2 (A) Python: Display a multiplication table when a button is clicked

**Save as:** `multiplication_button.py`

```python
import tkinter as tk
from tkinter import messagebox

root = tk.Tk()
root.title("Multiplication Table")
entry = tk.Entry(root)
entry.pack(padx=10, pady=8)
result = tk.Label(root, justify="left")
result.pack(padx=10, pady=8)

def show_table():
    try:
        n = int(entry.get())
        result.config(text="\n".join(f"{n} x {i} = {n * i}" for i in range(1, 11)))
    except ValueError:
        messagebox.showerror("Invalid input", "Enter an integer.")

tk.Button(root, text="Show Table", command=show_table).pack(pady=8)
root.mainloop()
```

**Run:**

```bash
python multiplication_button.py
```

## Q2 (B) Python: Use a package to calculate circle area and perimeter

**Folder structure:**

```text
circle_package/
    __init__.py
    circle.py
    main.py
```

**`circle_package/__init__.py`**

```python
from .circle import area, perimeter
```

**`circle_package/circle.py`**

```python
import math

def area(radius):
    return math.pi * radius ** 2

def perimeter(radius):
    return 2 * math.pi * radius
```

**`circle_package/main.py`**

```python
from .circle import area, perimeter

r = float(input("Enter radius: "))
print(f"Area: {area(r):.2f}")
print(f"Perimeter: {perimeter(r):.2f}")
```

**Run from the directory containing `circle_package`:**

```bash
python -m circle_package.main
```
