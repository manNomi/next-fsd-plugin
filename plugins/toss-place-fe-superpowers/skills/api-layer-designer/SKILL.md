---
name: api-layer-designer
description: Design an API layer that separates pure API call functions, React Query hooks, query keys, domain types, and mappers under the entities layer.
---

# API Layer Designer

Use this when the assignment has API calls, mock APIs, domain responses, React Query, Server Component fetching, or React Query hydration.

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
- usable in Server Components
- usable inside React Query hook

`useGetStock.ts`

- client-only React Query hook
- wraps shared query options
- defines `enabled` condition
- optionally defines `staleTime`, `retry`, `select`, `placeholderData`

`stockOptions.ts`

- query option factory
- reusable by `prefetchQuery`, `useQuery`, and hydration
- wraps pure API functions without React dependency
- should not include hook-only conditions like `enabled` when the same options are used by server prefetch

`keys.ts`

- query key factory
- avoids key duplication

`types.ts`

- domain model
- API response type if needed

`mapper.ts`

- converts API response to domain model
- keeps UI clean

## When this is too much

For small assignments, use a flatter structure:

```text
entities/stock/api/getStock.ts
entities/stock/api/stockOptions.ts
entities/stock/api/useGetStock.ts
entities/stock/model/types.ts
```

Avoid adding mappers or key factories until the response shape, query count, or reuse justifies them.

## Hydration-first query design

When React Query is useful, design for hydration first:

- Pure API functions fetch and map data.
- Query options reuse pure API functions.
- Server `views/*Page` components prefetch query options and wrap interactive sections in `HydrationBoundary`.
- Client widgets call hooks wherever the data is needed.
- The same query key must be used for prefetch and client hook consumption.

This maximizes local data access through hooks while keeping server prefetch, cache policy, and domain mapping centralized.

## Output format

### 1. Domain API inventory

List each domain/resource, endpoint or mock source, request params, and consumer.

### 2. Recommended file structure

Choose nested or flatter structure and show exact files.
Include query option files when React Query or hydration is used.

### 3. Pure API functions

Define function names, inputs, outputs, cache options, and error behavior.
For Next.js, state whether `fetch` uses `revalidate`, `force-cache`, or `no-store`.

### 4. React Query hooks

Define hook names, client-only location, query options, enabled conditions, stale time, retry, mutation, and invalidation where needed.

### 5. Query keys

Define key factories and key shape.

### 6. Types and mappers

Define API response types, domain model types, and mapping responsibilities.

### 7. Server Component usage

Show which pure functions or query options can be called on the server and whether `prefetchQuery` plus `HydrationBoundary` is recommended.

### 8. Client Component usage

Show which hooks are used from Client Components and why.

### 9. What not to abstract

List wrappers, clients, mappers, hooks, or generics that are not needed yet.

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

export const stockOptions = {
  detail: (symbol: string) => ({
    queryKey: stockKeys.detail(symbol),
    queryFn: () => getStock(symbol),
    staleTime: 30_000,
  }),
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

"use client";

import { useQuery } from "@tanstack/react-query";

export function useGetStock(symbol: string) {
  return useQuery({
    ...stockOptions.detail(symbol),
    enabled: symbol.length > 0,
  });
}
```
