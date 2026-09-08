# 🚀 Installation & Setup Guide

This guide explains how to clone, configure, and run the **AI Expense Manager** project on a new computer.

The project consists of two main parts:

* **Backend:** Spring Boot + Java
* **Frontend:** React + Vite

---

## 📋 Prerequisites

Before running the project, install the following software:

| Software    | Recommended Version                     |
| ----------- | --------------------------------------- |
| Java / JDK  | **21**                                  |
| Spring Boot | **3.5.4**                               |
| Node.js     | **24.x**                                |
| npm         | Comes with Node.js                      |
| Maven       | **3.9.x**                               |
| MySQL       | **8.x or compatible**                   |
| Git         | Latest version                          |
| IDE         | IntelliJ IDEA / STS / Eclipse / VS Code |

> **Important:** The project is developed and configured using **JDK 21**. JDK 21 is recommended for the most predictable results.

---

# 1. 📥 Clone the Repository

Open a terminal or PowerShell and run:

```bash
git clone https://github.com/Debastab0-2107/AI-EXPENSE-MANAGER.git
```

Move into the project directory:

```bash
cd AI-EXPENSE-MANAGER
```

The project structure should look approximately like:

```text
AI-EXPENSE-MANAGER/
│
├── cashcompass-frontend/
│
├── expense-manager-backend/
│
├── .gitignore
│
└── README.md
```

---

# 2. ⚠️ Do NOT Create a New Spring Boot Project

You **do not need to create a new project using Spring Initializr**.

The Spring Boot backend is already included in:

```text
expense-manager-backend/
```

It already contains:

```text
pom.xml
mvnw
mvnw.cmd
src/
```

The `pom.xml` file contains the dependencies required by the project.

Therefore, you should simply open the existing:

```text
expense-manager-backend/
```

project in your IDE.

---

# 3. 📦 Backend Dependencies

The backend uses Maven for dependency management.

The required dependencies are already defined in:

```text
expense-manager-backend/pom.xml
```

The project includes technologies such as:

* Spring Boot
* Spring Web
* Spring Data JPA
* Spring Security
* JWT
* Java Mail Sender
* MySQL Connector
* Lombok
* Bean Validation
* PDF generation
* Playwright
* Spring Boot Testing

You **do not need to manually download these libraries or JAR files**.

Maven automatically downloads the required dependencies when the project is built.

The dependency flow is:

```text
pom.xml
    ↓
Maven
    ↓
Downloads dependencies
    ↓
Spring Security
JWT
Lombok
JPA
Java Mail
MySQL Driver
etc.
```

---

# 4. ☕ Configure Java / JDK

This project is configured for:

```text
JDK 21
```

The Java version is specified in the `pom.xml`.

Therefore, make sure Java 21 is installed.

Check your Java version:

```bash
java -version
```

You should see something similar to:

```text
java version "21.x.x"
```

You can also check the Java compiler:

```bash
javac -version
```

Expected:

```text
javac 21.x.x
```

### What if you have JDK 25?

A newer JDK may be capable of running code targeting Java 21, but **JDK 21 is the recommended version for this project** because that is the version against which the project is configured and tested.

For maximum compatibility, use:

```text
JDK 21
```

---

# 5. 🗄️ Configure MySQL

The backend uses MySQL as its database.

Make sure MySQL Server is installed and running.

Create the required database using MySQL:

```sql
CREATE DATABASE cashcompass;
```

> If the database name in your local configuration is different, use the same database name specified in `application.properties`.

---

# 6. 🔐 Configure `application.properties`

### Important Security Information

The actual:

```text
application.properties
```

file is intentionally excluded from GitHub using `.gitignore`.

This is done because it may contain sensitive information such as:

* Database username
* Database password
* Email credentials
* JWT secret
* API keys
* Other private configuration

Therefore, after cloning the project, you must create your own:

```text
application.properties
```

inside:

```text
expense-manager-backend/
└── src/
    └── main/
        └── resources/
            └── application.properties
```

---

# 7. 📝 Example Configuration

Use your own credentials and configuration values.

A typical configuration may look like:

