# 1. Authentication, Authorization, Filter Chain & Password Encoding

> 🟡 **Level:** Intermediate | 🔥 **Interview Frequency:** Very High

---

## 🧠 Concept

- **Authentication (AuthN)** = **Who are you?** (verify identity — login).
- **Authorization (AuthZ)** = **What are you allowed to do?** (check permissions).

```
Authentication → prove identity (username + password)
Authorization  → check access (is this user an ADMIN?)
```

### 💬 Simple Explanation
At an airport:
- **Authentication** = showing your passport (who you are).
- **Authorization** = your boarding pass deciding which plane/seat you can access.

---

## 🔗 Security Filter Chain

Spring Security works as a **chain of filters** that every request passes through **before**
reaching your controller.

```
Request → [ Filter1 → Filter2 → AuthN Filter → AuthZ Filter ] → Controller
              (each filter can allow, block, or modify the request)
```

Key filters: `UsernamePasswordAuthenticationFilter`, `BasicAuthenticationFilter`,
(and your custom `JwtFilter`).

---

## 🧩 Basic Config (Spring Security 6)

```java
@Configuration
@EnableWebSecurity
public class SecurityConfig {

    @Bean
    public SecurityFilterChain filterChain(HttpSecurity http) throws Exception {
        http
            .csrf(csrf -> csrf.disable())
            .authorizeHttpRequests(auth -> auth
                .requestMatchers("/public/**").permitAll()   // open
                .requestMatchers("/admin/**").hasRole("ADMIN")// admin only
                .anyRequest().authenticated()                // everything else needs login
            )
            .httpBasic(Customizer.withDefaults());
        return http.build();
    }

    @Bean
    public PasswordEncoder passwordEncoder() {
        return new BCryptPasswordEncoder();   // hash passwords
    }
}
```

---

## 🔑 Password Encoding

**Never store plain passwords.** Hash them with **BCrypt** (a one-way, salted hash).

```java
String hashed = passwordEncoder.encode("myPassword");  // store this
boolean ok = passwordEncoder.matches("myPassword", hashed);  // verify on login
```

- **Hashing** ≠ encryption — you can't reverse a hash.
- BCrypt adds a **salt** (random data) so identical passwords have different hashes.

---

## 🌍 Real-World Use Case
A user logs in → Spring authenticates the credentials → checks their role → allows access to
`/admin` only if they're an ADMIN. Passwords are stored as BCrypt hashes.

---

## ❓ Interview Questions
1. Difference between authentication and authorization?
2. How does the Spring Security filter chain work?
3. Why hash passwords? Why BCrypt (with salt)?
4. Difference between hashing and encryption?
5. What is `UserDetailsService`? (Loads user data for authentication)
6. What is `SecurityContext`? (Holds the current authenticated user)
7. What is `AuthenticationManager`?
8. Stateful (session) vs stateless (token) auth?

---

## ✅ Best Practices
- Always hash passwords (BCrypt/Argon2) — never plain text.
- Give least privilege (only needed roles).
- Keep security config in one place.
- Use HTTPS everywhere.

## ⚠️ Common Mistakes
- Storing plain or weakly-hashed (MD5/SHA1) passwords.
- Confusing authentication with authorization.
- Disabling security "temporarily" and forgetting.

---

## ⚡ Quick Revision Notes
- AuthN = who you are (login); AuthZ = what you can do (roles/permissions).
- Security = chain of filters before the controller.
- Hash passwords with BCrypt (salted, one-way).
- `UserDetailsService` loads users; `SecurityContext` holds the current user.

## 🙋 FAQs
**Q: Can you reverse a BCrypt hash?** No — hashing is one-way; you verify by re-hashing the input.

## 📎 References
- Spring Security reference docs

[⬅ Back to Security Index](./README.md)

