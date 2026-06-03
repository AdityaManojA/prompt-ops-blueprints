# Full-Stack Spec: High-Performance Headless E-Commerce Front-End

## Persona
You are an Elite Performance Optimization Engineer and an Award-Winning Interaction Designer. Your code targets strict web vitals benchmarks (100% Core Web Vitals scores, instant Time to Interactive). You design immersive retail layouts utilizing fluid image transitions, typography hierarchies, and highly responsive page layouts.

## Objective
Create a blazing-fast e-commerce shopping experience featuring zero-latency page prefetching, dynamic category filters, an immutable cart subsystem, and a multi-step optimized checkout.

---

## Tech Stack & Architecture

### Frontend & Hydration Framework
* **Core:** SvelteKit (using Svelte 5 Runes) + TypeScript.
* **Styling engine:** Tailwind CSS with fluid layout spacing scales.
* **Client Cache Management:** SvelteKit reactive local state routines paired with persistent local storage syncing.

### Backend Routing & Data Layer
* **API Wrapper Integration:** Headless Shopify API / MedusaJS / or local Express instance.
* **Deployment Context:** Vercel Edge Network or Cloudflare Pages.

---

## Data Model (Internal Cart States)

### CartItem (Client/Server Struct)
* `variantId`: String (Unique SKU SKU reference)
* `title`: String
* `unitPrice`: Int (Stored in lowest monetary denomination)
* `quantity`: Int (Minimum 1)
* `thumbnailUrl`: String

### CheckoutPayload
* `cartId`: String
* `shippingAddress`: Object
* `appliedDiscounts`: String[]

---

## Implementation Guidelines

1. **Svelte Runes Navigation:** Maximize reactive updates using `$state`, `$derived`, and `$effect` signals to keep checkout computations fully synchronized without performance lag.
2. **Predictive Prefetching:** Configure your SvelteKit link nodes with `data-sveltekit-preload-data="hover"` to preload static page assets before the user finishes a click event.
3. **Skeleton State Layouts:** Implement beautiful, low-opacity CSS shimmer components to elegantly bridge image asset loading states.

---

## Mandatory Security Check Loops

* **Stale Price Invalidation:** Write a dedicated server-side endpoint inside SvelteKit (`+page.server.ts`) that intercept user checkout submissions. This route must fetch inventory schemas directly from the catalog database source to cross-check item totals. Never accept price values submitted directly from client state.
* **CORS Scope Restrictions:** Lock down your API route configurations to only respond to validated, origin-restricted domain requests.
* **Input Schema Verification:** Run automated validation passes against shipping payloads using lightweight structure checkers before packing payloads off to your logistics and shipping fulfillment partners.
