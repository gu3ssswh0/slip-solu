# Slip No. 20 — Java and Python Programming

## Q1 (A) Java AWT: Create a red frame titled TYBBACA that closes properly

**Save as:** `RedFrame.java`

```java
import java.awt.*;
import java.awt.event.*;

public class RedFrame {
    public static void main(String[] args) {
        Frame frame = new Frame("TYBBACA");
        frame.setBackground(Color.RED);
        frame.setSize(400, 300);
        frame.addWindowListener(new WindowAdapter() {
            public void windowClosing(WindowEvent e) { frame.dispose(); }
        });
        frame.setLocationRelativeTo(null);
        frame.setVisible(true);
    }
}
```

**Run:**

```bash
javac RedFrame.java
java RedFrame
```

## Q1 (B) Java: TCP/IP client sends two strings; server concatenates them

**Save as:** `ConcatServer.java`

```java
import java.io.*;
import java.net.*;

public class ConcatServer {
    public static void main(String[] args) throws IOException {
        try (ServerSocket server = new ServerSocket(5000)) {
            System.out.println("Waiting for client on port 5000...");
            try (Socket socket = server.accept();
                 BufferedReader in = new BufferedReader(new InputStreamReader(socket.getInputStream()));
                 PrintWriter out = new PrintWriter(socket.getOutputStream(), true)) {
                String first = in.readLine();
                String second = in.readLine();
                out.println(first + second);
            }
        }
    }
}
```

**Save as:** `ConcatClient.java`

```java
import java.io.*;
import java.net.*;
import java.util.Scanner;

public class ConcatClient {
    public static void main(String[] args) throws IOException {
        Scanner sc = new Scanner(System.in);
        System.out.print("First string: ");
        String first = sc.nextLine();
        System.out.print("Second string: ");
        String second = sc.nextLine();
        try (Socket socket = new Socket("localhost", 5000);
             PrintWriter out = new PrintWriter(socket.getOutputStream(), true);
             BufferedReader in = new BufferedReader(new InputStreamReader(socket.getInputStream()))) {
            out.println(first);
            out.println(second);
            System.out.println("Concatenated: " + in.readLine());
        }
        sc.close();
    }
}
```

**Run in two terminals:**

```bash
javac ConcatServer.java ConcatClient.java
java ConcatServer
```

In the second terminal:

```bash
java ConcatClient
```

## Q2 (A) Python: Display all prime numbers up to n

**Save as:** `primes_to_n.py`

```python
def is_prime(n):
    return n >= 2 and all(n % i for i in range(2, int(n ** 0.5) + 1))

n = int(input("Enter n: "))
print([x for x in range(2, n + 1) if is_prime(x)])
```

**Run:**

```bash
python primes_to_n.py
```

## Q2 (B) Python: Generate a dictionary of numbers and their squares

**Save as:** `squares_dictionary.py`

```python
n = int(input("Enter n: "))
print({x: x * x for x in range(1, n + 1)})
```

**Run:**

```bash
python squares_dictionary.py
```
