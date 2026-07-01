# 2. REST API: Layers, DTO, Validation & Exception Handling

> 🟡 **Level:** Intermediate | 🔥 **Interview Frequency:** Very High

---

## 🧠 Concept

A **REST API** lets clients talk to your backend over HTTP using standard methods
(GET, POST, PUT, DELETE) and JSON. Spring Boot organizes it in clean **layers**.

---

## 🗺️ The Layers

```
Controller  →  Service  →  Repository  →  Database
 (HTTP)        (logic)      (data)
   ▲
  DTO (in/out)      Entity (DB table)     Mapper (Entity ↔ DTO)
```

| Layer | Annotation | Job |
|-------|-----------|-----|
| **Controller** | `@RestController` | Receive HTTP requests, return responses |
| **Service** | `@Service` | Business logic |
| **Repository** | `@Repository` | Talk to the database |
| **Entity** | `@Entity` | Maps to a DB table |
| **DTO** | plain class | Data sent/received (no DB details) |
| **Mapper** | class/MapStruct | Convert Entity ↔ DTO |

---

## 🧩 HTTP Methods (REST)

| Method | Use | Example |
|--------|-----|---------|
| GET | Read | `GET /users/1` |
| POST | Create | `POST /users` |
| PUT | Update (full) | `PUT /users/1` |
| PATCH | Update (partial) | `PATCH /users/1` |
| DELETE | Delete | `DELETE /users/1` |

---

## 🧩 Example — Full Flow

```java
// ENTITY
@Entity
public class User {
    @Id @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    private String name;
    private String email;
}

// DTO (what the client sees/sends — no internal fields)
public record UserDTO(Long id, String name, String email) {}

// REPOSITORY
public interface UserRepository extends JpaRepository<User, Long> {}

// SERVICE
@Service
public class UserService {
    private final UserRepository repo;
    public UserService(UserRepository repo) { this.repo = repo; }

    public User create(User u) { return repo.save(u); }
    public User get(Long id) {
        return repo.findById(id)
                   .orElseThrow(() -> new ResourceNotFoundException("User not found"));
    }
}

// CONTROLLER
@RestController
@RequestMapping("/api/users")
public class UserController {
    private final UserService service;
    public UserController(UserService service) { this.service = service; }

    @GetMapping("/{id}")
    public ResponseEntity<User> get(@PathVariable Long id) {
        return ResponseEntity.ok(service.get(id));
    }

    @PostMapping
    public ResponseEntity<User> create(@Valid @RequestBody User u) {
        return ResponseEntity.status(HttpStatus.CREATED).body(service.create(u));
    }
}
```

### Why DTOs?
- Hide internal fields (e.g., password).
- Decouple API from database structure.
- Control exactly what data goes in/out.

---

## ✅ Validation

Add rules with annotations + `@Valid`:
```java
public class UserDTO {
    @NotBlank(message = "Name is required")
    private String name;
    @Email
    private String email;
    @Min(18)
    private int age;
}
```
`@Valid @RequestBody UserDTO dto` → Spring validates and rejects bad input automatically.

---

## 🛡️ Exception Handling (Global)

Handle errors in ONE place with `@RestControllerAdvice`:
```java
@RestControllerAdvice
public class GlobalExceptionHandler {

    @ExceptionHandler(ResourceNotFoundException.class)
    public ResponseEntity<ApiError> handleNotFound(ResourceNotFoundException ex) {
        ApiError err = new ApiError(404, ex.getMessage());
        return ResponseEntity.status(HttpStatus.NOT_FOUND).body(err);
    }

    @ExceptionHandler(MethodArgumentNotValidException.class)
    public ResponseEntity<String> handleValidation(MethodArgumentNotValidException ex) {
        return ResponseEntity.badRequest().body("Validation failed");
    }
}
```

**ResponseEntity** lets you control the status code, headers, and body.

---

## 📋 Common HTTP Status Codes
| Code | Meaning |
|------|---------|
| 200 OK | Success |
| 201 Created | Resource created |
| 204 No Content | Success, no body |
| 400 Bad Request | Invalid input |
| 401 Unauthorized | Not logged in |
| 403 Forbidden | No permission |
| 404 Not Found | Doesn't exist |
| 500 Server Error | Something broke |

---

## 🌍 Real-World Use Case
Every backend — an e-commerce API exposes `/products`, `/cart`, `/orders` following this exact
layered structure with DTOs, validation, and global error handling.

---

## ❓ Interview Questions
1. What is REST? Principles of RESTful APIs? (Stateless, resource-based, uses HTTP methods)
2. Difference between `@Controller` and `@RestController`?
3. Why use DTOs instead of exposing entities?
4. Difference between `@RequestParam`, `@PathVariable`, `@RequestBody`?
5. How do you handle exceptions globally? (`@RestControllerAdvice`)
6. What is `ResponseEntity`?
7. PUT vs PATCH?
8. How does validation work in Spring Boot?
9. Is REST stateless? (Yes)
10. Difference between `@RequestMapping` and `@GetMapping`?

---

## ✅ Best Practices
- Keep controllers thin; put logic in services.
- Always use DTOs for request/response.
- Validate input with `@Valid`.
- Centralize error handling with `@RestControllerAdvice`.
- Return proper HTTP status codes.

## ⚠️ Common Mistakes
- Exposing entities directly (leaks DB structure, causes lazy-loading issues).
- Business logic in controllers.
- Returning 200 for everything (even errors).
- No input validation.

---

## ⚡ Quick Revision Notes
- Layers: Controller → Service → Repository → DB. DTO for I/O, Mapper converts.
- `@RestController` = `@Controller` + `@ResponseBody`.
- `@PathVariable` (URL path), `@RequestParam` (query), `@RequestBody` (JSON body).
- Validate with `@Valid` + annotations; handle errors with `@RestControllerAdvice`.
- `ResponseEntity` controls status/headers/body.

## 🙋 FAQs
**Q: PUT vs PATCH?** PUT replaces the whole resource; PATCH updates part of it.

## 📎 References
- Spring Boot docs — Web, Validation
- REST API design guidelines

[⬅ Back to Spring Boot Index](./README.md)

