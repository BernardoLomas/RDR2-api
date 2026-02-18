## 01 – Project Vision – RDR2 API 
> Purpose
The RDR2 API is a backend training project designed to simulate a production-grade public REST API. Its primary goal is to apply backend architecture principles in a realistic context, emphasizing clean structure, scalability, security, and data integrity.

> Target Consumer
This API is intended for developers and gaming enthusiasts who want to experiment with or build applications using structured Red Dead Redemption 2 compendium data. While it does not solve a business problem, it simulates a real-world public API designed for consumption.

> Technical Stack
. TypeScript
. Node.js
. NestJS
. Relational Database

> Why It Exists
The project exists to bridge backend theory and production-level implementation. It provides a structured environment to practice architectural decisions, validation strategies, authentication mechanisms, transactional consistency, and modular design.

> Learning Objectives
# Architecture
. Design a modular NestJS application following clean separation of concerns.
. Structure the application using domain-driven module boundaries.
# Security
. Implement JWT-based authentication.
. Apply role-based access control (RBAC) for write operations.
# Data Integrity
. Apply ACID-compliant transaction management.
. Design relational database schemas with proper constraints.
. Implement soft deletes and audit fields.
# API Design
. Build RESTful endpoints with consistent response patterns.
. Implement scalable pagination and filtering mechanisms.
. Design slug-based resource access.
# Observability
. Implement centralized error handling.
. Apply structured logging strategies.