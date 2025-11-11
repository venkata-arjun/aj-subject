# Advanced Java Programs

---

## 1) JDBC Program using Statement Object

**Question:**  
Write a JDBC program using the Statement object to create a Student table (RollNo, Name, Address) and perform insert, update, delete, and display operations.

### Program: `StudentDB.java`
```java
import java.sql.*;

public class StudentDB {
    public static void main(String[] args) {
        try {
            // Load Driver
            Class.forName("com.mysql.cj.jdbc.Driver");

            // Create Connection
            Connection con = DriverManager.getConnection(
                    "jdbc:mysql://localhost:3306/testdb", "root", "password");

            // Create Statement
            Statement stmt = con.createStatement();

            // Create Table
            String q1 = "CREATE TABLE IF NOT EXISTS Student (" +
                        "RollNo INT PRIMARY KEY, " +
                        "Name VARCHAR(50), " +
                        "Address VARCHAR(100))";
            stmt.executeUpdate(q1);
            System.out.println("Table Created Successfully");

            // Insert Records
            stmt.executeUpdate("INSERT INTO Student VALUES (1, 'Arjun', 'Hyderabad')");
            stmt.executeUpdate("INSERT INTO Student VALUES (2, 'Ravi', 'Chennai')");
            stmt.executeUpdate("INSERT INTO Student VALUES (3, 'Sita', 'Mumbai')");
            System.out.println("Records Inserted");

            // Update Record
            stmt.executeUpdate("UPDATE Student SET Address='Bangalore' WHERE RollNo=2");
            System.out.println("Record Updated");

            // Delete Record
            stmt.executeUpdate("DELETE FROM Student WHERE RollNo=3");
            System.out.println("Record Deleted");

            // Display Records
            ResultSet rs = stmt.executeQuery("SELECT * FROM Student");
            System.out.println("\nStudent Table Records:");
            System.out.println("--------------------------------");
            while (rs.next()) {
                System.out.println(rs.getInt("RollNo") + "  " +
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
1  Arjun  Hyderabad
2  Ravi   Bangalore
```

---

## 2) Servlet Program and Deployment Descriptor

**Question:**  
Write down the program for testing the Servlet and study deployment descriptor.

### Program: `TestServlet.java`
```java
import java.io.*;
import javax.servlet.*;
import javax.servlet.http.*;

public class TestServlet extends HttpServlet {
    public void doGet(HttpServletRequest request, HttpServletResponse response)
            throws ServletException, IOException {

        response.setContentType("text/html");
        PrintWriter out = response.getWriter();

        out.println("<html><body>");
        out.println("<h2>Welcome! Servlet is Working Successfully.</h2>");
        out.println("</body></html>");
    }
}
```

### Deployment Descriptor: `web.xml`
```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://java.sun.com/xml/ns/javaee"
         version="3.0">

    <servlet>
        <servlet-name>test</servlet-name>
        <servlet-class>TestServlet</servlet-class>
    </servlet>

    <servlet-mapping>
        <servlet-name>test</servlet-name>
        <url-pattern>/test</url-pattern>
    </servlet-mapping>

</web-app>
```

### How to Run
1. Place `TestServlet.java` in **src** folder.
2. Place `web.xml` inside **WEB-INF** folder.
3. Deploy project on **Apache Tomcat**.
4. Open browser and enter:
```
http://localhost:8080/YourProjectName/test
```

### Output
```
Welcome! Servlet is Working Successfully.
```

---
