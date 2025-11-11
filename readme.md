# Advanced Java Programs

---

## 4) JDBC Program using PreparedStatement

**Question:**  
Write a JDBC program using the PreparedStatement object to create a Student table (RollNo, Name, Address) and perform insert, update, delete, and display operations.

### Program: `StudentPreparedDemo.java`
```java
import java.sql.*;

public class StudentPreparedDemo {
    public static void main(String[] args) {
        try {
            Class.forName("com.mysql.cj.jdbc.Driver");

            Connection con = DriverManager.getConnection(
                    "jdbc:mysql://localhost:3306/testdb", "root", "password");

            String create = "CREATE TABLE IF NOT EXISTS Student (" +
                            "RollNo INT PRIMARY KEY, " +
                            "Name VARCHAR(50), " +
                            "Address VARCHAR(100))";
            Statement stmt = con.createStatement();
            stmt.executeUpdate(create);
            System.out.println("Table Created Successfully");

            PreparedStatement ps = con.prepareStatement("INSERT INTO Student VALUES (?, ?, ?)");
            ps.setInt(1, 10);
            ps.setString(2, "Rahul");
            ps.setString(3, "Delhi");
            ps.executeUpdate();

            ps.setInt(1, 11);
            ps.setString(2, "Kiran");
            ps.setString(3, "Pune");
            ps.executeUpdate();
            System.out.println("Records Inserted");

            PreparedStatement psUpdate = con.prepareStatement("UPDATE Student SET Address=? WHERE RollNo=?");
            psUpdate.setString(1, "Bangalore");
            psUpdate.setInt(2, 11);
            psUpdate.executeUpdate();
            System.out.println("Record Updated");

            PreparedStatement psDelete = con.prepareStatement("DELETE FROM Student WHERE RollNo=?");
            psDelete.setInt(1, 10);
            psDelete.executeUpdate();
            System.out.println("Record Deleted");

            ResultSet rs = stmt.executeQuery("SELECT * FROM Student");
            System.out.println("\nStudent Table Records:");
            System.out.println("--------------------------------");
            while (rs.next()) {
                System.out.println(
                    rs.getInt("RollNo") + "  " +
                    rs.getString("Name") + "  " +
                    rs.getString("Address"));
            }

            con.close();
        } catch (Exception e) {
            System.out.println(e);
        }
    }
}
```

### Output
```
Table Created Successfully
Records Inserted
Record Updated
Record Deleted

Student Table Records:
--------------------------------
11  Kiran  Bangalore
```

---

## 6) Addition of Two Numbers Using HTML and JSP

**Question:**  
Input two numbers in HTML and display the addition in JSP.

### HTML File: `input.html`
```html
<!DOCTYPE html>
<html>
<head>
    <title>Addition Form</title>
</head>
<body>
    <h2>Enter Two Numbers</h2>
    <form action="add.jsp" method="post">
        Number 1: <input type="text" name="num1"><br><br>
        Number 2: <input type="text" name="num2"><br><br>
        <input type="submit" value="Add">
    </form>
</body>
</html>
```

### JSP File: `add.jsp`
```jsp
<%
    int a = Integer.parseInt(request.getParameter("num1"));
    int b = Integer.parseInt(request.getParameter("num2"));
    int sum = a + b;
%>
<html>
<body>
    <h2>Addition Result</h2>
    <p>The sum of <b><%=a%></b> and <b><%=b%></b> is: <b><%=sum%></b></p>
</body>
</html>
```

### Output
```
Input:
10 and 20

Result:
The sum of 10 and 20 is: 30
```

---
