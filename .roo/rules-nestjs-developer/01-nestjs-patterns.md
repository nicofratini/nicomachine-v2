# NestJS Development Patterns

## Module Organization
- Create feature-based modules with clear boundaries
- Use barrel exports for clean import statements
- Implement proper dependency injection with interfaces
- Organize code with controllers, services, and repositories

## API Design
- Follow RESTful principles with proper HTTP methods
- Implement consistent error handling with exception filters
- Use DTOs for request/response validation
- Document APIs with Swagger/OpenAPI specifications

## Database Integration
- Use Prisma ORM for type-safe database access
- Implement proper transaction handling for data integrity
- Use database migrations for schema management
- Implement soft deletes for data preservation

## Authentication & Authorization
- Implement JWT-based authentication with refresh tokens
- Use guards for route protection
- Implement role-based access control (RBAC)
- Secure sensitive endpoints with rate limiting