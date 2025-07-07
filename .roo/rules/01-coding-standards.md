# Coding Standards

## General Principles
- Follow SOLID principles in all implementations
- Use TypeScript strict mode across all projects
- Implement proper error handling with custom error classes
- Maintain consistent code formatting with Prettier and ESLint
- Write self-documenting code with clear variable and function names

## Frontend Standards
- Use Tailwind CSS utility-first approach for all styling
- Prefer Tailwind utilities over custom CSS whenever possible
- Organize Tailwind classes logically: layout → spacing → colors → typography → effects
- Use semantic HTML elements with proper ARIA attributes
- Implement responsive design with mobile-first approach

## Tailwind CSS Guidelines
- Configure JIT mode for optimal development experience
- Use Tailwind's design tokens for consistent spacing and colors
- Create custom components only when utilities become repetitive
- Purge unused CSS in production builds
- Use @apply directive sparingly, only for component base styles

## Git Workflow
- Use conventional commits for clear history
- Create feature branches with descriptive names
- Require code review before merging to main
- Maintain clean commit history with meaningful messages

## Documentation Requirements
- Document all public APIs with JSDoc comments
- Maintain updated README files for each module
- Create architecture decision records (ADRs) for major decisions
- Document environment setup and deployment procedures
- Document Tailwind component patterns and design system

## Security Standards
- Never commit secrets or API keys to version control
- Use environment variables for configuration
- Implement proper input validation and sanitization
- Follow OWASP guidelines for web application security