# 🚀 Getting Started

## 1. Clone the Repository

```bash
git clone https://github.com/Debastab0-2107/AI-EXPENSE-MANAGER.git
```

Move into the project:

```bash
cd AI-EXPENSE-MANAGER
```

---

# 🗄️ Backend Setup

Move into the backend directory:

```bash
cd expense-manager-backend
```

## 2. Create the MySQL Database

Open MySQL and create the database:

```sql
CREATE DATABASE expense_manager;
```

The backend is configured to connect to:

```text
localhost:3306/expense_manager
```

---

# 🔑 3. Configure `application.properties`

The repository contains:

```text
expense-manager-backend/
└── src/
    └── main/
        └── resources/
            ├── application.properties
            └── application-example.properties
```

### ⚠️ Important

`application-example.properties` is provided as a **template/example**.

It shows the structure and configuration required to run the backend, but it does **not** contain your actual passwords, secrets, email credentials, or API keys.

The example file contains placeholders such as:

```properties
spring.datasource.username=YOUR_DATABASE_USERNAME
spring.datasource.password=YOUR_DATABASE_PASSWORD

spring.mail.username=YOUR_EMAIL
spring.mail.password=YOUR_EMAIL_APP_PASSWORD

jwt.secret=YOUR_JWT_SECRET

gemini.api.key=${GEMINI_API_KEY}
```

These values must be replaced with your own configuration.

---

## 📝 4. Configure the Backend

Open:

```text
expense-manager-backend/src/main/resources/application.properties
```

You can use:

```text
application-example.properties
```

as the reference for the required configuration structure.

Configure the following:

### MySQL

```properties
spring.datasource.url=jdbc:mysql://localhost:3306/expense_manager
spring.datasource.username=YOUR_DATABASE_USERNAME
spring.datasource.password=YOUR_DATABASE_PASSWORD
```

### Email / OTP

The application uses Gmail SMTP for email-related functionality.

```properties
spring.mail.host=smtp.gmail.com
spring.mail.port=587
spring.mail.username=YOUR_EMAIL
spring.mail.password=YOUR_EMAIL_APP_PASSWORD
```

> For Gmail, use a **Google App Password**, not your normal Gmail account password.

### JWT

Configure your own secret:

```properties
jwt.secret=YOUR_JWT_SECRET
jwt.expiration=86400000
```

### Gemini AI

Configure your Gemini API key:

```properties
gemini.api.key=${GEMINI_API_KEY}
gemini.api.model=gemini-3.6-flash
```

Then provide the `GEMINI_API_KEY` environment variable with your actual API key.

---

# 🔒 Security Note

**Never commit real secrets to GitHub.**

Do not upload:

* Database passwords
* Gmail passwords
* Gmail App Passwords
* JWT secrets
* Gemini API keys
* Other private credentials

The repository intentionally provides:

```text
application-example.properties
```

so that developers can understand the required configuration without exposing sensitive information.

---

# ▶️ 5. Run the Backend

From:

```text
expense-manager-backend
```

Windows:

```bash
mvnw.cmd spring-boot:run
```

or, if Maven is installed:

```bash
mvn spring-boot:run
```

The backend runs on:

```text
http://localhost:8080
```

---

# 💻 Frontend Setup

Open another terminal.

From the project root:

```bash
cd cashcompass-frontend
```

Install dependencies:

```bash
npm install
```

Start the development server:

```bash
npm run dev
```

The frontend will normally be available at:

```text
http://localhost:5173
```

---

# 🔄 Application Architecture

The overall application follows this architecture:

```text
                    ┌─────────────────────┐
                    │       User          │
                    └──────────┬──────────┘
                               │
                               ▼
                    ┌─────────────────────┐
                    │   React Frontend    │
                    │      Vite            │
                    │   localhost:5173    │
                    └──────────┬──────────┘
                               │
                         REST API / HTTP
                               │
                               ▼
                    ┌─────────────────────┐
                    │   Spring Boot       │
                    │      Backend        │
                    │   localhost:8080    │
                    └──────────┬──────────┘
                               │
              ┌────────────────┼────────────────┐
              │                │                │
              ▼                ▼                ▼
       ┌────────────┐   ┌────────────┐   ┌────────────┐
       │   Spring   │   │   MySQL    │   │  Gemini AI │
       │  Security  │   │  Database  │   │    API     │
       └────────────┘   └────────────┘   └────────────┘
              │
              ▼
       ┌────────────┐
       │    JWT     │
       │Authentication│
       └────────────┘
```

