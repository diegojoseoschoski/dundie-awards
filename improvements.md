# Code Review Findings – Dundie Awards Application

## Overview

This document lists the issues identified during the code review of the Dundie Awards application. The items are grouped by category and prioritized based on impact and production risk.


---

# Stability (High Priority)

- Sensitive data such as passwords are stored directly in configuration files.
- Request payloads lack proper input validation .
- Remove duplicated or incorrectly nested `spring` keys in application.yaml file.
- There is no global exception handling mechanism (`@ControllerAdvice` missing).
- The system lacks automated tests beyond basic context loading.
- The application uses `CommandLineRunner` for database initialization instead of a proper migration tool such as Flyway or Liquibase.


---

# Architecture & Domain Design (High Priority)

- Controllers contain business logic instead of delegating to a service layer.
- JPA entities are exposed directly in API requests and responses, creating mass assignment risks.
- The employee creation payload requires knowledge of the full Organization structure instead of accepting only an organization identifier.
- There is no dedicated endpoint to grant Dundie Awards, even though it is a core domain concept.
- The Activity model exists but is not clearly integrated into the business flow.
- The update endpoint does not clearly define whether it supports full or partial updates.

---
# Performance & Operational Improvements

- Employee listing endpoints do not implement pagination.
- No authentication or authorization is configured.
- Health check endpoints are not enabled.
- Logging configuration is minimal and not production-oriented.
- The project does not provide a Dockerfile for containerized deployment.
- Ensure OpenAPI documentation is properly configured and functional.

---
# Code Quality

- The code uses field injection (@Autowired) instead of constructor injection, which limits testability and weakens immutability.
- Inconsistent use of `Integer` and `int` may lead to null-related issues.
- The field occuredAt in the Activity model is misspelled and should be renamed to occurredAt, ensuring the change is applied consistently in the entity, database schema, and templates.
- Test or demo data is hardcoded in application startup logic.
- The `application.properties` file appears unused and may cause configuration confusion.



