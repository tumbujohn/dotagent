---
name: engineering-constitution
description: Mandatory, always-on engineering standards covering planning, UI/UX, accessibility, performance, security, authentication, file uploads, logging, error handling, architecture, naming, APIs, database, migrations, git workflow, testing, refactoring, documentation, dependencies, and framework conventions (Laravel/CodeIgniter). Consult before planning or implementing any non-trivial feature, and run the quality checklist before finishing work.
---

# Engineering Constitution
Version: 1.0

This document defines the engineering standards, architecture principles, development workflow, and quality expectations for every project.

These rules are mandatory unless explicitly overridden by project documentation.

---

# 1. Project Documentation

Before beginning ANY new feature or task:

1. Read `/docs/`
2. Read `README.md`
3. Read architecture documentation
4. Read existing conventions
5. Never assume.

If documentation conflicts with this file:

Project documentation wins ONLY for project-specific behavior.

This document always governs engineering quality.

---

# 2. Planning First

Never immediately write code.

For every non-trivial task:

- Understand the problem
- Identify affected modules
- Identify risks
- Produce a small implementation plan
- Then implement

Large features should always be broken into logical phases.

---

# 3. UI / UX

ALWAYS invoke:

/frontend-design

before writing ANY frontend.

This includes:

- HTML
- PHP Views
- Blade Templates
- Tailwind
- CSS
- Components
- Forms
- Tables
- Dashboards
- Reports
- Emails
- Landing pages

Never build UI before consulting the frontend design skill.

---

# 4. Design Principles

Every interface must follow modern UX principles.

Always enforce:

- Visual hierarchy
- Accessibility
- Responsive layouts
- Consistent spacing
- Design systems
- Reusable components
- Progressive disclosure
- Clear navigation
- Proper empty states
- Proper loading states
- Error handling
- Success feedback

Avoid:

- Clutter
- Tiny click targets
- Misaligned layouts
- Random colors
- Multiple competing actions

---

# 5. Accessibility

Minimum WCAG AA compliance.

Always include:

- Labels
- Keyboard navigation
- Focus states
- Semantic HTML
- Proper heading hierarchy
- Color contrast
- Screen reader support

Never rely on color alone.

---

# 6. Mobile First

Every UI must work on:

Desktop

Tablet

Mobile

Never assume desktop-only.

---

# 7. Performance

Optimize before shipping.

Avoid:

- unnecessary queries
- duplicate rendering
- excessive JS
- blocking requests

Prefer:

- lazy loading
- pagination
- caching
- eager loading
- optimized assets
- code splitting

Performance is a feature.

---

# 8. Security

Always follow OWASP Top 10.

Never trust user input.

Always:

Validate

Sanitize

Escape output

Use parameterized queries

Protect against:

SQL Injection

XSS

CSRF

SSRF

File upload attacks

Session hijacking

Command injection

Mass assignment

Rate limit sensitive endpoints.

Never expose secrets.

Never hardcode credentials.

Always use environment variables.

Passwords:

Hash only.

Never encrypt passwords.

---

# 9. Authentication

Always use secure authentication.

Sessions:

Secure

HTTP Only

SameSite

Use CSRF protection.

Authorization must be server-side.

Never trust frontend permissions.

---

# 10. File Uploads

Always validate:

type

size

mime

extension

Store outside public directory whenever possible.

Generate random filenames.

Never trust uploaded filenames.

---

# 11. Logging

Log:

errors

warnings

security events

critical business events

Never log:

passwords

tokens

API secrets

PII unless required.

---

# 12. Error Handling

Never expose stack traces.

Show friendly messages.

Log detailed errors internally.

---

# 13. Architecture

Follow SOLID principles.

Favor:

composition

dependency injection

single responsibility

modularity

Avoid:

god classes

duplicate logic

massive controllers

business logic inside views

fat routes

---

# 14. Code Organization

Controllers:

Only coordinate.

Services:

Business logic.

Repositories:

Database.

Models:

Data.

Views:

Presentation only.

---

# 15. Naming

Names must describe intent.

Avoid abbreviations.

Bad:

temp1

abc

data2

Good:

InvoiceService

StudentRepository

PaymentProcessor

---

# 16. DRY

Never duplicate logic.

Extract reusable components.

---

# 17. Keep It Simple

Prefer simple solutions.

Avoid premature optimization.

---

# 18. Comments

Code should explain itself.

Comment WHY.

Never comment WHAT unless necessary.

---

# 19. APIs

RESTful.

Consistent responses.

Proper status codes.

Validate everything.

Version public APIs.

---

# 20. Database

Normalize appropriately.

Use indexes.

Use foreign keys.

Avoid N+1 queries.

Use transactions.

Never perform destructive operations without confirmation.

---

# 21. Migrations

Never modify existing production migrations.

Always create new migrations.

---

# 22. Git

Small commits.

Meaningful commit messages.

One logical change per commit.

---

# 23. Testing

Before completing work:

Check:

edge cases

validation

permissions

errors

performance

responsive UI

If automated tests exist:

Run them.

Never knowingly break existing functionality.

---

# 24. Refactoring

Always leave code cleaner.

Apply the Boy Scout Rule.

---

# 25. Documentation

Every significant feature should include:

purpose

architecture

usage

configuration

limitations

---

# 26. Dependencies

Prefer mature libraries.

Avoid unnecessary packages.

Every dependency increases maintenance cost.

---

# 27. AI Development Rules

When generating code:

Prefer readability.

Prefer maintainability.

Prefer explicitness.

Never generate code you wouldn't maintain.

When modifying existing code:

Respect project style.

Do not rewrite unrelated code.

Avoid introducing breaking changes.

---

# 28. Framework Standards

Laravel:

Use:

Policies

Requests

Services

Events

Jobs

Queues

Eloquent best practices

Avoid fat controllers.

CodeIgniter:

Use:

Services

Libraries

Validation

Filters

Repositories

Keep controllers thin.

---

# 29. Frontend Standards

Prefer:

Tailwind CSS

Component-driven UI

Reusable layouts

Minimal JavaScript

Accessible forms

Never duplicate components.

---

# 30. Code Quality Checklist

Before finishing:

✓ No duplicated code

✓ Proper validation

✓ Responsive

✓ Secure

✓ Accessible

✓ Clean architecture

✓ Naming consistent

✓ Errors handled

✓ Documentation updated

✓ Performance acceptable

✓ No console logs

✓ No debug code

✓ No dead code

✓ No TODOs without issue references

---

# 31. Decision Framework

When multiple solutions exist:

Prefer:

1. Simplicity

2. Maintainability

3. Security

4. Performance

5. Scalability

Never sacrifice maintainability for cleverness.

---

# 32. General Philosophy

Write software as if another engineer will maintain it in five years.

Every feature should be:

Simple.

Secure.

Elegant.

Maintainable.

Scalable.

Accessible.

Well documented.

Professional.