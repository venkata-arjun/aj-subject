## 16) JDBC Batch Processing

**Question:**  
Write a JDBC program to perform batch processing to insert multiple records into the Employee table and display success status.

### Program: `BatchInsertDemo.java`
```java
import java.sql.*;

public class BatchInsertDemo {
    public static void main(String[] args) {
        try {
            Class.forName("com.mysql.cj.jdbc.Driver");

            Connection con = DriverManager.getConnection(
                "jdbc:mysql://localhost:3306/testdb", "root", "password");

            Statement stmt = con.createStatement();

            stmt.addBatch("INSERT INTO Employee VALUES (201, 'Arjun', 45000)");
            stmt.addBatch("INSERT INTO Employee VALUES (202, 'Ravi', 48000)");
            stmt.addBatch("INSERT INTO Employee VALUES (203, 'Sita', 50000)");

            int result[] = stmt.executeBatch();
            System.out.println("Batch Executed Successfully");
            System.out.println("Inserted Records: " + result.length);

            con.close();
        } catch (Exception e) {
            System.out.println(e);
        }
    }
}
```

### Output
```
Batch Executed Successfully
Inserted Records: 3
```

---

## 17) JSTL Core Tag Demonstration

**Question:**  
Write a program which demonstrates the Core tag of JSTL.

### `coreDemo.jsp`
```jsp
<%@ taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c" %>
<html>
<body>
<h2>JSTL Core Tag Demo</h2>

<c:set var="name" value="Arjun"/>
<p>Name: <c:out value="${name}"/></p>

<c:forEach var="i" begin="1" end="5">
    Number: <c:out value="${i}"/> <br>
</c:forEach>

</body>
</html>
```

### Output
```
Name: Arjun
Number: 1
Number: 2
Number: 3
Number: 4
Number: 5
```
