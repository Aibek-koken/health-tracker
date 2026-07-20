# Health Tracker

A habit- and health-tracking web application built with Spring Boot. Users track
daily habits, log completions, record basic health data, and share short posts
with likes and comments. The frontend is served as static pages from the
backend.

> **Status:** Auth is limited to password hashing; endpoint authorization is not
> implemented — this is a learning project. See [Security](#security).

## Features

- **Habits** — create habits and log daily completion to build consistency.
- **Habit logs** — record and review completion history per habit.
- **Health stats** — per-user statistics, including sleep sessions.
- **Social feed** — publish posts (with tags), like them, and comment.
- **Accounts** — registration and login with BCrypt-hashed passwords.

## Tech stack

- Java 17, Spring Boot (Spring MVC)
- Spring Data JPA
- Spring Security — used only for the BCrypt `PasswordEncoder` (see Security)
- Static HTML/CSS/JS frontend served from `src/main/resources/static`
- Maven
- Docker support; Heroku-ready `Procfile`

## Security

This is a learning project and its security posture is intentionally minimal and
clearly bounded:

- Passwords are hashed with BCrypt via Spring Security's `PasswordEncoder`. Login
  verifies with `passwordEncoder.matches(...)`; signup and user creation hash
  before saving. Password hashes are never returned in API responses.
- **Authorization is not implemented.** `SecurityConfig` permits all requests
  (`anyRequest().permitAll()`); the Spring Security dependency is present only to
  provide a working password encoder without locking down every endpoint by
  default. There is no session, token, or per-endpoint access control.

Do not treat this as a secured application.

### Migration note: password hashing

Passwords are now hashed with BCrypt instead of being stored and compared as
plain text. This is a breaking change for any `users` row created before the
change: its `password` column holds a raw string, not a BCrypt hash, so
`passwordEncoder.matches(...)` will never match and that account can no longer
log in. There is no migration path for those old values — affected users must
re-register, or the `users` table must be cleared in environments that only ever
held test data.

## Getting started

Requirements: Java 17, Maven 3.6+ (Docker optional).

```bash
./mvnw clean install
./mvnw spring-boot:run
```

Open `http://localhost:8080`.

### Docker

```bash
docker build -t health-tracker .
docker run -p 8080:8080 health-tracker
```

## Project structure

```
src/main/java/com/helthtracer/
  config/        SecurityConfig (BCrypt encoder) and configuration
  controller/    auth, habits, habit logs, posts, comments, likes, stats, users
  model/         Habit, HabitLog, Post, Comment, Like, Tag, SleepSession, User
  repository/    Spring Data JPA repositories
src/main/resources/static/   landing, login, signup, main, analytics, profile
```
