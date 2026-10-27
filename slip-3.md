# Slip No. 3 — Java and Python Programming

## Q1 (A) Java: Check an Armstrong number using `static`

**Save as:** `ArmstrongNumber.java`

```java
import java.util.Scanner;

public class ArmstrongNumber {
    public static boolean isArmstrong(int number) {
        if (number < 0) {
            return false;
        }

        int digits = String.valueOf(number).length();
        int original = number;
        int sum = 0;

        do {
            int digit = number % 10;
            sum += (int) Math.pow(digit, digits);
            number /= 10;
        } while (number > 0);

        return sum == original;
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.print("Enter a number: ");
        int number = sc.nextInt();

        if (isArmstrong(number)) {
            System.out.println(number + " is an Armstrong number.");
        } else {
            System.out.println(number + " is not an Armstrong number.");
        }
        sc.close();
    }
}
```

**Run:**

```bash
javac ArmstrongNumber.java
java ArmstrongNumber
```

## Q1 (B) Java: Find the largest of three numbers using nested `if-else`

**Save as:** `LargestOfThree.java`

```java
import java.util.Scanner;

public class LargestOfThree {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.print("Enter three numbers: ");
        int a = sc.nextInt();
        int b = sc.nextInt();
        int c = sc.nextInt();
        int largest;

        if (a >= b) {
            if (a >= c) {
                largest = a;
            } else {
                largest = c;
            }
        } else {
            if (b >= c) {
                largest = b;
            } else {
                largest = c;
            }
        }

        System.out.println("Largest number: " + largest);
        sc.close();
    }
}
```

**Run:**

```bash
javac LargestOfThree.java
java LargestOfThree
```

## Q2 (A) Python: Check a dictionary key and replace its key-value pair

This program reads string key-value pairs, checks whether the old key exists, and if it does, removes that pair and inserts the new key-value pair.

**Save as:** `replace_dictionary_pair.py`

```python
data = {}
count = int(input("How many key-value pairs do you want to enter? "))

for i in range(count):
    key = input(f"Enter key {i + 1}: ")
    value = input(f"Enter value {i + 1}: ")
    data[key] = value

old_key = input("Enter the key to replace: ")

if old_key in data:
    new_key = input("Enter the new key: ")
    new_value = input("Enter the new value: ")
    del data[old_key]
    data[new_key] = new_value
    print("Updated dictionary:", data)
else:
    print("Key does not exist.")
    print("Dictionary:", data)
```

**Run:**

```bash
python replace_dictionary_pair.py
```

## Q2 (B) Python: Display all prime numbers up to n

**Save as:** `primes_till_n.py`

```python
def is_prime(number):
    if number < 2:
        return False
    divisor = 2
    while divisor * divisor <= number:
        if number % divisor == 0:
            return False
        divisor += 1
    return True

n = int(input("Enter n: "))
print("Prime numbers up to", n, ":", end=" ")
for number in range(2, n + 1):
    if is_prime(number):
        print(number, end=" ")
print()
```

**Run:**

```bash
python primes_till_n.py
```
