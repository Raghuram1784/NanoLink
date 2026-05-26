# 🔗 NanoLink - Premium URL Shortener

NanoLink is a high-performance, cloud-ready Spring Boot URL shortener wrapped in a stunning, ultra-premium **Sunset Gold & Charcoal Glassmorphism** user interface. It securely stores shortened URLs in a local MySQL database with automatic schema migrations, and falls back dynamically to in-memory configurations for immediate developer testing.

---

## ✨ Features & Visual Masterpieces

*   **Sunset Glassmorphism UI**: A gorgeous, warm charcoal gray backdrop (`#16161a`) overlaid with a semi-transparent card blur and custom golden borders.
*   **Floating Mesh Orbs & Light Particles**: Four slowly morphing background gradient orbs (saffron, gold, amber) layered with a gentle, floating stream of upward-drifting golden dust particles.
*   **Dynamic Stats Analytics**: Calculates and displays original vs. shortened URL character counts, and the exact percentage of database space saved in real time.
*   **Secure Dotenv Integration**: Local development credentials are kept safe in an ignored `.env` file and injected at run-time into Gradle tasks.
*   **Zero-Setup MySQL Execution**: Automatically checks for and creates the database schema (`createDatabaseIfNotExist=true`) on startup.
*   **Clickable Local Verification**: Automatically falls back to dynamic local request domains for 100% working, clickable links during testing.

---

## 🛠️ Technology Stack

*   **Java 21 (LTS)**: The modern foundation of the service.
*   **Spring Boot 4.0.1**: Core backend framework powering the MVC web layer.
*   **Spring Data JPA & Hibernate**: Object-relational mapping and schema management.
*   **MySQL**: Permanent production-ready relational database storage.
*   **H2 Database**: In-memory database used for zero-setup execution.
*   **Thymeleaf**: Server-side Java template engine rendering the interface.
*   **Gradle**: High-performance dependency management and build pipeline.
*   **Tabler Icons**: Sleek vector vector icon assets in the UI.

---


## 🚀 Getting Started (For Other Users)

To run NanoLink on your local computer, follow these simple setup steps:

### Prerequisites
*   **Java 21** installed.
*   **MySQL Server** installed and running on port `3306`.

### Step-by-Step Setup

1.  **Clone the Repository**
    ```bash
    git clone https://github.com/Raghuram1784/NanoLink.git
    cd NanoLink
    ```

2.  **Configure local secrets (`.env`)**
    Create a file named `.env` in the root directory of the project (at the same level as `build.gradle`).
    This file holds your sensitive MySQL credentials and is automatically ignored by Git. Add the following lines:
    ```env
    DB_USERNAME=root
    DB_PASSWORD=your_actual_mysql_root_password
    ```

3.  **Run the Server**
    Run the Gradle wrapper execution script. You don't need to manually create any databases in MySQL Workbench—Spring Boot will automatically check for and create the `urlshortener` database on startup!
    ```powershell
    # On Windows:
    .\gradlew.bat bootRun

    # On macOS / Linux:
    ./gradlew bootRun
    ```

4.  **Access the Application**
    Open your browser and navigate to:
    👉 **[http://localhost:8081](http://localhost:8081)**

---

## 🔄 Internal Architecture & Backend Flow

NanoLink follows a layered Spring Boot MVC architecture designed for scalability, maintainability, and clean separation of concerns.

```text
┌─────────────────────┐
│     User Browser    │
└──────────┬──────────┘
           │
           │ 1. User enters long URL
           ▼
┌─────────────────────┐
│   Thymeleaf UI      │
│  index.html/result  │
└──────────┬──────────┘
           │
           │ 2. HTTP Request
           ▼
┌─────────────────────┐
│   Controller Layer  │
│ Handles Web Routes  │
└──────────┬──────────┘
           │
           │ 3. Calls Business Logic
           ▼
┌─────────────────────┐
│    Service Layer    │
│ URL Generation Logic│
└──────────┬──────────┘
           │
           │ 4. Database Operations
           ▼
┌─────────────────────┐
│  Repository Layer   │
│ Spring Data JPA ORM │
└──────────┬──────────┘
           │
           │ 5. Persist Data
           ▼
┌─────────────────────┐
│  MySQL / H2 Database│
└─────────────────────┘
```

---

## 🧠 Complete URL Shortening Flow

```text
User submits long URL
        │
        ▼
Controller receives POST request
        │
        ▼
Service validates URL format
        │
        ▼
Generate unique short code
        │
        ▼
Check database for collisions
        │
        ▼
Create URL entity object
        │
        ▼
Save mapping into database
        │
        ▼
Return shortened URL to frontend
        │
        ▼
Thymeleaf renders result page
```

---

## 🔁 URL Redirection Flow

```text
User opens shortened URL
        │
        ▼
GET /{shortCode}
        │
        ▼
Controller extracts shortCode
        │
        ▼
Service searches database
        │
        ▼
Repository fetches original URL
        │
        ▼
Spring Boot returns HTTP redirect
        │
        ▼
Browser opens original website
```

---

## 🏗️ MVC Architecture

```text
Controller  →  Handles HTTP requests & routes
Service     →  Contains business logic
Repository  →  Manages database operations
Model       →  Represents application data
View        →  Thymeleaf frontend templates
```

### 📂 Project Structure

```text
controller/  → Request handling
service/     → URL shortening logic
repository/  → Database communication
entity/      → Database entities
model/       → Request/response models
templates/   → Thymeleaf UI pages
```

### 🖼️ View Layer

```text
index.html   → URL submission page
result.html  → Shortened URL result page
```

---

## 🗄️ Database Architecture

NanoLink uses relational database storage for persistent URL mapping.

```text
┌─────────────────────────────┐
│           url_table         │
├──────────────┬──────────────┤
│ id           │ Primary Key  │
│ originalUrl  │ Long URL     │
│ shortCode    │ Unique Code  │
│ createdAt    │ Timestamp    │
└──────────────┴──────────────┘
```

Example:

```text
id: 1
originalUrl: https://spring.io/projects/spring-boot
shortCode: nL92xA
createdAt: 2026-05-26
```

---

## ⚡ Spring Data JPA & Hibernate Flow

```text
Java Entity Object
        │
        ▼
Hibernate ORM Mapping
        │
        ▼
SQL Query Generation
        │
        ▼
MySQL Database Execution
```

Example:

```java
urlRepository.save(url);
```

Automatically becomes:

```sql
INSERT INTO urls (...)
```

without manually writing SQL queries.

---

## ☁️ Cloud-Ready Architecture

NanoLink follows Twelve-Factor App principles by separating configuration from application code.

```text
GitHub Repository
        │
        ▼
Cloud Provider (Render/Railway/AWS)
        │
        ▼
Environment Variables
        │
        ▼
Spring Boot Application
        │
        ▼
Hosted MySQL Database
```

Environment Variables Used:

```env
DB_USERNAME
DB_PASSWORD
SPRING_DATASOURCE_URL
APP_BASE_URL
```

---

## 🚀 Tech Stack Architecture

```text
Frontend:
Thymeleaf + HTML + CSS + Glassmorphism UI

Backend:
Java 21 + Spring Boot + MVC Architecture

Persistence:
Spring Data JPA + Hibernate ORM

Database:
MySQL / H2

Build Tool:
Gradle Wrapper

Deployment:
Render / Railway / Cloud Platforms
```
