---
name: abstraction-boundary-reviewer
description: Review frontend assignment code for separation of concerns, over-abstraction, unclear naming, view model boundaries, raw API/error leakage into views, and reviewer-readable data flow.
---

# Abstraction Boundary Reviewer

Use this when a frontend assignment review mentions unclear responsibilities, vague names, over-abstraction, confusing data flow, raw API/error leakage, or code that looks extensible but is hard to read.

## Core principle

For take-home assignments, reviewer-readable explicit structure beats generic architecture that only looks scalable. An abstraction is good only when it reduces understanding cost.

## Separation of concerns checklist

Flag as a smell when a Page/View component directly handles:

- raw API response shapes
- API key or environment availability decisions
- raw errors from API clients
- toast payload construction
- loader internals such as `PromiseSettledResult`
- domain mapping or business rule normalization
- unrelated section errors in one vague object

Prefer this flow:

1. API/loader layer fetches data and reports typed failures.
2. Mapper/adapter/view-model layer turns raw data and failures into screen state.
3. Page/View composes UI from explicit props and view model fields.
4. Widgets own local interactions and render user-visible states.

Ask: "Does this component need to know this error exists?"

## Over-abstraction checklist

Review generic wrappers such as:

- `{ data, error }`
- `Resource<T>`
- `Result<T>`
- `AsyncState<T>`
- generic `current`, `data`, `result`, or `resource` fields

Accept them only when they make multiple flows easier to understand. For one or two resources, prefer explicit domain names and a screen-specific view model.

Ask: "Did this abstraction reduce code and understanding cost, or did it hide product meaning?"

## Naming smell checklist

Flag names that are unclear without surrounding context:

- `current`
- `data`
- `result`
- `resource`
- `item`
- `state`
- `errorMessage` when several independent errors exist
- `currentErrorMessage` or `forecastErrorMessage` when the difference is not obvious

Prefer domain nouns:

- `currentWeather`
- `forecastDays`
- `currentWeatherErrorMessage`
- `forecastErrorMessageBySection`
- `weatherSectionErrors`
- `orderSubmitErrorMessage`
- `cartItemsByOptionKey`

## View model pattern

Use a view model when API loader output does not match what the screen should render.

Example:

```ts
type WeatherDetailViewModel = {
  currentWeather: CurrentWeather | null;
  forecastDays: DailyForecast[] | null;
  errors: WeatherSectionError[];
  toastErrors: WeatherToastError[];
};
```

The Page/View should not directly interpret `hasApiKey`, raw `error`, response envelopes, or loader settlement objects when an adapter can expose explicit screen state.

## Bad vs good examples

Bad:

```ts
weather.current
currentErrorMessage
forecastErrorMessage
Resource<Weather>
WeatherDetailPage decides whether API key errors create toast payloads
```

Good:

```ts
currentWeather
forecastDays
currentWeatherErrorMessage
weatherSectionErrors
WeatherDetailViewModel
mapWeatherDetailToViewModel(loaderResult)
```

## Test connection

Boundary problems often appear in tests:

- Page tests asserting raw toast payload JSON are too implementation-specific.
- Page tests asserting internal error IDs are too implementation-specific.
- Page tests should verify user-visible states and interactions.
- Mapper/adapter tests should verify raw response and error conversion.
- View model tests should verify section state combinations.

## Output format

### 1. Responsibility map

List what API/loader, mapper/adapter, Page/View, widgets, and shared UI currently know.

### 2. Separation of concerns issues

List raw data, raw error, env/config, toast payload, or business-rule leakage into the wrong layer.

### 3. Over-abstraction issues

List generic wrappers or structures whose understanding cost is higher than their value.

### 4. Naming smells

List vague names and propose domain-specific replacements.

### 5. View model recommendation

State whether a screen-specific view model is needed. If yes, propose its shape.

### 6. Test impact

Identify tests that should move from implementation detail assertions to user-visible state or pure adapter coverage.

### 7. Patch plan

Give the smallest safe refactor order. Prefer renaming and adapter extraction before architecture-wide rewrites.

### 8. README note

Draft the trade-off explanation if the assignment README should mention explicit view models over generic abstraction.
