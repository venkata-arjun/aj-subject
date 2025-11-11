## 13) CRUD Operations Using Spring JDBC Template

**Question:**  
Write a JDBC program to perform CRUD operations using Spring JDBC Template.

### 1) `applicationContext.xml`
```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="
       http://www.springframework.org/schema/beans
       http://www.springframework.org/schema/beans/spring-beans.xsd">

    <bean id="dataSource" class="org.springframework.jdbc.datasource.DriverManagerDataSource">
        <property name="driverClassName" value="com.mysql.cj.jdbc.Driver" />
        <property name="url" value="jdbc:mysql://localhost:3306/testdb" />
        <property name="username" value="root" />
        <property name="password" value="password" />
    </bean>

    <bean id="jdbcTemplate" class="org.springframework.jdbc.core.JdbcTemplate">
        <property name="dataSource" ref="dataSource" />
    </bean>

    <bean id="employeeDAO" class="EmployeeDAO">
        <property name="jdbcTemplate" ref="jdbcTemplate" />
    </bean>

</beans>
```

### 2) `EmployeeDAO.java`
```java
import org.springframework.jdbc.core.JdbcTemplate;

public class EmployeeDAO {
    JdbcTemplate jdbcTemplate;

    public void setJdbcTemplate(JdbcTemplate jdbcTemplate) {
        this.jdbcTemplate = jdbcTemplate;
    }

    public void insert(int id, String name, int salary) {
        jdbcTemplate.update("INSERT INTO Employee VALUES (?, ?, ?)", id, name, salary);
        System.out.println("Record Inserted");
    }

    public void update(int id, int salary) {
        jdbcTemplate.update("UPDATE Employee SET Salary=? WHERE EmpID=?", salary, id);
        System.out.println("Record Updated");
    }

    public void delete(int id) {
        jdbcTemplate.update("DELETE FROM Employee WHERE EmpID=?", id);
        System.out.println("Record Deleted");
    }
}
```

### 3) `Main.java`
```java
import org.springframework.context.ApplicationContext;
import org.springframework.context.support.ClassPathXmlApplicationContext;

public class Main {
    public static void main(String[] args) {
        ApplicationContext ctx = new ClassPathXmlApplicationContext("applicationContext.xml");
        EmployeeDAO dao = (EmployeeDAO) ctx.getBean("employeeDAO");

        dao.insert(1, "Arjun", 45000);
        dao.update(1, 50000);
        dao.delete(1);
    }
}
```

### Output
```
Record Inserted
Record Updated
Record Deleted
```

---

## 15) Addition of Two Numbers Using HTML and JSP

**Question:**  
Write down the program in which input the two numbers in an HTML file and then display the addition in JSP file.

### `input.html`
```html
<!DOCTYPE html>
<html>
<head><title>Add Two Numbers</title></head>
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

### `add.jsp`
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

