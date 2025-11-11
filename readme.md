## 19) JDBC Transaction Management (Commit & Rollback)

**Question:**  
Design a JDBC program to demonstrate transaction management using commit and rollback for banking fund transfer.

### Program: `TransactionDemo.java`
```java
import java.sql.*;

public class TransactionDemo {
    public static void main(String[] args) {
        try {
            Class.forName("com.mysql.cj.jdbc.Driver");

            Connection con = DriverManager.getConnection(
                "jdbc:mysql://localhost:3306/testdb", "root", "password");

            con.setAutoCommit(false); // Start Transaction

            Statement stmt = con.createStatement();

            // Withdraw 500 from Account A (AccNo=101)
            stmt.executeUpdate("UPDATE Bank SET Balance = Balance - 500 WHERE AccNo = 101");

            // Deposit 500 to Account B (AccNo=102)
            stmt.executeUpdate("UPDATE Bank SET Balance = Balance + 500 WHERE AccNo = 102");

            con.commit(); // Confirm Transaction
            System.out.println("Transaction Successful (Commit Executed)");

            con.close();
        } catch (Exception e) {
            System.out.println("Error occurred: " + e);
            try {
                // If any error → rollback
                Connection con = DriverManager.getConnection(
                    "jdbc:mysql://localhost:3306/testdb", "root", "password");
                con.rollback();
                System.out.println("Transaction Rolled Back");
            } catch (Exception ex) {
                System.out.println(ex);
            }
        }
    }
}
```

### Output
```
Transaction Successful (Commit Executed)
```
(or)
```
Error occurred: ...
Transaction Rolled Back
```

---

## 20) JSTL Function Tag Demonstration

**Question:**  
Write a program which demonstrates the Function tag of JSTL.

### `functionDemo.jsp`
```jsp
<%@ taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c" %>
<%@ taglib uri="http://java.sun.com/jsp/jstl/functions" prefix="fn" %>

<html>
<body>
<h2>JSTL Function Tag Demo</h2>

<c:set var="message" value="Welcome to Java Programming"/>

<p>Original Text: ${message}</p>

<p>Length of Text: ${fn:length(message)}</p>

<p>Uppercase: ${fn:toUpperCase(message)}</p>

</body>
</html>
```

### Output
```
Original Text: Welcome to Java Programming
Length of Text: 27
Uppercase: WELCOME TO JAVA PROGRAMMING
```

---
