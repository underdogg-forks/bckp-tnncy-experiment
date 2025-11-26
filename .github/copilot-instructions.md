# Copilot Instructions for tnncy-experiment

## Project Overview

This is a Laravel 7 application with multi-tenancy support using the `hyn/multi-tenant` package. The project separates system-level and tenant-level models and functionality.

## Code Style and Formatting

- **Preset**: Laravel coding standards (PSR-2/PSR-12)
- **Indentation**: 4 spaces for PHP, 2 spaces for YAML files
- **Line Endings**: LF (Unix-style)
- **Charset**: UTF-8
- **Final Newline**: Always include a final newline in files
- **Trailing Whitespace**: Remove trailing whitespace (except in Markdown files)

Refer to `.editorconfig` and `.styleci.yml` for specific formatting rules.

## Project Structure

```
app/
├── Console/         # Artisan commands
├── Exceptions/      # Custom exception handlers
├── Http/           # Controllers, middleware, requests
├── Providers/      # Service providers
└── models/
    ├── System/     # System-level models (cross-tenant)
    └── Tenant/     # Tenant-specific models
```

## Multi-Tenancy Architecture

This project uses multi-tenancy with separate databases per tenant:
- **System Models**: Located in `app/models/System/` - used for cross-tenant data
- **Tenant Models**: Located in `app/models/Tenant/` - used for tenant-specific data
- Always consider tenant context when working with database operations
- Be mindful of which database connection you're using

## Testing

### Running Tests

```bash
# Run all tests
./vendor/bin/phpunit

# Run specific test suite
./vendor/bin/phpunit --testsuite=Unit
./vendor/bin/phpunit --testsuite=Feature

# Run specific test file
./vendor/bin/phpunit tests/Feature/ExampleTest.php
```

### Test Structure

- **Unit Tests**: `tests/Unit/` - Test individual classes/methods in isolation
- **Feature Tests**: `tests/Feature/` - Test HTTP endpoints and full features
- Test methods should start with `test` prefix
- Use descriptive test method names that explain what is being tested

### Test Database

Tests use an in-memory SQLite database by default (configured in `phpunit.xml`)

## Building Assets

### NPM Scripts

```bash
# Install dependencies
npm install

# Development build
npm run dev

# Production build
npm run prod

# Watch for changes
npm run watch

# Hot module replacement
npm run hot
```

## Laravel Conventions

### Naming Conventions

- **Controllers**: PascalCase with `Controller` suffix (e.g., `UserController`)
- **Models**: Singular PascalCase (e.g., `User`, `Post`)
- **Database Tables**: Plural snake_case (e.g., `users`, `blog_posts`)
- **Migrations**: Descriptive with timestamp prefix
- **Routes**: kebab-case for URL segments
- **Variables**: camelCase

### Best Practices

- Use Eloquent ORM for database operations
- Follow Laravel's service container and dependency injection patterns
- Use form requests for validation logic
- Keep controllers thin, use services for business logic
- Use resource controllers for RESTful operations
- Leverage Laravel's built-in features (validation, authentication, caching, etc.)

## Dependencies

### PHP Requirements

- PHP ^7.2.5
- Composer for dependency management

### Key Dependencies

- Laravel Framework ^7.0
- hyn/multi-tenant ^5.6 (multi-tenancy support)
- Guzzle HTTP client
- Laravel Tinker

### Development Dependencies

- PHPUnit ^8.5
- Faker for test data
- Mockery for mocking

## Environment Setup

1. Copy `.env.example` to `.env`
2. Generate application key: `php artisan key:generate`
3. Configure database connections in `.env`
4. Run migrations: `php artisan migrate`
5. Install Composer dependencies: `composer install`
6. Install NPM dependencies: `npm install`

## Common Commands

```bash
# Clear caches
php artisan cache:clear
php artisan config:clear
php artisan route:clear
php artisan view:clear

# Generate files
php artisan make:controller ControllerName
php artisan make:model ModelName
php artisan make:migration create_table_name
php artisan make:seeder SeederName

# Database
php artisan migrate
php artisan migrate:rollback
php artisan db:seed
```

## Security Considerations

- Never commit `.env` file or secrets
- Use Laravel's built-in CSRF protection
- Sanitize user input
- Use parameterized queries (Eloquent handles this)
- Follow Laravel security best practices
- Be cautious with tenant data isolation in multi-tenant context

## Notes for AI Assistants

- Always check tenant context when modifying database queries
- Respect existing code style and Laravel conventions
- Run tests after making changes to ensure nothing breaks
- Consider the multi-tenant architecture when adding new features
- Use Laravel's built-in helpers and facades when appropriate
- Keep backward compatibility in mind when modifying existing code
