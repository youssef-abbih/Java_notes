# Java Database Connections

## Introduction to Database Connections

Connecting to a database is a fundamental part of many applications. It involves setting up a connection between your Java application and a database to execute SQL queries, retrieve data, and perform other database operations.

## JDBC (Java Database Connectivity)

JDBC is a Java API that allows Java programs to connect to a database and execute SQL statements. JDBC is part of the Java Standard Edition platform, from Oracle Corporation.

### JDBC Architecture

The JDBC architecture consists of two main layers:

1. **JDBC API**: Provides the application-to-JDBC Manager connection.
2. **JDBC Driver API**: Supports the JDBC Manager-to-Driver Connection.

### Steps to Connect to a Database using JDBC

1. **Load the JDBC driver**
2. **Establish a connection**
3. **Create a statement**
4. **Execute the query**
5. **Process the result**
6. **Close the connection**

### Loading the JDBC Driver

Different databases require different JDBC drivers. You can load a driver using:

```java
Class.forName("com.mysql.cj.jdbc.Driver");
```

### Establishing a Connection

You establish a connection using the `DriverManager` class:

```java
Connection conn = DriverManager.getConnection(url, user, password);
```

**Example:**

```java
String url = "jdbc:mysql://localhost:3306/mydatabase";
String user = "root";
String password = "password";

Connection conn = DriverManager.getConnection(url, user, password);
```

### Creating a Statement

#### What is a Statement?

A Statement object is used for executing a static SQL statement and obtaining the results produced by it. There are three types of statements in JDBC:

1. **Statement:** Used for executing simple SQL queries without parameters.
2. **PreparedStatement:** Used for executing precompiled SQL queries with or without input parameters.
3. **CallableStatement:** Used for executing stored procedures in the database.

#### Why Do We Need to Create a Statement?

1. **Executing SQL Queries:** A Statement object provides methods to send SQL queries to the database and receive results. This is fundamental for performing CRUD (Create, Read, Update, Delete) operations on the database.

2. **Managing SQL Execution:** It allows the application to control how SQL queries are executed. For example, you can choose to execute a query as a batch, set fetch sizes, or manage timeouts.

3. **Receiving Results:** The Statement object can return the result of a query in the form of a ResultSet object, which provides methods to iterate over the returned data.

4. **Preventing SQL Injection:** While the basic Statement interface is vulnerable to SQL injection attacks, using PreparedStatement helps prevent SQL injection by parameterizing queries.

#### Types of statements

+ **Statement:** Basic interface for executing simple SQL queries without parameters.
+ **PreparedStatement:** Used for precompiled SQL queries with parameters, offering better performance and security.
+ **CallableStatement:** Used for executing stored procedures in the database.

Once the connection is established, you can create a statement object to execute SQL queries:

```java
Statement stmt = conn.createStatement();
```

### Executing a Query

You can execute SQL queries using the statement object:

```java
ResultSet rs = stmt.executeQuery("SELECT * FROM users");
```

### Processing the Result

The `ResultSet` object contains the results of the query, which you can process as follows:

```java
while (rs.next()) {
    int id = rs.getInt("id");
    String name = rs.getString("name");
    System.out.println("ID: " + id + ", Name: " + name);
}
```

### Closing the Connection

Finally, it's important to close the connection to free up database resources:

```java
rs.close();
stmt.close();
conn.close();
```

### Complete Example

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.Statement;

public class Main {
    public static void main(String[] args) {
        String url = "jdbc:mysql://localhost:3306/mydatabase";
        String user = "root";
        String password = "password";

        try {
            Class.forName("com.mysql.cj.jdbc.Driver");
            Connection conn = DriverManager.getConnection(url, user, password);
            Statement stmt = conn.createStatement();
            ResultSet rs = stmt.executeQuery("SELECT * FROM users");

            while (rs.next()) {
                int id = rs.getInt("id");
                String name = rs.getString("name");
                System.out.println("ID: " + id + ", Name: " + name);
            }

            rs.close();
            stmt.close();
            conn.close();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

## PreparedStatement

`PreparedStatement` is used to execute parameterized queries, which helps prevent SQL injection attacks and can improve performance.

**Example:**

```java
String query = "SELECT * FROM users WHERE id = ?";
PreparedStatement pstmt = conn.prepareStatement(query);
pstmt.setInt(1, 1);
ResultSet rs = pstmt.executeQuery();

while (rs.next()) {
    int id = rs.getInt("id");
    String name = rs.getString("name");
    System.out.println("ID: " + id + ", Name: " + name);
}

rs.close();
pstmt.close();
conn.close();
```

## CallableStatement

`CallableStatement` is used to execute stored procedures in the database.

**Example:**

```java
CallableStatement cstmt = conn.prepareCall("{call getUserById(?)}");
cstmt.setInt(1, 1);
ResultSet rs = cstmt.executeQuery();

while (rs.next()) {
    int id = rs.getInt("id");
    String name = rs.getString("name");
    System.out.println("ID: " + id + ", Name: " + name);
}

rs.close();
cstmt.close();
conn.close();
```

## Transaction Management

JDBC allows you to manage transactions manually by setting auto-commit to false.

**Example:**

```java
conn.setAutoCommit(false);

try {
    Statement stmt = conn.createStatement();
    stmt.executeUpdate("UPDATE users SET balance = balance - 100 WHERE id = 1");
    stmt.executeUpdate("UPDATE users SET balance = balance + 100 WHERE id = 2");
    conn.commit();
} catch (Exception e) {
    conn.rollback();
    e.printStackTrace();
}

conn.setAutoCommit(true);
stmt.close();
conn.close();
```

## Connection Pooling

Connection pooling is a technique used to improve the performance of executing commands on a database. A pool of connections is maintained and reused, reducing the overhead of creating new connections.

**Example using HikariCP:**

```xml
<!-- pom.xml for Maven users -->
<dependency>
    <groupId>com.zaxxer</groupId>
    <artifactId>HikariCP</artifactId>
    <version>3.4.5</version>
</dependency>
```

**Example:**

```java
import com.zaxxer.hikari.HikariConfig;
import com.zaxxer.hikari.HikariDataSource;

import java.sql.Connection;
import java.sql.ResultSet;
import java.sql.Statement;

public class Main {
    public static void main(String[] args) {
        HikariConfig config = new HikariConfig();
        config.setJdbcUrl("jdbc:mysql://localhost:3306/mydatabase");
        config.setUsername("root");
        config.setPassword("password");

        HikariDataSource dataSource = new HikariDataSource(config);

        try (Connection conn = dataSource.getConnection();
             Statement stmt = conn.createStatement();
             ResultSet rs = stmt.executeQuery("SELECT * FROM users")) {

            while (rs.next()) {
                int id = rs.getInt("id");
                String name = rs.getString("name");
                System.out.println("ID: " + id + ", Name: " + name);
            }
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

## Conclusion

Understanding JDBC and database connections in Java is essential for developing robust, efficient, and secure database-driven applications. By utilizing the JDBC API and best practices such as using `PreparedStatement`, managing transactions, and implementing connection pooling, you can ensure your applications perform well and are secure against common vulnerabilities.
