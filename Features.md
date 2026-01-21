# Demo Feature Ideas (Windsurf)

## Solution overview (high level)

This repository is a .NET Aspire solution with:
- App orchestration: [src/eShop.AppHost/Program.cs](cci:7://file:///Users/pathenk/repo/windsurf-pov/eShop-windsurf/src/eShop.AppHost/Program.cs:0:0-0:0) (Aspire, Redis, RabbitMQ, Postgres/pgvector)
- Web frontend: [src/WebApp](cci:9://file:///Users/pathenk/repo/windsurf-pov/eShop-windsurf/src/WebApp:0:0-0:0) (Blazor/Razor Components, Interactive Server, OIDC auth)
- APIs / services:
  - [src/Catalog.API](cci:9://file:///Users/pathenk/repo/windsurf-pov/eShop-windsurf/src/Catalog.API:0:0-0:0) (Minimal APIs with v1/v2, semantic search via embeddings, pgvector)
  - [src/Ordering.API](cci:9://file:///Users/pathenk/repo/windsurf-pov/eShop-windsurf/src/Ordering.API:0:0-0:0) (Minimal APIs, MediatR pipeline, auth required)
  - [src/Basket.API](cci:9://file:///Users/pathenk/repo/windsurf-pov/eShop-windsurf/src/Basket.API:0:0-0:0) (gRPC)
  - [src/Identity.API](cci:9://file:///Users/pathenk/repo/windsurf-pov/eShop-windsurf/src/Identity.API:0:0-0:0), [src/Webhooks.API](cci:9://file:///Users/pathenk/repo/windsurf-pov/eShop-windsurf/src/Webhooks.API:0:0-0:0)
  - background processors: [src/OrderProcessor](cci:9://file:///Users/pathenk/repo/windsurf-pov/eShop-windsurf/src/OrderProcessor:0:0-0:0), [src/PaymentProcessor](cci:9://file:///Users/pathenk/repo/windsurf-pov/eShop-windsurf/src/PaymentProcessor:0:0-0:0)
- Infrastructure: Redis, RabbitMQ, Postgres (including pgvector)

This mix is well-suited for small demo slices: UI, API, auth, messaging, and distributed concerns.

---

## Candidate demo features (small, well-scoped)

### 1) Improve catalog pagination UI (quick win)
- Goal: avoid rendering all page links; use a windowed pagination (e.g. `1 … 4 5 6 … n`).
- Scope: UI only.
- Touch points:
  - [src/WebApp/Components/Pages/Catalog/Catalog.razor](cci:7://file:///Users/pathenk/repo/windsurf-pov/eShop-windsurf/src/WebApp/Components/Pages/Catalog/Catalog.razor:0:0-0:0) (`GetVisiblePageIndexes`)
- Demo value: small refactor + immediate UI impact.

### 2) Add catalog sorting (UI + API light)
- Goal: add a `sort` query parameter (`name`, `priceAsc`, `priceDesc`) and a UI dropdown.
- Scope: small API change + small UI change.
- Touch points:
  - [src/Catalog.API/Apis/CatalogApi.cs](cci:7://file:///Users/pathenk/repo/windsurf-pov/eShop-windsurf/src/Catalog.API/Apis/CatalogApi.cs:0:0-0:0) ([GetAllItems](cci:1://file:///Users/pathenk/repo/windsurf-pov/eShop-windsurf/src/Catalog.API/Apis/CatalogApi.cs:122:4-158:5))
  - [src/WebApp/Components/Pages/Catalog/Catalog.razor](cci:7://file:///Users/pathenk/repo/windsurf-pov/eShop-windsurf/src/WebApp/Components/Pages/Catalog/Catalog.razor:0:0-0:0) (query param + UI)
  - possibly catalog search component used by the page (`CatalogSearch`)
- Demo value: cross-project change (API + frontend) with clear acceptance criteria.

### 3) Stock / out-of-stock badge + disable add-to-cart when unavailable
- Goal: show stock status and prevent adding when `AvailableStock == 0`.
- Scope: UI only (or UI + minor styling).
- Touch points:
  - [src/WebApp/Components/Pages/Item/ItemPage.razor](cci:7://file:///Users/pathenk/repo/windsurf-pov/eShop-windsurf/src/WebApp/Components/Pages/Item/ItemPage.razor:0:0-0:0)
  - possibly listing component (`CatalogListItem`) if you also want badges in the catalog grid
- Demo value: product-like UX improvement, easy to validate manually.

### 4) Cart: explicit remove item button + better empty state
- Goal: add a dedicated "Remove" action (in addition to quantity update).
- Scope: UI + BasketState interaction.
- Touch points:
  - [src/WebApp/Components/Pages/Cart/CartPage.razor](cci:7://file:///Users/pathenk/repo/windsurf-pov/eShop-windsurf/src/WebApp/Components/Pages/Cart/CartPage.razor:0:0-0:0)
  - basket-related services wired in [src/WebApp/Extensions/Extensions.cs](cci:7://file:///Users/pathenk/repo/windsurf-pov/eShop-windsurf/src/WebApp/Extensions/Extensions.cs:0:0-0:0)
- Demo value: small UI enhancement, simple workflow demonstration.

### 5) Checkout: add one custom validation rule
- Goal: add a focused rule (e.g. allowlist countries, zip code format, etc.).
- Scope: one file change.
- Touch points:
  - [src/WebApp/Components/Pages/Checkout/Checkout.razor](cci:7://file:///Users/pathenk/repo/windsurf-pov/eShop-windsurf/src/WebApp/Components/Pages/Checkout/Checkout.razor:0:0-0:0) (`PerformCustomValidationAsync`)
- Demo value: demonstrates validation and UX feedback.

### 6) Orders: add a details page (end-to-end)
- Goal: click an order in the list and navigate to a details view.
- Scope: new page + use existing API endpoint.
- Touch points:
  - UI: [src/WebApp/Components/Pages/User/Orders.razor](cci:7://file:///Users/pathenk/repo/windsurf-pov/eShop-windsurf/src/WebApp/Components/Pages/User/Orders.razor:0:0-0:0) + new Razor component page
  - API already exists: [src/Ordering.API/Apis/OrdersApi.cs](cci:7://file:///Users/pathenk/repo/windsurf-pov/eShop-windsurf/src/Ordering.API/Apis/OrdersApi.cs:0:0-0:0) ([GetOrderAsync](cci:1://file:///Users/pathenk/repo/windsurf-pov/eShop-windsurf/src/Ordering.API/Apis/OrdersApi.cs:79:4-90:5))
  - client: `OrderingService` (registered in [src/WebApp/Extensions/Extensions.cs](cci:7://file:///Users/pathenk/repo/windsurf-pov/eShop-windsurf/src/WebApp/Extensions/Extensions.cs:0:0-0:0))
- Demo value: full vertical slice (routing + auth + API client + UI state).

### 7) Security/logging hardening for order creation (API only, focused)
- Goal: ensure sensitive payment data cannot leak into logs/telemetry.
- Scope: tighten logging/payload handling around order creation.
- Touch points:
  - [src/Ordering.API/Apis/OrdersApi.cs](cci:7://file:///Users/pathenk/repo/windsurf-pov/eShop-windsurf/src/Ordering.API/Apis/OrdersApi.cs:0:0-0:0) ([CreateOrderAsync](cci:1://file:///Users/pathenk/repo/windsurf-pov/eShop-windsurf/src/Ordering.API/Apis/OrdersApi.cs:117:4-167:5))
  - potentially MediatR pipeline behaviors (logging behavior)
- Demo value: security best practices, easy to explain.

### 8) Chatbot: graceful fallback + feature flag
- Goal: if AI is not configured, provide a better UX (feature flag + fallback suggestions).
- Scope: UI + config.
- Touch points:
  - [src/WebApp/Components/Chatbot/Chatbot.razor](cci:7://file:///Users/pathenk/repo/windsurf-pov/eShop-windsurf/src/WebApp/Components/Chatbot/Chatbot.razor:0:0-0:0)
  - [src/WebApp/Extensions/Extensions.cs](cci:7://file:///Users/pathenk/repo/windsurf-pov/eShop-windsurf/src/WebApp/Extensions/Extensions.cs:0:0-0:0) ([AddAIServices](cci:1://file:///Users/pathenk/repo/windsurf-pov/eShop-windsurf/src/WebApp/Extensions/Extensions.cs:93:4-108:5))
  - [src/eShop.AppHost/Program.cs](cci:7://file:///Users/pathenk/repo/windsurf-pov/eShop-windsurf/src/eShop.AppHost/Program.cs:0:0-0:0) (`useOpenAI`, `useOllama`)
- Demo value: configuration-driven behavior + good “before/after”.

---

## Recommended demo backlog (2–3 features)

### A) Quick win: catalog pagination UI
- Low risk
- Very visible

### B) End-to-end slice: orders details page
- Demonstrates routing, auth, API calls, UI state changes

### C) Cross-cutting slice: chatbot feature flag + fallback
- Demonstrates config + UX + service wiring