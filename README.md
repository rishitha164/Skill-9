# Experiment 9 – Global Exception Handling using @ControllerAdvice

## Overview
This Spring Boot project demonstrates centralized exception handling using `@ControllerAdvice` and `@ExceptionHandler`.

## Project Structure
```
src/main/java/com/experiment/globalexception/
├── GlobalExceptionApplication.java       # Main entry point
├── controller/
│   └── StudentController.java            # REST endpoints
├── exception/
│   ├── StudentNotFoundException.java     # Custom 404 exception
│   └── InvalidInputException.java        # Custom 400 exception
├── handler/
│   └── GlobalExceptionHandler.java       # @ControllerAdvice handler
├── model/
│   └── Student.java                      # Student model
└── dto/
    └── ErrorResponse.java                # Structured JSON error response
```

## How to Run
```bash
mvn spring-boot:run
```
The server starts at: `http://localhost:8080`

---

## API Endpoints & Postman Tests

### ✅ 1. Get All Students (Valid)
- **GET** `http://localhost:8080/api/students`
- **Expected:** `200 OK` with list of students

### ✅ 2. Get Student by Valid ID
- **GET** `http://localhost:8080/api/student/1`
- **Expected:** `200 OK`
```json
{
  "id": 1,
  "name": "Alice Johnson",
  "email": "alice@example.com",
  "age": 20
}
```

### ❌ 3. Get Student – Not Found (StudentNotFoundException)
- **GET** `http://localhost:8080/api/student/99`
- **Expected:** `404 Not Found`
```json
{
  "status": 404,
  "error": "Not Found",
  "message": "Student not found with ID: 99",
  "path": "/api/student/99",
  "timestamp": "2024-01-01T10:00:00"
}
```

### ❌ 4. Get Student – Invalid ID (InvalidInputException)
- **GET** `http://localhost:8080/api/student/-5`
- **Expected:** `400 Bad Request`
```json
{
  "status": 400,
  "error": "Bad Request",
  "message": "Student ID must be a positive integer.",
  "path": "/api/student/-5",
  "timestamp": "2024-01-01T10:00:00",
  "details": ["Field: id", "Rejected value: -5"]
}
```

### ❌ 5. Get Student – Type Mismatch
- **GET** `http://localhost:8080/api/student/abc`
- **Expected:** `400 Bad Request`
```json
{
  "status": 400,
  "error": "Type Mismatch",
  "message": "Parameter 'id' should be of type 'int' but received: 'abc'",
  "path": "/api/student/abc",
  "timestamp": "2024-01-01T10:00:00"
}
```

### ✅ 6. Add Student (Valid POST)
- **POST** `http://localhost:8080/api/student`
- **Body (JSON):**
```json
{
  "name": "David Lee",
  "email": "david@example.com",
  "age": 23
}
```
- **Expected:** `201 Created`

### ❌ 7. Add Student – Invalid Age (InvalidInputException)
- **POST** `http://localhost:8080/api/student`
- **Body:**
```json
{
  "name": "Eve",
  "email": "eve@example.com",
  "age": 200
}
```
- **Expected:** `400 Bad Request`

---

## Key Concepts
| Annotation | Purpose |
|---|---|
| `@ControllerAdvice` | Marks class as global exception handler |
| `@ExceptionHandler` | Maps specific exceptions to handler methods |
| `ResponseEntity<ErrorResponse>` | Returns structured JSON with HTTP status |
| Custom Exception classes | Carry meaningful error context |

## GitHub
Push to GitHub:
```bash
git init
git add .
git commit -m "Experiment 9: Global Exception Handling with @ControllerAdvice"
git remote add origin <your-repo-url>
git push -u origin main
```
"# Skill-9" 
