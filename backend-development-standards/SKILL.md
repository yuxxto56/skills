---
name: backend-development-standards
description: Use when designing or modifying backend APIs, controller-logic-model layering, BaseController inheritance, validation, response formats, error codes, upload security, performance-sensitive endpoints, multi-table queries, or MySQL table schemas.
---

# Backend Development Standards

## Core Rule

Apply these standards before designing or changing backend interfaces, business logic, data access, multi-table queries, uploads, tests, or MySQL schemas. Prefer clear layering, explicit parameters, unified responses, and predictable data access over clever shortcuts.

## Layering

- Business Controllers must extend `BaseController` or the project's shared Controller base class.
- Keep shared response handling, exception capture, parameter reading, and basic type conversion in `BaseController`.
- Controllers only receive parameters one by one, perform basic validation, authorize, call Logic, and return unified responses.
- Controllers must not contain complex business decisions, database query assembly, transaction details, or cross-model workflows.
- Business Controllers must not call low-level response helpers directly or duplicate shared response and exception handling.
- Keep Logic and Model as sibling layers; do not put Logic inside the Model directory.
- Logic owns business rules, state checks, workflow orchestration, and transaction boundaries.
- Logic must access data through Model methods only; do not build SQL directly or bypass Model table access.
- Model owns field constants, base queries, writes, updates, deletes, counts, and reusable data access methods.
- Use Model field constants instead of scattering raw field-name strings through business code.
- On business-rule failure, Logic must throw a business exception; do not use `null`, `false`, empty arrays, or special IDs to signal failure.
- Transactions should wrap only required read/write steps, not validation, file processing, response assembly, or unrelated reads.

## API, Validation, And Errors

- Keep APIs frontend/backend separated and return JSON.
- All API responses must be `{ code, message, data }`.
- Use `code = 0` for success and `code != 0` for business or API errors.
- Successful `data` returns real business data.
- Error responses must keep `data`, defaulting to an empty array.
- GET parameters come from query string; POST parameters come from body.
- Prefer POST for writes unless the project defines another convention.
- Do not default to RESTful path-parameter style.
- Keep routes explicit, stable, and predictable; avoid fuzzy matching or route-order fallbacks.
- Separate public and admin APIs clearly by route, name, and authorization boundary.
- Controllers handle required checks, basic type conversion, string trimming, integer defaults, and simple range checks.
- Logic still validates business validity, such as resource existence, allowed state, and relationship constraints.
- Repeated validation belongs in `BaseController` or reusable validation utilities.
- Define error codes centrally and get messages through an error-code mapping.
- Unknown error codes need a fallback message.

## Upload, Security, Performance, And Queries

- Admin write APIs require an explicit authorization boundary.
- MVP admin tokens may be fixed, but must come from environment configuration and never be hardcoded.
- Upload APIs must validate file existence, size, extension, and MIME type.
- Upload failures must return unified error codes and unified response shape.
- Keep public file URLs separate from physical storage paths.
- Never let untrusted client parameters directly participate in file-path construction.
- List APIs return only list-page fields; detail APIs return full fields.
- Do not load large fields, long text, or detail-only fields for list display.
- Use batch queries for interaction, statistics, or relationship states; never query inside loops.
- Multi-table business queries must not use `LEFT JOIN`, `RIGHT JOIN`, or similar join queries.
- For multi-table relationships, query in stages: first fetch the primary table's relationship IDs, then query related tables with `IN`, then assemble results in Logic.
- Example: query users to get `uid[]`, query orders with `WHERE uid IN (...)`, group orders by `uid`, and merge into user results in Logic.
- Do not introduce cache early; evaluate cache, object storage, or CDN only after data volume, traffic, or stability issues are proven.

## MySQL Schema Rules

- Use MySQL by default.
- Maintain table-creation scripts in the project's database script directory.
- Use `utf8mb4` and `utf8mb4_unicode_ci`.
- Use the `InnoDB` engine.
- Every table needs a clear table comment.
- Every field needs a clear comment explaining meaning, value rules, or business constraints.
- Store time fields as Unix seconds: `INT(10) NOT NULL DEFAULT 0`.
- Do not use `DATE` or `DATETIME` for business time fields.
- Use `TINYINT(1)` for status, type, and switch fields.
- Do not use `ENUM`.
- Prefer normal indexes or application-layer combined search over `FULLTEXT`; confirm MySQL version, engine, and deployment support before using `FULLTEXT`.
- Protect duplicate-write relationships with database unique constraints.
- For related deletes, define foreign-key constraints, cascade strategy, or application-layer delete strategy explicitly.
- After schema changes, check Models, Logic, API docs, seed data, and tests.

## Verification Checklist

- Controller structure tests verify business Controllers inherit the shared base class and do not directly call low-level response helpers.
- Logic layering tests verify Logic does not bypass Model to access database query APIs.
- Validation tests cover missing required parameters, invalid types, and error responses with `data` as an empty array.
- Tests or static checks cover response shape, error codes, route style, layering rules, multi-table query style, and database constraints.
- Interface or schema changes update affected frontend requests, backend routes, tests, API docs, and troubleshooting notes where relevant.
