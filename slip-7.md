# Slip No. 7 — Java and Python Programming

## Q1 (A) Java: Throw `NegativeNumberException` for a negative number

**Save as:** `SquareNumber.java`

```java
import java.util.Scanner;

class NegativeNumberException extends Exception {
    NegativeNumberException(String message) {
        super(message);
    }
}

public class SquareNumber {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.print("Enter a number: ");
        int number = sc.nextInt();

        try {
            if (number < 0) throw new NegativeNumberException("Negative number entered.");
            System.out.println("Square: " + number * number);
        } catch (NegativeNumberException e) {
            System.out.println(e.getMessage());
        }
        sc.close();
    }
}
```

**Run:**

```bash
javac SquareNumber.java
java SquareNumber
```

## Q1 (B) Java: Find the cricket player with the maximum batting average

**Save as:** `CricketPlayers.java`

```java
import java.util.Scanner;

class Player {
    int pid, totalRuns, inningsPlayed, notOutTimes;
    String pname;

    Player(int pid, String pname, int totalRuns, int inningsPlayed, int notOutTimes) {
        this.pid = pid;
        this.pname = pname;
        this.totalRuns = totalRuns;
        this.inningsPlayed = inningsPlayed;
        this.notOutTimes = notOutTimes;
    }

    double average() {
        int dismissals = inningsPlayed - notOutTimes;
        return dismissals == 0 ? Double.POSITIVE_INFINITY : (double) totalRuns / dismissals;
    }
}

public class CricketPlayers {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.print("Enter number of players: ");
        int n = sc.nextInt();
        if (n <= 0) {
            System.out.println("Enter at least one player.");
            sc.close();
            return;
        }
        Player[] players = new Player[n];

        for (int i = 0; i < n; i++) {
            System.out.println("Enter player ID, name, total runs, innings played, not-out times:");
            int id = sc.nextInt();
            String name = sc.next();
            int runs = sc.nextInt();
            int innings = sc.nextInt();
            int notOut = sc.nextInt();
            players[i] = new Player(id, name, runs, innings, notOut);
        }

        Player best = players[0];
        for (Player player : players) {
            if (player.average() > best.average()) best = player;
        }

        System.out.println("Player ID: " + best.pid);
        System.out.println("Player Name: " + best.pname);
        System.out.println("Total Runs: " + best.totalRuns);
        System.out.println("Batting Average: " + (Double.isInfinite(best.average()) ? "Not dismissed" : String.format("%.2f", best.average())));
        sc.close();
    }
}
```

**Run:**

```bash
javac CricketPlayers.java
java CricketPlayers
```

## Q2 (A) Python: Display date and time in different formats

**Save as:** `datetime_formats.py`

```python
from datetime import datetime

now = datetime.now()
print("Current date and time:", now.strftime("%d-%m-%Y %H:%M:%S"))
print("Month of year:", now.strftime("%B"))
print("Week number of the year:", now.isocalendar().week)
print("Day of year:", now.strftime("%j"))
print("Day of month:", now.day)
```

**Run:**

```bash
python datetime_formats.py
```

## Q2 (B) Python: Generate a random password with uppercase and lowercase letters

**Save as:** `random_password.py`

```python
import random
import string

length = int(input("Enter password length (minimum 2): "))
if length < 2:
    print("Length must be at least 2.")
else:
    password = [random.choice(string.ascii_uppercase), random.choice(string.ascii_lowercase)]
    password += random.choices(string.ascii_letters, k=length - 2)
    random.shuffle(password)
    print("Password:", "".join(password))
```

**Run:**

```bash
python random_password.py
```
