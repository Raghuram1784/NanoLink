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
