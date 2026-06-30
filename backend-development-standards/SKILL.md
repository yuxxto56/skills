---
name: backend-development-standards
description: Use when designing or modifying backend APIs, controller-logic-model layering, BaseController inheritance, validation, response formats, error codes, upload security, performance-sensitive endpoints, multi-table queries, PHP timezone configuration, database initialization checks, or MySQL table schemas.
---

# Backend Development Standards

## Core Rule

Apply these standards before designing or changing backend interfaces, business logic, data access, multi-table queries, uploads, tests, database initialization, or MySQL schemas. Prefer clear layering, explicit parameters, unified responses, and verifiable data access over clever shortcuts.

## Layering

- Business Controllers must extend `BaseController` or the project's shared Controller base class.
- Keep shared response handling, exception capture, parameter reading, and basic type conversion in `BaseController`.
- Controllers receive request parameters one by one, perform basic validation, authorize, call Logic, and return unified responses.
- Business Controller action methods must not receive request-context parameters such as `array $body`, `array $query`, `array $request`, `Request $request`, or `int $userId`.
- Keep business action signatures semantic and context-free, such as `create()`, `save()`, `list()`, and `detail()`.
- Read authenticated user identity through a shared base method such as `currentUserId()`; do not pass it into business actions as a method parameter.
- Controllers must not contain complex business decisions, database query assembly, transaction details, or cross-model workflows.
- Business Controllers must not call framework-native response helpers directly, manually assemble duplicate `{ code, message, data }` responses, or duplicate shared response and exception handling.
- Business Controllers may call `BaseController` or project-equivalent unified response methods.
- Keep Logic and Model as sibling layers; do not put Logic inside the Model directory.
- Logic owns business rules, state checks, workflow orchestration, and transaction boundaries.
- Logic must access data through Model methods only; do not build SQL directly or bypass Model table access.
- Raw SQL belongs only inside Model methods, database scripts, initialization scripts, health-check scripts, or project-equivalent data access boundaries; business Logic must not write raw SQL.
- Model owns field constants, base queries, writes, updates, deletes, counts, and reusable data access methods.
- Use Model field constants instead of scattering raw field-name strings through business code.
- On business-rule failure, Logic must throw a business exception; do not use `null`, `false`, empty arrays, or special IDs to signal failure.
- Transactions should wrap only required read/write steps, not validation, file processing, response assembly, or unrelated reads.
- When one operation changes both files and database rows, use a temporary-file, compensation cleanup, or equivalent strategy so failed database writes do not leave orphaned files.

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
- Controllers handle required checks, basic type conversion, string trimming, optional integer defaults, and simple range checks.
- Required integer parameters must explicitly validate presence, type, and range; do not silently coerce missing required values to `0`.
- Controllers should read each parameter through `BaseController` helpers such as `getRequiredString()`, `postRequiredString()`, `getInt()`, `postInt()`, or project-equivalent methods.
- In ThinkPHP 6 projects, wrap `think\facade\Request::get()` and `Request::post()` inside `BaseController` or a shared request adapter instead of scattering direct framework calls through every Controller.
- Local development or test entrypoints may inject fallback request context, but that adapter context must not appear in business Controller action signatures.
- Logic still validates business validity, such as resource existence, allowed state, and relationship constraints.
- Repeated validation belongs in `BaseController` or reusable validation utilities.
- Define error codes centrally and get messages through an error-code mapping.
- Unknown error codes need a fallback message.

## Upload, Security, Performance, And Queries

- Admin write APIs require an explicit authorization boundary.
- MVP admin tokens may be fixed, but must come from environment configuration and never be hardcoded.
- Upload APIs must validate file existence, size, extension, and MIME type.
- Upload validation must use an extension whitelist and server-side MIME or content detection; do not trust client-provided MIME type alone.
- Store uploads with generated random names; never use original filenames or other untrusted client values directly in storage paths.
- Image uploads should validate actual image content or re-encode images when the project risk level requires it.
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

## MySQL Schema And Initialization Rules

- Use MySQL by default.
- Configure PHP's default runtime timezone to `Asia/Shanghai` in backend bootstrap or the shared application entry before business code calls `time()`, `date()`, `strtotime()`, or `DateTime`.
- Keep business time calculations consistent with the configured PHP timezone; if a query needs explicit boundaries, compute them from `DateTimeImmutable` plus `DateTimeZone('Asia/Shanghai')` rather than relying on server defaults.
- Maintain table-creation scripts in the project's database script directory.
- Keep schema scripts and seed scripts separate.
- Seed scripts should be idempotent where practical, for example by using unique keys plus upsert behavior or a documented equivalent.
- Projects that require MySQL setup should provide both an initialization script and a health-check script.
- Use `utf8mb4` and `utf8mb4_unicode_ci`.
- Use the `InnoDB` engine.
- Every table needs a clear table comment.
- Every field needs a clear comment explaining meaning, value rules, or business constraints.
- Store time fields as Unix seconds: at least `INT(10) UNSIGNED NOT NULL DEFAULT 0`; use `BIGINT UNSIGNED` when the project needs a longer date range.
- Do not use `DATE` or `DATETIME` for business time fields.
- Use `TINYINT(1)` for status, type, and switch fields.
- Do not use `ENUM`.
- Prefer normal indexes or application-layer combined search over `FULLTEXT`; confirm MySQL version, engine, and deployment support before using `FULLTEXT`.
- Protect duplicate-write relationships with database unique constraints.
- For related deletes, define foreign-key constraints, cascade strategy, or application-layer delete strategy explicitly.
- After schema changes, check Models, Logic, API docs, seed data, and tests.

## Database Verification Flow

- Do not treat an API health response as proof that MySQL is connected, tables exist, or seed data is loaded.
- Verify database readiness before API smoke tests.
- Database initialization should follow this order: read environment configuration, connect to the MySQL service, check or create the target database, execute schema scripts, execute seed scripts, inspect tables and seed data, then run API smoke tests.
- Health-check scripts should clearly report `connected`, `database_exists`, `tables_ready`, and `seed_ready`, or project-equivalent status fields.
- Connection failures must include enough context to debug safely in server logs or CLI health-check output: host, port, database, user, and the driver error message.
- API responses must not expose database connection details; return unified error codes and generalized messages instead.
- Classify common database failures when possible: invalid username or password, unreachable host or port, missing target database, insufficient privileges, and SQL execution failure.
- Do not report initialization as complete when any database readiness check fails.

## Verification Checklist

Required for touched areas:

- Controller structure tests verify changed business Controllers inherit the shared base class and do not directly call framework-native response helpers.
- Controller signature tests verify changed business actions do not accept request-context parameters such as `array $body`, `array $query`, `Request $request`, or `int $userId`.
- BaseController or shared request-adapter tests verify changed GET, POST, required, optional, integer, and current-user parameter helpers.
- Logic layering tests verify changed Logic does not bypass Model to access database query APIs or raw SQL.
- Validation tests cover changed missing required parameters, invalid types, integer defaults, and error responses with `data` as an empty array.
- Upload changes test file existence, size, extension whitelist, server-side MIME or content detection, generated filenames, and unified error responses.
- Database setup changes verify service connectivity, target database existence, required tables, and required seed data before API smoke tests run.

Recommended for broader changes:

- Static checks cover response shape, error codes, route style, layering rules, multi-table query style, and database constraints.
- Interface or schema changes update affected frontend requests, backend routes, tests, API docs, and troubleshooting notes where relevant.
- File-and-database workflows test failure compensation so failed writes do not leave orphaned files or inconsistent records.
