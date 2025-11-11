## 10) JDBC Application Demonstrating Scrollable ResultSet

**Question:**  
Design a JDBC application which will demonstrate Scrollable Result Set functionality.

### Program: `ScrollableResultSetDemo.java`
```java
import java.sql.*;

public class ScrollableResultSetDemo {
    public static void main(String[] args) {
        try {
            Class.forName("com.mysql.cj.jdbc.Driver");

            Connection con = DriverManager.getConnection(
                "jdbc:mysql://localhost:3306/testdb", "root", "password");

            Statement stmt = con.createStatement(
                ResultSet.TYPE_SCROLL_INSENSITIVE,
                ResultSet.CONCUR_READ_ONLY
            );

            ResultSet rs = stmt.executeQuery("SELECT * FROM Student");

            System.out.println("Forward Direction:");
            while(rs.next()) {
                System.out.println(rs.getInt("RollNo") + "  " + rs.getString("Name"));
            }

            System.out.println("\nReverse Direction:");
            while(rs.previous()) {
                System.out.println(rs.getInt("RollNo") + "  " + rs.getString("Name"));
            }

            // Move to 2nd Record
            rs.absolute(2);
            System.out.println("\nRecord at Position 2:");
            System.out.println(rs.getInt("RollNo") + "  " + rs.getString("Name"));

            con.close();
        } catch(Exception e) {
            System.out.println(e);
        }
    }
}
```

### Output (Example)
```
Forward Direction:
1  Arjun
2  Ravi
3  Sita

Reverse Direction:
3  Sita
2  Ravi
1  Arjun

Record at Position 2:
2  Ravi
```

---

## 11) Testing a Servlet and Deployment Descriptor

**Question:**  
Write down the Program for testing the Servlet and study deployment descriptor.

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
1. Place `TestServlet.java` inside **src**.
2. Place `web.xml` inside **WEB-INF**.
3. Run Tomcat and open:
```
http://localhost:8080/YourProjectName/test
```

### Sample Output
```
Welcome! Servlet is Working Successfully.
```

