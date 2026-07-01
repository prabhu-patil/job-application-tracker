# Job Application Tracker – Backend

Spring Boot backend for tracking job applications, interview stages, and outcomes with domain-level validation and status history.

## Core Features
- Create and manage job applications
- Application status lifecycle with enforced transitions
- Status history tracking for auditing
- Clean layered architecture (Controller, Service, Repository)
- Global exception handling

## Tech Stack
**Backend:** Java 17, Spring Boot, Spring Data JPA, Spring Security
**Database:** PostgreSQL
**Tools:** Maven, Postman, STS, GitHub

## Application Status Flow
```
APPLIED → SHORTLISTED → INTERVIEW → OFFERED
                            ↓
                         REJECTED
```

Invalid transitions are blocked at the domain level.

## API Overview
* **POST** /api/applications — Create a job application
* **PUT** /api/applications/{id}/status — Update application status
* **GET** /api/applications/user/{userId} — Get all applications for a user
* **GET** /api/applications/user/{userId}/status/{status} — Filter applications by status

## Project Architecture

```
/job-application-tracker
 ├── src/main/java
 │    ├── controller
 │    ├── service
 │    ├── service/impl
 │    ├── repository
 │    ├── entity
 │    ├── enums
 │    ├── dto
 │    ├── exception
 │    └── config
 ├── src/main/resources
 │    └── application.properties
 ├── pom.xml
```

## Running the Project

### Prerequisites
- Java 17+
- Maven 3.9+
- PostgreSQL (a database named `job_tracker_db`)

### 1. Clone
```bash
git clone https://github.com/prabhu-patil/job-application-tracker.git
cd job-application-tracker
```

### 2. Configure the database
Database settings are read from environment variables (with local-dev defaults in
`application.properties`). Override them for your own setup:

| Variable | Default | Description |
|----------|---------|-------------|
| `DB_URL` | `jdbc:postgresql://localhost:5432/job_tracker_db` | JDBC connection URL |
| `DB_USERNAME` | `postgres` | Database user |
| `DB_PASSWORD` | `changeme` | Database password |

```bash
# Example (Linux/macOS)
export DB_PASSWORD=your_password
```

### 3. Run
```bash
mvn spring-boot:run
```

### 4. Test the API
Use Postman or curl against the base URL:
```
http://localhost:8080
```
```bash
curl -X POST http://localhost:8080/api/applications \
  -H "Content-Type: application/json" \
  -d '{"userId": 1, "companyName": "Acme Corp", "role": "Backend Engineer"}'
```
## Highlights
- Domain-driven status transition validation
- Status history persistence
- Clean separation of concerns (Controller–Service–Repository)
- Transaction-safe service layer

## Author

Sangram Swain
