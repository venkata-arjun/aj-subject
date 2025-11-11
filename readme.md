## 7) JDBC Program Using Stored Procedures

**Question:**  
Write a JDBC program to interact with a database by creating and invoking stored procedures — one to insert a record into the Employee table and another to retrieve the salary of a given employee ID, and display the results.

### SQL (Run in MySQL Before Running Java Program)
```sql
CREATE TABLE Employee (
    EmpID INT PRIMARY KEY,
    EmpName VARCHAR(50),
    Salary INT
);

CREATE PROCEDURE InsertEmp(IN id INT, IN name VARCHAR(50), IN sal INT)
BEGIN
    INSERT INTO Employee VALUES(id, name, sal);
END;

CREATE PROCEDURE GetSalary(IN id INT, OUT sal INT)
BEGIN
    SELECT Salary INTO sal FROM Employee WHERE EmpID = id;
END;
```

### Java Program: `StoredProcedureDemo.java`
```java
import java.sql.*;

public class StoredProcedureDemo {
    public static void main(String[] args) {
        try {
            Class.forName("com.mysql.cj.jdbc.Driver");

            Connection con = DriverManager.getConnection(
                "jdbc:mysql://localhost:3306/testdb", "root", "password");

            // Insert Employee Record
            CallableStatement cs1 = con.prepareCall("{call InsertEmp(?, ?, ?)}");
            cs1.setInt(1, 101);
            cs1.setString(2, "Arjun");
            cs1.setInt(3, 45000);
            cs1.execute();
            System.out.println("Record Inserted");

            // Get Salary of Employee
            CallableStatement cs2 = con.prepareCall("{call GetSalary(?, ?)}");
            cs2.setInt(1, 101);
            cs2.registerOutParameter(2, Types.INTEGER);
            cs2.execute();

            int salary = cs2.getInt(2);
            System.out.println("Salary of Employee 101 = " + salary);

            con.close();
        } catch (Exception e) {
            System.out.println(e);
        }
    }
}
```

### Output
```
Record Inserted
Salary of Employee 101 = 45000
```

---

## 8) Login Form and State Management (Cookies, Session, URL Rewriting)

### HTML Login Page: `login.html`
```html
<!DOCTYPE html>
<html>
<body>
<h2>Login</h2>
<form action="LoginServlet" method="post">
    Username: <input type="text" name="user"><br><br>
    <input type="submit" value="Login">
</form>
</body>
</html>
```

### Servlet: `LoginServlet.java`
```java
import java.io.*;
import javax.servlet.*;
import javax.servlet.http.*;

public class LoginServlet extends HttpServlet {
    public void doPost(HttpServletRequest request, HttpServletResponse response)
    throws ServletException, IOException {

        String user = request.getParameter("user");
        response.setContentType("text/html");
        PrintWriter out = response.getWriter();

        // Store using Cookie
        Cookie c = new Cookie("username", user);
        response.addCookie(c);

        // Store using Session
        HttpSession session = request.getSession();
        session.setAttribute("u", user);

        // URL Rewriting Link
        out.println("<a href='WelcomeServlet?uname=" + user + "'>Go to Welcome Page</a>");
    }
}
```

### Servlet to Display State: `WelcomeServlet.java`
```java
import java.io.*;
import javax.servlet.*;
import javax.servlet.http.*;

public class WelcomeServlet extends HttpServlet {
    public void doGet(HttpServletRequest request, HttpServletResponse response)
    throws ServletException, IOException {

        response.setContentType("text/html");
        PrintWriter out = response.getWriter();

        // Cookie Data
        Cookie[] ck = request.getCookies();
        String cookieUser = ck[0].getValue();

        // Session Data
        HttpSession session = request.getSession();
        String sessionUser = (String) session.getAttribute("u");

        // URL Rewrite Data
        String urlUser = request.getParameter("uname");

        out.println("<h2>Cookie User: " + cookieUser + "</h2>");
        out.println("<h2>Session User: " + sessionUser + "</h2>");
        out.println("<h2>URL Rewrite User: " + urlUser + "</h2>");
    }
}
```

### Output
```
Cookie User: Arjun
Session User: Arjun
URL Rewrite User: Arjun
```