---

# 🔄 Backend Request Flow

A typical request follows this flow:

```text
React Frontend
      │
      ▼
HTTP Request
      │
      ▼
Spring Boot Controller
      │
      ▼
DTO / Validation
      │
      ▼
Service
      │
      ▼
Repository
      │
      ▼
MySQL Database
      │
      ▼
Repository
      │
      ▼
Service
      │
      ▼
Controller
      │
      ▼
JSON Response
      │
      ▼
React Frontend
```

For protected requests, Spring Security and JWT authentication are involved before the request reaches the application logic.

---

# 🧩 Backend Architecture

The backend follows a layered architecture.

### Controller

Handles incoming HTTP requests and exposes REST API endpoints.

```text
Client → Controller
```

### DTO

Data Transfer Objects are used to transfer structured data between the frontend and backend.

```text
Request/Response Data → DTO
```

### Entity

Represents database tables and their relationships.

```text
Entity → Database Table
```

### Repository

Handles database operations using Spring Data JPA.

```text
Service → Repository → Database
```

### Service

Contains the application's business logic.

```text
Controller → Service
```

### ServiceImpl

Provides the concrete implementation of the service interfaces.

```text
Service Interface
       ↓
ServiceImpl
       ↓
Repository
```

---

# 🤖 AI Processing Flow

When AI financial insights are requested:

```text
User
 │
 ▼
React Frontend
 │
 ▼
Spring Boot REST API
 │
 ▼
Financial Data
 │
 ▼
AI Service
 │
 ▼
Google Gemini API
 │
 ▼
AI Financial Analysis
 │
 ▼
Spring Boot
 │
 ▼
React Dashboard
```

The AI can analyze financial information and generate summaries, observations, recommendations, and warnings.

---

# 📄 PDF Report Flow

```text
User requests report
        │
        ▼
React Frontend
        │
        ▼
Spring Boot Backend
        │
        ▼
Collect financial data
        │
        ▼
Generate report
        │
        ▼
HTML / CSS / PDF processing
        │
        ▼
PDF File
        │
        ▼
Download by User
```

---

# 🌐 Default Ports

| Application         |   Port |
| ------------------- | -----: |
| React Frontend      | `5173` |
| Spring Boot Backend | `8080` |
| MySQL               | `3306` |

---

# 🧪 Development

For development, run the two parts separately.

### Terminal 1 — Backend

```bash
cd expense-manager-backend
mvnw.cmd spring-boot:run
```

### Terminal 2 — Frontend

```bash
cd cashcompass-frontend
npm install
npm run dev
```

Then open:

```text
http://localhost:5173
```

---

# 🔐 Environment & Secrets

Sensitive configuration should remain outside version control.

Recommended approach:

```text
application-example.properties
        │
        │  copy structure
        ▼
application.properties
        │
        ├── Database credentials
        ├── Email credentials
        ├── JWT secret
        └── Gemini API configuration
```

Only the example/template configuration should be shared publicly.

---

# 📌 Important Configuration Files

| File                             | Purpose                                              |
| -------------------------------- | ---------------------------------------------------- |
| `application.properties`         | Local backend configuration                          |
| `application-example.properties` | Safe configuration template                          |
| `pom.xml`                        | Backend dependencies and Maven configuration         |
| `package.json`                   | Frontend dependencies and scripts                    |
| `.gitignore`                     | Prevents unwanted/private files from being committed |

---

# 🛡️ Security Recommendations

Before pushing or deploying the application:

* Never expose API keys.
* Never commit database passwords.
* Never commit email App Passwords.
* Use strong JWT secrets.
* Keep `application.properties` out of public repositories when it contains real credentials.
* Use environment variables for production secrets.
* Rotate any credential immediately if it is accidentally exposed.

---

# 🚀 Future Improvements

Possible future enhancements include:

* 📱 Mobile application
* 🔔 Financial notifications
* 📊 More advanced analytics
* 💡 Improved AI financial recommendations
* ☁️ Cloud deployment
* 🔄 Automated backups
* 👥 Shared/family expense management
* 📈 Advanced financial forecasting

---

# 👨‍💻 Author

**Debastab Das**

GitHub:
https://github.com/Debastab0-2107

Project Repository:
https://github.com/Debastab0-2107/AI-EXPENSE-MANAGER

---

# 📜 License

This project is developed for educational and project purposes.

---

## ⭐ If you find this project useful

Consider giving the repository a ⭐ on GitHub!

**CashCompass — Directing your money, daily.**