```properties
# ===============================
# DATABASE CONFIGURATION
# ===============================

spring.datasource.url=jdbc:mysql://localhost:3306/cashcompass
spring.datasource.username=YOUR_MYSQL_USERNAME
spring.datasource.password=YOUR_MYSQL_PASSWORD

spring.jpa.hibernate.ddl-auto=update


# ===============================
# EMAIL CONFIGURATION
# ===============================

spring.mail.host=smtp.gmail.com
spring.mail.port=587
spring.mail.username=YOUR_EMAIL
spring.mail.password=YOUR_EMAIL_APP_PASSWORD


# ===============================
# JWT CONFIGURATION
# ===============================

jwt.secret=YOUR_JWT_SECRET


# ===============================
# OTHER API CONFIGURATION
# ===============================

# Add the API keys required by the project
# Example:
# gemini.api.key=YOUR_API_KEY
```

> **Never commit real passwords, API keys, JWT secrets, or email credentials to GitHub.**

---

# 8. 📧 Email Configuration

The project uses **Java Mail / Spring Boot Mail** for email functionality.

The dependency is already included in:

```text
pom.xml
```

However, Maven only provides the Java library.

It does **not** provide an email account.

Therefore, every developer must configure their own email credentials.

For example:

```properties
spring.mail.username=YOUR_EMAIL
spring.mail.password=YOUR_APP_PASSWORD
```

If Gmail is used, an **App Password** may be required depending on the account's security configuration.

---

# 9. 🔑 JWT Configuration

The project uses JWT for authentication.

The JWT library is already defined in:

```text
pom.xml
```

Therefore, no manual JWT installation is required.

However, the JWT secret must be configured locally.

For example:

```properties
jwt.secret=YOUR_JWT_SECRET
```

Use a secure secret and do not upload it to GitHub.

---

# 10. 🤖 AI / API Configuration

If the project uses an external AI/API service, the required API key must be configured locally.

For example:

```properties
gemini.api.key=YOUR_API_KEY
```

> Replace the property name with the exact property used by the project.

Never upload a real API key to GitHub.

---

# 11. ▶️ Run the Backend

Open a terminal inside:

```text
expense-manager-backend/
```

### Windows

The project includes the Maven Wrapper, so Maven does not necessarily need to be installed globally.

Run:

```powershell
.\mvnw.cmd spring-boot:run
```

### Linux / macOS

Run:

```bash
./mvnw spring-boot:run
```

Alternatively, if Maven is installed globally:

```bash
mvn spring-boot:run
```

Maven will:

```text
Read pom.xml
      ↓
Download dependencies
      ↓
Compile the project
      ↓
Process Lombok annotations
      ↓
Build the Spring Boot application
      ↓
Start the backend server
```

---

# 12. 🧩 Why You Don't Need to Install Lombok Manually

Lombok is already defined in:

```text
pom.xml
```

Therefore Maven handles the dependency.

For example, classes may use annotations such as:

```java
@Getter
@Setter
@Builder
@NoArgsConstructor
@AllArgsConstructor
```

Maven will download and process Lombok as part of the project build.

If your IDE displays Lombok-related errors, make sure annotation processing/Lombok support is enabled in the IDE.

---

# 13. 🔒 Why You Don't Need to Install Spring Security Manually

Spring Security is already included as a Maven dependency.

Therefore:

```text
Spring Security
       ↓
pom.xml
       ↓
Maven
       ↓
Automatically downloaded
```

There is no need to manually download a Spring Security JAR.

The same principle applies to:

* JWT
* Spring Data JPA
* Spring Mail
* MySQL Connector
* Validation
* Other Maven dependencies

---

# 14. 🌐 Frontend Setup

The frontend is located inside:

```text
cashcompass-frontend/
```

Move into the frontend directory:

```bash
cd cashcompass-frontend
```

Install the required Node.js dependencies:

```bash
npm install
```

`npm install` reads:

```text
package.json
```

and downloads the required frontend packages.

You do **not** need to manually install React, Vite, React Router, etc.

---

# 15. ▶️ Run the Frontend

After installing the dependencies:

```bash
npm run dev
```

Vite will start the development server.

The terminal will display the local URL, usually something similar to:

```text
http://localhost:5173
```

Open the displayed URL in your browser.

---

# 16. 🔄 Complete Application Flow

Once both the frontend and backend are running, the application works approximately like this:

```text
                 USER
                  │
                  ↓
          React Frontend
                  │
                  │ HTTP Requests
                  ↓
        Spring Boot Backend
                  │
                  ↓
          Spring Security
                  │
                  ↓
              JWT Auth
                  │
                  ↓
          Service Layer
                  │
                  ↓
           JPA / Hibernate
                  │
                  ↓
              MySQL
```

For email functionality:

```text
Spring Boot
     ↓
Spring Mail
     ↓
Email Provider
     ↓
User's Email
```

