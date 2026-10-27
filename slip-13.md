# Slip No. 13 — Java and Python Programming

## Q1 (A) Java: Store integers in an ArrayList and display them in reverse order

**Save as:** `ReverseArrayList.java`

```java
import java.util.ArrayList;
import java.util.Scanner;

public class ReverseArrayList {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.print("Enter number of integers: ");
        int n = sc.nextInt();
        ArrayList<Integer> numbers = new ArrayList<>();
        for (int i = 0; i < n; i++) numbers.add(sc.nextInt());
        for (int i = numbers.size() - 1; i >= 0; i--) System.out.println(numbers.get(i));
        sc.close();
    }
}
```

**Run:**

```bash
javac ReverseArrayList.java
java ReverseArrayList
```

## Q1 (B) Java: Greet the user using their name in uppercase

**Save as:** `UppercaseGreeting.java`

```java
import java.util.Scanner;

public class UppercaseGreeting {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.print("Enter your name: ");
        String name = sc.nextLine().toUpperCase();
        System.out.println("Hello, " + name + ", nice to meet you!");
        sc.close();
    }
}
```

**Run:**

```bash
javac UppercaseGreeting.java
java UppercaseGreeting
```

## Q2 (A) Python: Accept a positive integer using exception handling

**Save as:** `positive_integer.py`

```python
try:
    number = int(input("Enter a positive integer: "))
    if number <= 0:
        raise ValueError
    print("Valid positive integer:", number)
except ValueError:
    print("Invalid input. Enter a positive integer.")
```

**Run:**

```bash
python positive_integer.py
```

## Q2 (B) Python: Remove characters at even index positions using a function

**Save as:** `remove_even_indices.py`

```python
def remove_even_indices(text):
    return text[1::2]

text = input("Enter a string: ")
print(remove_even_indices(text))
```

**Run:**

```bash
python remove_even_indices.py
```
