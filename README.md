# Spring Boot Thymeleaf CRUD Pagination Sorting WebApp

Spring Boot CRUD Web application with Pagination and Sorting features using Spring Boot, ThymeLeaf, Spring Data JPA, Hibernate, and Azure SQL Database.

## Steps To Configure The Database With Azure

### 1. Create an Azure SQL Database
```bash
# Go to Azure Portal → Search for SQL Database → Click Create.
# Select a Resource Group (or create a new one).
# Set the Database Name
Database Name: springboot1

# Create a New Server:
Server Name: springboot-app
Location: Choose a region near you.
Authentication: Username: admin@123 and a strong password.
```
Click **OK**.

```bash
# Select Compute + Storage
# For development, use a lower-tier like Basic or Standard.
# Networking → Choose Public Endpoint → Allow access.
# Review + Create → Click Create.
```

### 2. Configure Firewall Rules
```bash
# Go to the newly created database → Click Set Firewall Rules.
# Allow Azure Services: Click ON.
# Add Your IP Address: Click Add Client IP.
# Click Save.
```

### 3. Get the Connection String
```bash
# Go to the SQL database resource.
# Navigate to Connection Strings → Copy the JDBC connection string:
jdbc:sqlserver://springboot-app.database.windows.net:1433;database=springboot1;user=admin@123@springboot-app;password={your_password_here};encrypt=true;trustServerCertificate=false;hostNameInCertificate=*.database.windows.net;loginTimeout=30;
```

### 4. Update `application.properties` in Spring Boot
Replace MySQL settings with Azure SQL Server:

```properties
spring.datasource.url=jdbc:sqlserver://springboot-app.database.windows.net:1433;database=springboot1;encrypt=true;trustServerCertificate=false;
spring.datasource.username=admin@123
spring.datasource.password=Your_Password_Here
spring.datasource.driver-class-name=com.microsoft.sqlserver.jdbc.SQLServerDriver
spring.jpa.database-platform=org.hibernate.dialect.SQLServerDialect
```

### 5. Add SQL Server Dependencies in `pom.xml`
Remove MySQL and add Microsoft SQL Server JDBC driver:

```xml
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <scope>runtime</scope>
</dependency>
```

### 6. Run the Application
```bash
# Build and Run the Spring Boot Application
mvn spring-boot:run
