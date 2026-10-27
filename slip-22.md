# Slip No. 22 — Java and Python Programming

## Q1 (A) Java: Calculate factorial using a loop

**Save as:** `FactorialLoop.java`

```java
import java.math.BigInteger;
import java.util.Scanner;

public class FactorialLoop {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.print("Enter a non-negative integer: ");
        int n = sc.nextInt();
        if (n < 0) {
            System.out.println("Factorial is not defined for negative integers.");
        } else {
            BigInteger fact = BigInteger.ONE;
            for (int i = 2; i <= n; i++) fact = fact.multiply(BigInteger.valueOf(i));
            System.out.println("Factorial: " + fact);
        }
        sc.close();
    }
}
```

**Run:**

```bash
javac FactorialLoop.java
java FactorialLoop
```

## Q1 (B) Java Swing: Display table records in JTable and navigate with a scrollable ResultSet

**Save as:** `StudentTableNavigation.java`

```java
import javax.sql.rowset.CachedRowSet;
import javax.sql.rowset.RowSetProvider;
import javax.swing.*;
import javax.swing.table.DefaultTableModel;
import java.awt.*;
import java.sql.*;

public class StudentTableNavigation extends JFrame {
    private final CachedRowSet rows;
    private final JTable table = new JTable(new DefaultTableModel(new String[]{"ID", "Name"}, 0));
    private final JLabel status = new JLabel();
    private int count = 0, current = 1;

    public StudentTableNavigation() throws SQLException {
        CachedRowSet data = RowSetProvider.newFactory().createCachedRowSet();
        try (Connection con = DriverManager.getConnection("jdbc:sqlite:students.db");
             Statement st = con.createStatement()) {
            st.executeUpdate("CREATE TABLE IF NOT EXISTS students (id INTEGER PRIMARY KEY AUTOINCREMENT, name TEXT NOT NULL)");
            try (ResultSet c = st.executeQuery("SELECT COUNT(*) FROM students")) {
                c.next();
                if (c.getInt(1) == 0) st.executeUpdate("INSERT INTO students(name) VALUES ('Asha'), ('Rahul'), ('Sam')");
            }
            try (ResultSet rs = st.executeQuery("SELECT id, name FROM students ORDER BY id")) {
                data.populate(rs);
            }
        }
        rows = data;
        DefaultTableModel model = (DefaultTableModel) table.getModel();
        while (rows.next()) {
            model.addRow(new Object[]{rows.getObject(1), rows.getObject(2)});
            count++;
        }
        rows.beforeFirst();
        JPanel buttons = new JPanel();
        addButton(buttons, "First");
        addButton(buttons, "Previous");
        addButton(buttons, "Next");
        addButton(buttons, "Last");
        JPanel bottom = new JPanel(new BorderLayout());
        bottom.add(buttons, BorderLayout.CENTER);
        bottom.add(status, BorderLayout.SOUTH);
        add(new JScrollPane(table), BorderLayout.CENTER);
        add(bottom, BorderLayout.SOUTH);
        setTitle("Student Records");
        setSize(400, 300);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setLocationRelativeTo(null);
        if (count > 0) selectRecord(1);
        setVisible(true);
    }

    private void addButton(JPanel panel, String label) {
        JButton button = new JButton(label);
        button.addActionListener(e -> {
            int next = switch (label) {
                case "First" -> 1;
                case "Previous" -> current - 1;
                case "Next" -> current + 1;
                default -> count;
            };
            selectRecord(next);
        });
        panel.add(button);
    }

    private void selectRecord(int index) {
        if (count == 0) return;
        current = Math.max(1, Math.min(count, index));
        try {
            rows.absolute(current);
            table.setRowSelectionInterval(current - 1, current - 1);
            status.setText("Record " + current + " of " + count);
        } catch (SQLException e) {
            JOptionPane.showMessageDialog(this, e.getMessage());
        }
    }

    public static void main(String[] args) {
        SwingUtilities.invokeLater(() -> {
            try { new StudentTableNavigation(); }
            catch (SQLException e) { JOptionPane.showMessageDialog(null, e.getMessage()); }
        });
    }
}
```

**Dependency:** Place the SQLite JDBC driver JAR named `sqlite-jdbc.jar` beside the file. The program creates `students.db` and sample rows if the table is empty.

**Compile and run on Linux:**

```bash
javac -cp ".:sqlite-jdbc.jar" StudentTableNavigation.java
java -cp ".:sqlite-jdbc.jar" StudentTableNavigation
```

## Q2 (A) Python: Count uppercase and lowercase letters

**Save as:** `count_case.py`

```python
def count_case(text):
    upper = sum(ch.isupper() for ch in text)
    lower = sum(ch.islower() for ch in text)
    print("No. of Upper case characters:", upper)
    print("No. of Lower case characters:", lower)

count_case("The quick Brow Fox")
```

**Run:**

```bash
python count_case.py
```

Expected output: 3 uppercase characters and 12 lowercase characters.

## Q2 (B) Python: E-commerce order analysis with visualizations and report

**Save as:** `ecommerce_analysis.py`

```python
import pandas as pd
import matplotlib.pyplot as plt

orders = pd.DataFrame({
    "Order ID": [101, 102, 103, 104, 105, 106],
    "Product": ["Laptop", "Phone", "Phone", "Mouse", "Laptop", "Keyboard"],
    "Quantity": [1, 2, 1, 3, 2, 2],
    "Price": [50000, 15000, 15000, 500, 50000, 1500],
    "Region": ["West", "North", "West", "South", "East", "North"]
})
orders["Order Value"] = orders["Quantity"] * orders["Price"]
region_sales = orders.groupby("Region")["Order Value"].sum().sort_values(ascending=False)
product_sales = orders.groupby("Product")["Quantity"].sum().sort_values(ascending=False)
top_product = product_sales.index[0]

report = "E-COMMERCE ORDER REPORT\n"
report += f"Total sales: {orders['Order Value'].sum():.2f}\n\nRegion-wise sales:\n{region_sales.to_string()}\n"
report += f"\nTop-selling product by quantity: {top_product} ({product_sales.iloc[0]} units)\n"
print(orders.to_string(index=False))
print("\n" + report)
with open("ecommerce_report.txt", "w", encoding="utf-8") as file:
    file.write(report)

region_sales.plot(kind="bar", title="Region-wise Sales", ylabel="Sales")
plt.tight_layout()
plt.savefig("region_sales.png")
plt.show()

product_sales.plot(kind="bar", title="Units Sold by Product", ylabel="Quantity")
plt.tight_layout()
plt.savefig("product_sales.png")
plt.show()
```

**Run:**

```bash
pip install pandas matplotlib
python ecommerce_analysis.py
```

The sample dataset is included because the question does not provide actual order rows. Replace the values in `orders` with the required dataset. The script generates a text report and two bar charts.
