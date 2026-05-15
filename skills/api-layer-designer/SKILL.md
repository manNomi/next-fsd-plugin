---
name: api-layer-designer
description: Design a domain API layer that separates pure API call functions, React Query hooks, query keys, API-bound domain types, mappers, and view-model adapters while keeping common code in shared.
---

# API Layer Designer

Use this when the assignment has API calls, mock APIs, domain responses, React Query, view-model adapters, or screen data-flow decisions.

## Preferred pattern

```text
entities/{domain}/{resource}/api/getResource.ts
entities/{domain}/{resource}/api/resourceOptions.ts
entities/{domain}/{resource}/api/useGetResource.ts
entities/{domain}/{resource}/api/keys.ts
entities/{domain}/{resource}/model/types.ts
entities/{domain}/{resource}/lib/mapper.ts
```

Example:

```text
entities/bank/stock/api/getStock.ts
entities/bank/stock/api/stockOptions.ts
entities/bank/stock/api/useGetStock.ts
entities/bank/stock/api/keys.ts
entities/bank/stock/model/types.ts
entities/bank/stock/lib/mapStock.ts
```

## Responsibilities

`getStock.ts`

- pure API call
- no React dependency
- reusable by React Query hooks, event handlers, or view-level loaders

`useGetStock.ts`

- React Query hook
- wraps domain query options
- defines `enabled` condition
- optionally defines `staleTime`, `retry`, `select`, `placeholderData`

`stockOptions.ts`

- query option factory
- reusable by `useQuery`, `prefetchQuery`, and router-level prefetch when the project uses it
- wraps pure API functions without React dependency
- should not include hook-only conditions like `enabled` when reused outside hooks

`keys.ts`

- query key factory
- avoids key duplication

`types.ts`

- domain model
- API response type if needed

`mapper.ts`

- converts API response to domain model
- keeps UI clean

View-model adapters, when needed:

- convert domain data, partial failures, and UI decisions into screen-ready state
- should use explicit domain names instead of generic `data`, `current`, or `resource`
- may live near `views/` when the shape is screen-specific

## When this is too much

For small assignments, use a flatter structure:

```text
entities/stock/api/getStock.ts
entities/stock/api/stockOptions.ts
entities/stock/api/useGetStock.ts
entities/stock/model/types.ts
```

Avoid adding mappers, key factories, adapters, or generic wrappers until the response shape, query count, or reuse justifies them.

## React Query design

When React Query is useful:

- Pure API functions fetch and map data.
- Query options reuse pure API functions.
- Hooks consume query options.
- Client widgets call hooks where the data is needed.
- The same query key must be used across hooks, prefetch, invalidation, and mutation updates.
- `staleTime`, retry, `enabled`, `select`, placeholder data, mutation, and invalidation must be deliberate.

## Entities vs shared boundary

`entities/` is only for API-adjacent domain modules.

Allowed in `entities/`:

- domain-specific pure API functions
- domain-specific React Query hooks
- domain-specific query option factories and query keys
- API response types and domain types directly tied to the API
- mappers directly tied to that API response

Forbidden in `entities/`:

- common utilities
- common formatters
- common fetch clients
- common query wrappers
- cross-domain helpers
- reusable UI
- global constants or config

Move common code to:

- `shared/util` for generic functions
- `shared/api` for API clients, fetchers, and common query helpers
- `shared/ui` for reusable UI
- `shared/config` or `shared/constants` for global config and constants

## Output format

### 1. Domain API inventory

List each domain/resource, endpoint or mock source, request params, and consumer.

### 2. Recommended file structure

Choose nested or flatter structure and show exact files.
Include query option files when React Query is used.
State which common files belong in `shared/` instead of `entities/`.

### 3. Pure API functions

Define function names, inputs, outputs, error behavior, and whether the function maps raw responses.

### 4. React Query hooks

Define hook names, location, query options, enabled conditions, stale time, retry, mutation, and invalidation where needed.

### 5. Query keys

Define key factories and key shape.

### 6. Types and mappers

Define API response types, domain model types, and mapping responsibilities.

### 7. View-model adapters

State whether raw data or errors need a screen-specific adapter before reaching Page/View components.

### 8. Component usage

Show which views/widgets call hooks, receive view models, or own local UI state.

### 9. What not to abstract

List wrappers, clients, mappers, hooks, or generics that are not needed yet.
Explicitly list any common utilities, fetchers, query helpers, constants, or UI that must not be placed in `entities/`.

### 10. Example code skeleton

```ts
export type StockResponse = {
  symbol: string;
  price: number;
  updatedAt: string;
};

export type Stock = {
  symbol: string;
  price: number;
  updatedAt: Date;
};

export const stockKeys = {
  all: ["stock"] as const,
  detail: (symbol: string) => [...stockKeys.all, symbol] as const,
};

export function mapStock(response: StockResponse): Stock {
  return {
    symbol: response.symbol,
    price: response.price,
    updatedAt: new Date(response.updatedAt),
  };
}

export async function getStock(symbol: string): Promise<Stock> {
  const response = await fetch(`/api/stocks/${symbol}`);

  if (!response.ok) {
    throw new Error("Failed to load stock");
  }

  return mapStock(await response.json());
}

export const stockOptions = {
  detail: (symbol: string) => ({
    queryKey: stockKeys.detail(symbol),
    queryFn: () => getStock(symbol),
    staleTime: 60_000,
  }),
};

import { useQuery } from "@tanstack/react-query";

export function useGetStock(symbol: string) {
  return useQuery({
    ...stockOptions.detail(symbol),
    enabled: symbol.length > 0,
  });
}
```
