---
name: commerce-order-flow-auditor
description: Analyze or review commerce order assignments with menu/catalog, item detail, option selection, cart grouping, order submit, order completion, pricing, payload correctness, duplicate-submit prevention, Toast/error behavior, and API contract checks.
---

# Commerce Order Flow Auditor

Use this for product-focused commerce/order assignments: menu pages, item detail pages, option selectors, carts, checkout/order submit, and order completion screens. This skill is intentionally domain-specific, but it must not copy private assignment text. Generalize to reusable order-flow patterns.

## Core principle

Order flows fail when state transitions, pricing, option validation, or payload shape drift apart. Audit the implementation as a small state machine, not as isolated screens.

## What to inspect

- Catalog/category API and menu filtering.
- Item detail API and item-not-found behavior.
- Option API and option ordering.
- Option type behavior: single required choices, optional single choices, multi-choice min/max choices, icon/grid variants, prices, labels, and defaults.
- Cart storage and grouping rules.
- Quantity update, remove, empty cart, CTA count, and total price.
- Order submit payload and duplicate-submit prevention.
- Order complete lookup, missing order behavior, and restart/reset assumptions.
- Toast/error messages and disabled/pending states.
- Manual QA across mobile, tablet, desktop, touch, keyboard, and slow network.

## Commerce rules

- Preserve option display order from the API unless the assignment explicitly says otherwise.
- Normalize option labels before cart grouping so the same item plus the same option set groups together.
- Include option prices, base item price, and quantity in total price calculations.
- Treat payload correctness as Critical: item id, quantity, option id, selected labels, and total price must match the API contract.
- Disable or guard submit actions while pending.
- Surface API errors to users with Toast, alert, or the existing project pattern.
- Do not hide option validation in JSX if it becomes complex. Extract pure validation or mapper logic.
- Prefer existing design system, bottom sheet, toast, button, list, and icon components when provided.

## Per-screen decision checklist

- Menu/list: category source, initial category, empty list behavior, image fallback, cart CTA count/price wording.
- Detail/options: option defaults, required choice behavior, optional select empty state, bottom sheet behavior, min/max validation, Toast copy.
- Cart: grouping key, option order in labels, quantity update rules, remove behavior, empty cart CTA, total count/price.
- Submit: payload shape, pending guard, duplicate submit prevention, success navigation, API error feedback.
- Complete: order lookup source, missing order fallback, total display, return-to-menu behavior, restart/reset assumptions.

## Output format

### 1. Order flow inventory

List pages, routes, user intents, and required transitions from catalog to completion.

### 2. API contract map

Map each required API to request shape, response shape, error cases, caller, and trusted source of truth.

### 3. Option rule matrix

Create a matrix with columns: option type, required, single/multi, min, max, labels, prices, icons, default, validation, UI component.

### 4. Cart grouping and pricing rules

Define grouping key, quantity behavior, remove behavior, total count, total price, and rounding/formatting rules.

### 5. State transition map

Describe idle, loading, selected, invalid, pending, success, error, empty, and not-found states for each page.

### 6. Failure / Toast / disabled checks

List API 400/404, network failure, slow response, duplicate click, invalid option selection, stale order lookup, and expected user feedback.

### 7. Page acceptance checklist

List acceptance checks per page: menu, detail/options, cart, submit, complete. Include the decision checklist result for each page.

### 8. Test scenarios

List high-value tests for option validation, cart grouping, price calculation, order payload, duplicate submit, API error, and completion lookup.

### 9. README assumptions and trade-offs

Draft assumptions and trade-offs around persistence, stale order data, ignored tests, option defaults, and incomplete polish.

### 10. Patch priorities

Order fixes by Critical, Important, and Minor. Pricing, payload, required validation, and duplicate submit are Critical.