For AI functionality:

```text
Spring Boot
     ↓
AI API
     ↓
AI Response
     ↓
Application
```

---

# 17. 🛠️ Complete Setup in Short

For a new developer, the complete process is:

```text
1. Install JDK 21
        ↓
2. Install Node.js 24.x
        ↓
3. Install MySQL
        ↓
4. Install Git
        ↓
5. Clone the repository
        ↓
6. Open the existing project
        ↓
7. Configure MySQL
        ↓
8. Create application.properties
        ↓
9. Add personal credentials/API keys
        ↓
10. Start Spring Boot backend
        ↓
11. Run npm install
        ↓
12. Start React frontend
        ↓
13. Open the application in browser
```

---

# 18. ❌ Things You DON'T Need to Do

After cloning the repository, you **do not** need to:

* ❌ Create a new Spring Boot project
* ❌ Recreate the project using Spring Initializr
* ❌ Manually install Spring Security
* ❌ Manually download JWT JAR files
* ❌ Manually download Lombok JAR files
* ❌ Manually download Spring Mail
* ❌ Manually download the MySQL JDBC driver
* ❌ Recreate the Java package structure
* ❌ Copy Java classes manually

Maven handles the Java dependencies through:

```text
pom.xml
```

Similarly, npm handles frontend dependencies through:

```text
package.json
```

---

# 19. 📁 Important Project Files

| File / Directory           | Purpose                                                 |
| -------------------------- | ------------------------------------------------------- |
| `expense-manager-backend/` | Spring Boot backend                                     |
| `cashcompass-frontend/`    | React frontend                                          |
| `pom.xml`                  | Backend dependencies and Maven configuration            |
| `mvnw`                     | Maven Wrapper for Linux/macOS                           |
| `mvnw.cmd`                 | Maven Wrapper for Windows                               |
| `package.json`             | Frontend dependencies and scripts                       |
| `.gitignore`               | Prevents unnecessary/private files from being committed |
| `application.properties`   | Local application configuration and secrets             |

---

# 20. 🔐 Security Best Practices

Never commit the following information to GitHub:

```text
Database passwords
Email passwords
Email App Passwords
JWT secrets
API keys
Access tokens
Private credentials
```

Keep sensitive configuration inside:

```text
application.properties
```

and/or environment variables.

Make sure sensitive files are included in `.gitignore`.

---

# 21. 💡 Recommended Repository Improvement

For easier setup by other developers, consider adding:

```text
application-example.properties
```

to the repository.

For example:

```text
src/main/resources/
│
├── application-example.properties
└── application.properties
```

The example file should contain placeholders:

```properties
spring.datasource.username=YOUR_USERNAME
spring.datasource.password=YOUR_PASSWORD

spring.mail.username=YOUR_EMAIL
spring.mail.password=YOUR_APP_PASSWORD

jwt.secret=YOUR_SECRET

gemini.api.key=YOUR_API_KEY
```

This allows developers to understand exactly which configuration values are required without exposing your actual secrets.

---

# 22. 🧠 Understanding the Architecture

The project can be thought of as three separate requirements:

### 1. Project Dependencies

Handled automatically by:

```text
pom.xml
```

Examples:

```text
Spring Security
JWT
Lombok
JPA
Spring Mail
MySQL Driver
```

### 2. Frontend Dependencies

Handled automatically by:

```text
package.json
```

and:

```bash
npm install
```

### 3. Local Environment & Secrets

Provided by the developer:

```text
JDK 21
MySQL
Database credentials
Email credentials
JWT secret
API keys
```

The repository provides the **application**, while each developer provides their own **local environment and private credentials**.

---

# 23. ✅ Final Checklist

Before running the project, verify:

```text
[ ] Git installed
[ ] JDK 21 installed
[ ] Node.js 24.x installed
[ ] npm installed
[ ] MySQL installed and running
[ ] Repository cloned
[ ] Backend opened
[ ] application.properties created
[ ] Database created
[ ] Database credentials configured
[ ] Email credentials configured
[ ] JWT secret configured
[ ] Required API keys configured
[ ] Backend started successfully
[ ] npm install completed
[ ] Frontend started successfully
```

Once everything is configured:

```text
Frontend
   │
   ↓
React + Vite
   │
   ↓
Spring Boot REST API
   │
   ↓
Spring Security + JWT
   │
   ↓
JPA / Hibernate
   │
   ↓
MySQL
```

🎉 **The AI Expense Manager is ready to use!**
