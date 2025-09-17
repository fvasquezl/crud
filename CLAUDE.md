# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a Laravel 12 + Inertia.js + Vue 3 application with authentication, user settings, and CRUD functionality. It uses Tailwind CSS v4 for styling and Pest v4 for testing.

### Architecture Overview

- **Backend**: Laravel 12 with Laravel Fortify for authentication
- **Frontend**: Inertia.js v2 with Vue 3 and TypeScript
- **UI Components**: Custom component library with Reka UI primitives
- **Styling**: Tailwind CSS v4 with custom design system
- **Testing**: Pest v4 with browser testing capabilities
- **Database**: MariaDB with Eloquent ORM

### Key Technology Stack

- PHP 8.4.1
- Laravel 12.29.0 (uses streamlined Laravel 11+ structure)
- Inertia.js v2 with deferred props and infinite scrolling
- Vue 3.5+ with Composition API and TypeScript
- Tailwind CSS v4 (note: uses `@import "tailwindcss"` syntax)
- Pest v4 with browser testing
- Laravel Wayfinder for page-based routing
- Laravel Fortify for authentication with 2FA support

## Development Commands

### Primary Development Workflow
```bash
composer run dev          # Start full development stack (server, queue, logs, vite)
composer run dev:ssr      # Development with SSR support
npm run dev              # Frontend development server only
php artisan serve        # Backend server only
```

### Build Commands
```bash
npm run build            # Build frontend assets
npm run build:ssr        # Build frontend assets with SSR
```

### Testing Commands
```bash
php artisan test                                    # Run all tests
php artisan test --filter=testName                # Run specific test
php artisan test tests/Feature/ExampleTest.php    # Run tests in specific file
php artisan test tests/Browser/                   # Run browser tests only
```

### Code Quality
```bash
vendor/bin/pint --dirty    # Format PHP code (run before committing)
npm run lint              # Lint and fix JavaScript/Vue files
npm run format            # Format JavaScript/Vue with Prettier
npm run format:check      # Check formatting without fixing
```

### Database
```bash
php artisan migrate              # Run migrations
php artisan migrate:fresh       # Fresh migration with data loss
php artisan db:seed             # Run seeders
```

## Application Structure

### Frontend Architecture
- **Pages**: `resources/js/pages/` - Inertia.js page components
- **Layouts**: `resources/js/layouts/` - Layout components (app, auth, settings)
- **Components**: `resources/js/components/` - Reusable Vue components
- **UI Components**: `resources/js/components/ui/` - Design system components
- **Composables**: `resources/js/composables/` - Vue composition functions
- **Types**: `resources/js/types/` - TypeScript type definitions

### Backend Architecture
- **Controllers**: Standard Laravel structure with Form Requests for validation
- **Models**: `app/Models/` with Eloquent relationships and proper type hints
- **Policies**: `app/Policies/` for authorization logic
- **Middleware**: Custom middleware in `app/Http/Middleware/`
- **Providers**: `app/Providers/` for service configuration

### Key Features Implemented
- **Authentication**: Laravel Fortify with 2FA support
- **User Settings**: Profile, password, appearance, two-factor authentication
- **CRUD Operations**: Post management with proper authorization
- **Theme System**: Dark/light mode with appearance persistence
- **Responsive Design**: Mobile-first with sidebar navigation

## Laravel Boost Integration

This application includes Laravel Boost MCP server with powerful development tools:

- Use `mcp__laravel-boost__search-docs` for package-specific documentation
- Use `mcp__laravel-boost__tinker` for PHP debugging and testing
- Use `mcp__laravel-boost__database-query` for read-only database operations
- Use `mcp__laravel-boost__application-info` to get current package versions
- Use `mcp__laravel-boost__browser-logs` for frontend debugging

## Important Conventions

### Laravel 12 Structure Notes
- No `app/Http/Kernel.php` - middleware registered in `bootstrap/app.php`
- No `app/Console/Kernel.php` - commands auto-register from `app/Console/Commands/`
- Service providers in `bootstrap/providers.php`
- Route files: `routes/web.php`, `routes/auth.php`, `routes/settings.php`

### Frontend Conventions
- Use Inertia `<Form>` component for forms with proper error handling
- Components use single root element (Vue 3 requirement with Inertia)
- TypeScript is used throughout the frontend
- Tailwind v4 syntax with `@import "tailwindcss"`
- Custom UI components follow design system patterns

### Code Quality Requirements
- All changes must have corresponding tests (Pest format)
- Run `vendor/bin/pint --dirty` before committing PHP changes
- Run `npm run lint` for JavaScript/Vue code quality
- Use Laravel Boost `search-docs` tool before making framework-related changes

## Testing Strategy

- **Unit Tests**: `tests/Unit/` for isolated component testing
- **Feature Tests**: `tests/Feature/` for application functionality
- **Browser Tests**: `tests/Browser/` for end-to-end user workflows
- Use Pest v4 browser testing for complex user interactions
- Test authentication, CRUD operations, and UI components
- Browser tests can interact with real browsers (Chrome, Firefox, Safari)

This application follows Laravel Boost guidelines for optimal development experience. Always use the available MCP tools for documentation, debugging, and development tasks.