# FirstSpringApp

Spring Boot REST API for basic student management with PostgreSQL persistence.

## Project purpose
This project is a CRUD backend used to manage students and practice core Spring concepts:
- REST controllers
- service layer
- JPA repositories
- PostgreSQL integration
- startup data seeding with `CommandLineRunner`

It exposes a simple API to create, read, update, and delete students.

## Tech stack
- Java 17
- Spring Boot 2.7
- Spring Web
- Spring Data JPA
- Spring Validation
- PostgreSQL
- Lombok
- Maven

## Domain model
`Student` fields:
- `id` (generated sequence)
- `name`
- `dob` (date of birth)
- `email`
- `age` (computed field, not persisted)

## API endpoints
Base path: `/api/v1/student`

- `GET /api/v1/student`  
  Returns all students.

- `GET /api/v1/student/{studentId}`  
  Returns one student by id.

- `POST /api/v1/student`  
  Creates a new student.

- `PUT /api/v1/student/{studentId}`  
  Replaces a student by id.

- `DELETE /api/v1/student/{studentId}`  
  Deletes a student by id.

## Local setup
### 1. Start PostgreSQL
The app is configured in `src/main/resources/application.properties` with:
- db: `student`
- user: `postgres`
- password: `docker`
- host: `localhost:5432`

Create DB if needed:

```sql
CREATE DATABASE student;
```

### 2. Run the application
From project root:

```bash
./mvnw spring-boot:run
```

Windows:

```powershell
.\mvnw.cmd spring-boot:run
```

### 3. Verify
```bash
curl http://localhost:8080/api/v1/student
```

## Example requests
Create:
```bash
curl -X POST http://localhost:8080/api/v1/student \
  -H "Content-Type: application/json" \
  -d "{\"name\":\"Mario Rossi\",\"dob\":\"2000-04-10\",\"email\":\"mario.rossi@example.com\"}"
```

Update:
```bash
curl -X PUT http://localhost:8080/api/v1/student/1 \
  -H "Content-Type: application/json" \
  -d "{\"name\":\"Mario Rossi Updated\",\"dob\":\"2000-04-10\",\"email\":\"mario.updated@example.com\"}"
```

Delete:
```bash
curl -X DELETE http://localhost:8080/api/v1/student/1
```

## Seed data
On startup, `StudentConfig` seeds initial sample students.

## Notes
- `spring.jpa.hibernate.ddl-auto=create-drop` recreates schema at startup and drops it at shutdown.
- This is useful for development/tests but not for production.
