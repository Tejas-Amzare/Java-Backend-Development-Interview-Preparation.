# 2. JWT, OAuth2, Roles, Method Security, CORS & CSRF

> 🔴 **Level:** Advanced | 🔥 **Interview Frequency:** Very High

---

## 🎟️ JWT (JSON Web Token)

### 🧠 Concept
A **JWT** is a signed token the server gives you after login. You send it with every request to
prove who you are — **no server-side session needed** (stateless).

### Structure
```
header.payload.signature
  │       │        │
  algo   data     verify (signed with secret key)
```
```json
// payload example
{ "sub": "aman", "role": "ADMIN", "exp": 1699999999 }
```

### Flow
```
1. Login (username + password)
2. Server verifies → returns JWT
3. Client stores JWT → sends it in header:
      Authorization: Bearer <token>
4. Server verifies signature → allows request
```

- **Stateless** — server doesn't store sessions → scales well.
- Token is **signed** (tamper-proof) but readable — never put secrets in it.

---

## 🔓 OAuth2

### 🧠 Concept
**OAuth2** lets users log in using **another provider** (Google, GitHub) without sharing their
password with your app. It's about **delegated access**.

```
"Login with Google" → Google authenticates → gives your app a token → app trusts it
```
Roles: Resource Owner (user), Client (your app), Authorization Server (Google), Resource Server.

---

## 👮 Roles & Permissions

- **Role** = a group (ADMIN, USER, MANAGER).
- **Permission/Authority** = a fine-grained action (READ_ORDER, DELETE_USER).

```java
.requestMatchers("/admin/**").hasRole("ADMIN")
.requestMatchers("/reports/**").hasAuthority("READ_REPORT")
```

---

## 🔒 Method-Level Security

Secure individual methods, not just URLs.
```java
@EnableMethodSecurity
// ...
@PreAuthorize("hasRole('ADMIN')")
public void deleteUser(Long id) { ... }

@PreAuthorize("#userId == authentication.principal.id")  // only own data
public User getUser(Long userId) { ... }
```

---

## 🌐 CORS (Cross-Origin Resource Sharing)

### 🧠 Concept
Browsers block requests from one origin (domain) to another by default. **CORS** tells the
browser which other origins are **allowed** to call your API.

```java
@Bean
public WebMvcConfigurer corsConfigurer() {
    return new WebMvcConfigurer() {
        public void addCorsMappings(CorsRegistry reg) {
            reg.addMapping("/**").allowedOrigins("https://myfrontend.com");
        }
    };
}
```
Use: allow your React frontend (different domain/port) to call the backend.

---

## 🛡️ CSRF (Cross-Site Request Forgery)

### 🧠 Concept
An attack where a logged-in user is tricked into making an **unwanted request**. Spring adds a
**CSRF token** to protect form-based/session apps.

- **Session-based apps** → keep CSRF **enabled**.
- **Stateless JWT APIs** → usually **disable** CSRF (no cookies/session used).

---

## 📋 CORS vs CSRF (don't confuse!)
| CORS | CSRF |
|------|------|
| Controls **who can call** your API | Prevents **forged requests** |
| Browser same-origin policy | Attack using user's logged-in session |
| Fixed via allowed origins | Fixed via CSRF tokens |

---

## 🌍 Real-World Use Case
A React app + Spring Boot API: login returns a JWT, the frontend sends it as `Bearer` token,
CORS allows the frontend domain, CSRF is disabled (stateless), and `@PreAuthorize` guards
admin endpoints.

---

## ❓ Interview Questions
1. What is JWT? What are its 3 parts?
2. Why is JWT stateless? Advantage over sessions?
3. Where should you store a JWT on the client? (HttpOnly cookie or memory; avoid localStorage for XSS)
4. What is OAuth2? Difference from JWT? (OAuth2 = protocol; JWT = token format)
5. Difference between role and authority?
6. What is method-level security? (`@PreAuthorize`)
7. What is CORS? Why do we need it?
8. What is CSRF? When to disable it?
9. Difference between CORS and CSRF?
10. How do you refresh an expired JWT? (Refresh token)

---

## ✅ Best Practices
- Keep JWTs short-lived; use refresh tokens.
- Sign JWTs with a strong secret / RSA keys; never expose the secret.
- Restrict CORS to known origins (not `*` in production).
- Disable CSRF only for stateless APIs.

## ⚠️ Common Mistakes
- Putting sensitive data in the JWT payload (it's readable!).
- Allowing all origins (`*`) in CORS in production.
- Storing JWT in localStorage (XSS risk).
- Disabling CSRF in a session-based app.

---

## ⚡ Quick Revision Notes
- JWT = signed stateless token: `header.payload.signature`, sent as `Bearer`.
- OAuth2 = login via Google/GitHub (delegated access).
- Roles (groups) vs authorities (fine-grained); `@PreAuthorize` for method security.
- CORS = who can call your API; CSRF = block forged requests (disable for stateless JWT).

## 🙋 FAQs
**Q: JWT vs session?** JWT is stateless (nothing stored server-side, scales easily); sessions are stored on the server.

## 📎 References
- jwt.io
- Spring Security OAuth2 docs

[⬅ Back to Security Index](./README.md)

