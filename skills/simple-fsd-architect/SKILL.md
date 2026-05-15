---
name: simple-fsd-architect
description: Design a lightweight FSD-inspired Vite React architecture using app, pages/views, widgets, entities, and shared without over-engineering.
---

# Simple FSD Architect

Use Simple FSD to make assignment code readable, not to create empty layers. In Vite React projects, `app/` owns bootstrapping and providers while real screen composition lives in `views/` or the existing project page layer.

## Default layers

`app/`

- app shell
- router setup
- providers
- global styles
- query client setup
- app-level bootstrapping

`views/`

- page-level composition
- route-level screen composition
- composition between widgets
- screen-specific adapters or view models when useful

Use `views/` by default for page-level screens. Use `pages/` only when the project already chose that convention.

`widgets/`

- meaningful page sections
- stateful UI blocks
- large domain-aware sections
- examples: `ProductListPanel`, `CartSummaryWidget`, `PaymentActionPanel`, `StoreFilterSection`

`entities/`

- domain API modules only
- domain-specific pure API functions
- domain-specific React Query hooks
- domain-specific query option factories and query keys
- API response types and domain types directly tied to that API
- mappers directly tied to that API response
- examples: `order`, `product`, `payment`, `store`, `customer`

`shared/`

- shared UI primitives
- common utilities
- common hooks
- common API client and fetchers
- common query helpers
- common formatters
- constants and config

## Rules

- Do not add folders just for architecture purity.
- Do not create `features/` by default.
- Prefer page-local code first.
- Promote code to widgets/entities/shared only when a real boundary appears.
- Keep the architecture readable for assignment reviewers.
- Let `app/` own bootstrapping, providers, router setup, and global setup.
- Keep real screen composition, data coordination, and widget wiring in `views/{route}/{RoutePage}.tsx` or the existing page layer.
- Never put common code in `entities/`.
- Move generic utilities to `shared/util`.
- Move common API clients and fetchers to `shared/api`.
- Move common query helpers to `shared/api` or `shared/lib` depending on the project convention.
- Move shared UI to `shared/ui`.
- Move common config and constants to `shared/config` or `shared/constants`.
- Treat page/view components importing API response types directly from API modules as a boundary smell. Prefer domain-facing types, view models, or view-local props.
- Treat Page/View components that interpret raw API errors, env/API key state, or toast payloads as a separation-of-concerns smell.
- If the team uses numbered FSD layers, document the logical layer names without renaming the actual project folders.

## View-model-aware structure

When API results do not match screen needs, prefer this flow:

1. Domain-specific pure API functions and query options live in `entities/`.
2. Domain mappers convert API response to domain model.
3. A view-level adapter converts domain data and failures to screen state.
4. Page/View renders explicit fields such as `currentWeather`, `forecastDays`, or `orderSubmitErrorMessage`.
5. Widgets own local interaction state where it belongs.

## Output format

### 1. Proposed folder structure

Show the exact initial structure. Include only useful folders and files.

### 2. App layer responsibilities

State what belongs in `app/`: app shell, providers, router setup, query client setup, global styles, and app-level bootstrapping.

### 3. Pages/views layer responsibilities

State what composes screens and connects widgets. Include any screen-specific view model or adapter.

### 4. Widgets layer responsibilities

List widgets that represent meaningful product sections.

### 5. Entities layer responsibilities

Map each domain to API-specific types, pure API functions, query option factories, hooks, query keys, and API response mappers.
Explicitly reject common utilities, common fetchers, common mappers, shared query helpers, shared UI, and global constants from `entities/`.

### 6. Shared layer responsibilities

List shared UI, common utilities, API client/fetchers, common query helpers, formatters, constants, and config.

### 7. What should stay page-local

Keep one-off composition, route-only state, screen-specific adapters, and simple markup local.

### 8. What should not be abstracted yet

Call out abstractions that would be premature.
Call out FSD boundary smells: API response type leakage into views, raw error handling in views, common code in `entities`, and mixed route/page/widget/entity files.

### 9. Migration path if the assignment grows

Explain when to introduce `features/`, more widgets, or deeper entity modules.
