# Slip No. 25 — Java and Python Programming

## Q1 (A) Java: Check whether a string is a palindrome

**Save as:** `StringPalindrome.java`

```java
import java.util.Scanner;

public class StringPalindrome {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        String s = sc.nextLine();
        System.out.println(s.equalsIgnoreCase(new StringBuilder(s).reverse().toString()) ? "Palindrome" : "Not palindrome");
        sc.close();
    }
}
```

**Run:**

```bash
javac StringPalindrome.java
java StringPalindrome
```

## Q1 (B) Java: Create the `Series` package for square and Fibonacci series

Create these four files with the shown folder structure:

```text
SeriesDemo.java
Series/
├── SquareSeries.java
└── FibonacciSeries.java
```

**Save as:** `Series/SquareSeries.java`

```java
package Series;

public class SquareSeries {
    public static void print(int n) {
        for (int i = 1; i <= n; i++) System.out.print((long) i * i + (i == n ? "\n" : " "));
    }
}
```

**Save as:** `Series/FibonacciSeries.java`

```java
package Series;

public class FibonacciSeries {
    public static void print(int n) {
        long a = 0, b = 1;
        for (int i = 0; i < n; i++) {
            System.out.print(a + (i == n - 1 ? "\n" : " "));
            long next = a + b;
            a = b;
            b = next;
        }
    }
}
```

**Save as:** `SeriesDemo.java`

```java
import java.util.Scanner;
import Series.SquareSeries;
import Series.FibonacciSeries;

public class SeriesDemo {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.print("Number of terms: ");
        int n = sc.nextInt();
        if (n < 1) {
            System.out.println("Enter a positive number.");
        } else {
            System.out.print("Squares: ");
            SquareSeries.print(n);
            System.out.print("Fibonacci: ");
            FibonacciSeries.print(n);
        }
        sc.close();
    }
}
```

**Run from the folder containing `SeriesDemo.java`:**

```bash
javac Series/*.java SeriesDemo.java
java SeriesDemo
```

## Q2 (A) Python: Count uppercase and lowercase letters

**Save as:** `case_count.py`

```python
def count_case(text):
    upper = sum(c.isupper() for c in text)
    lower = sum(c.islower() for c in text)
    print("No. of Upper case characters:", upper)
    print("No. of Lower case Characters:", lower)

count_case("The quick Brow Fox")
```

**Run:**

```bash
python case_count.py
```

## Q2 (B) Python: Create, clean, and display a DataFrame with missing and duplicate records

**Install:** `python -m pip install pandas`

**Save as:** `clean_dataframe.py`

```python
import pandas as pd

df = pd.DataFrame({
    "Name": ["Alice", "Bob", "Charlie", "Alice", "Eve"],
    "Age": [20, None, 22, 20, None],
    "City": ["Pune", "Mumbai", None, "Pune", "Nashik"]
})

print("Missing values:\n", df.isna().sum())
df["Age"] = df["Age"].fillna(df["Age"].mean())
df["City"] = df["City"].fillna("Unknown")
print("Duplicate records:", df.duplicated().sum())
df = df.drop_duplicates().reset_index(drop=True)
print("Cleaned DataFrame:\n", df)
```

**Run:**

```bash
python clean_dataframe.py
```
