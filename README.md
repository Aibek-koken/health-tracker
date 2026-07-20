# Health Tracer

A comprehensive health and habit tracking application built with Spring Boot and Jakarta EE that helps users monitor their daily habits, health metrics, and wellness journey.

---

## 📋 Overview

Health Tracer is a web-based application designed to help users:
- Track daily habits and health routines
- Monitor health statistics and progress
- Share experiences through posts and social features
- Build a community around health and wellness goals

---

## 🚀 Features

### Core Functionality
- **Habit Tracking**: Create, monitor, and maintain daily habits
- **Health Statistics**: Track various health metrics and view progress over time
- **Social Features**: Share posts, like content, and engage with the community
- **User Management**: Complete user authentication and profile management
- **Habit Logging**: Detailed logging of habit completion and consistency

### API Endpoints
- User authentication and authorization
- Habit creation and management
- Health statistics tracking
- Social posting and interaction features
- Comprehensive habit logging system

---

## 🛠️ Technology Stack

- **Backend Framework**: Spring Boot with Spring MVC
- **Database**: Spring Data JPA for data persistence
- **Java Version**: Java 25
- **Enterprise Features**: Jakarta EE integration
- **Build Tool**: Maven
- **Containerization**: Docker support
- **Deployment**: Heroku-ready with Procfile

---

## 📁 Project Structure

```
helth-tracer/
├── src/main/java/com/helthtracer/
│   ├── config/          # Application configuration
│   ├── controller/      # REST API controllers
│   ├── model/           # Entity models and data structures
│   ├── repository/      # Data access layer
│   └── HealthTracerApplication.java
├── src/main/resources/  # Application properties and resources
├── .github/workflows/   # CI/CD pipeline configuration
├── Dockerfile           # Container configuration
└── pom.xml              # Maven dependencies
```

---

## 🏃‍♂️ Getting Started

### Prerequisites
- Java 25 or higher
- Maven 3.6+
- Docker (optional, for containerization)

### Installation

1. **Clone the repository**
   ```bash
   git clone <repository-url>
   cd helth-tracer
   ```

2. **Build the project**
   ```bash
   ./mvnw clean install
   ```

3. **Run the application**
   ```bash
   ./mvnw spring-boot:run
   ```

4. **Access the application**
   Open your browser and navigate to `http://localhost:8080`

### Migration note: password hashing

Passwords are now hashed with BCrypt (`spring-boot-starter-security`,
`PasswordEncoder`) instead of being stored and compared as plain text.
This is a breaking change for any existing `users` row created before this
change: its `password` column holds a raw string, not a BCrypt hash, so
`passwordEncoder.matches(...)` will never match it and that account can no
longer log in. There is no migration path for those old values (a plain-text
password can't be turned into its own hash after the fact) — affected users
need to re-register, or the `users` table needs to be cleared in any
environment that only ever held test data.

### Docker Deployment

1. **Build the Docker image**
   ```bash
   docker build -t health-tracer .
   ```

2. **Run the container**
   ```bash
   docker run -p 8080:8080 health-tracer
   ```

---

## 🎯 Why Use Health Tracer?

### For Individuals
- **Habit Formation**: Build and maintain healthy daily routines
- **Progress Tracking**: Visualize your health journey with detailed statistics
- **Motivation**: Stay motivated through social features and community support
- **Comprehensive Logging**: Keep detailed records of your health activities

### For Developers
- **Modern Tech Stack**: Built with latest Java and Spring Boot features
- **Scalable Architecture**: Clean separation of concerns with MVC pattern
- **API-First Design**: RESTful APIs for easy integration
- **Container Ready**: Docker support for easy deployment
- **CI/CD Ready**: GitHub Actions workflow included

### For Organizations
- **Employee Wellness**: Deploy as an internal wellness platform
- **Customizable**: Extensible architecture for specific requirements
- **Secure**: Built with Spring Security best practices
- **Cloud Ready**: Heroku deployment configuration included

---

**Start your health journey today with Health Tracer!** 🌟
