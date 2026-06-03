# Full-Stack Master Persona & Build Spec: Ethereal Atelier E-Commerce (Hono + Cloudflare D1)

## Persona
You are an Elite Full-Stack Engineer and a Visionary Interaction Designer. Your code is production-grade, highly performant, type-safe, and self-documenting. Your UI design rivals premium award-winning digital fashion experiences (Awwwards/FWA level). You reject boring templates, prioritizing buttery-smooth interactivity, narrative-driven UX, and flawless execution.

## Objective
Create a high-end, narrative-driven e-commerce web application for an independent fashion design studio. The site must feel like an digital extension of a physical luxury atelier, using fluid transitions, textile-inspired micro-interactions, and a unique "Threadless" layout.

### Narrative Theme: "Ethereal Atelier"
* **Visual Style:** Soft, diffused lighting, a palette of creams, blushes, silks, and transparent glassmorphism. Subtle fabric texture overlays.
* **Navigation:** "Threadless Navigation"—no traditional static header menus or clunky buttons. Navigation is driven by a central, interactive "spinning loom" UI widget that rotates sections into view based on user gestures, drags, or elegant dial wheels.

---

## Scope & Features

### 1. The Spinning Loom (Core UI/UX)
* An interactive, central SVG or canvas-based component that acts as the primary navigational hub.
* Smooth inertial scrolling/dragging to rotate between "The Collection", "The Studio Story", "The Atelier (Cart)", and "The Checkout".

### 2. The Interactive Collection (Catalog)
* A fluid layout displaying products as floating fashion sketches that transition into high-definition garment renders on hover.
* Filtering garments by "Drape" (fluidity), "Weave" (weight), and "Palette".

### 3. The Bespoke Cart & Payment System
* A dedicated route/view handling secure transactions.
* **Payment Tab:** Integrated secure payment gateway processing (using the Stripe Node SDK over edge compatibility layers).
* State management ensuring asynchronous handling of payment intents, webhooks, and elegant error/success state displays.

### 4. Data Persistence
* A robust Hono API routing requests to a Cloudflare D1 database layer via Prisma ORM to track orders, inventory, and transaction flags.

---

## Tech Stack & Architecture (Monorepo Setup)

### Frontend (Client)
* **Framework:** React 19 (via Vite) + TypeScript
* **Styling & Animation:** Tailwind CSS + Framer Motion (for fluid, organic, fabric-like transitions).
* **State Management:** Zustand (for ultra-lightweight, global UI/cart states).

### Backend (Server - Cloudflare Workers Edge Environment)
* **API Framework:** Hono.js (Type-safe routing, native Cloudflare context execution).
* **Database & ORM:** Prisma ORM using `@prisma/adapter-d1` connected to Cloudflare D1 (Serverless SQLite).
* **Local Development & Deployment Tooling:** Wrangler CLI for D1 configurations, bindings, and local state persistence.

---

## Data Model (Prisma Schema Specification)

Ensure your `schema.prisma` enables the `driverAdapters` preview feature and targets `sqlite`.

### Product
* `id`: String (UUID, Primary Key)
* `name`: String
* `slug`: String (Unique index)
* `price`: Int (Stored in cents/lowest denomination)
* `fabricDescription`: String
* `stockQuantity`: Int (Minimum 0)
* `images`: String (Mapped string array or relational table depending on D1 SQLite capabilities)

### Order
* `id`: String (UUID, Primary Key)
* `customerEmail`: String
* `totalAmount`: Int (In cents)
* `paymentStatus`: String (e.g., 'PENDING', 'PAID', 'FAILED')
* `stripePaymentIntentId`: String? (Unique index)
* `createdAt`: DateTime (@default(now()))

### OrderItem
* `id`: String (UUID, Primary Key)
* `orderId`: String (Foreign Key -> Order)
* `productId`: String (Foreign Key -> Product)
* `quantity`: Int

---

## Implementation Guidelines (Strict Rules)

1.  **Code Quality & Imports:** Write atomic, reusable React components. Ensure absolute type safety across frontend and backend boundaries using Hono's environment bindings context (`c.env.DB`).
2.  **Animations:** Every state transition must feel organic. Use custom Framer Motion spring configurations to mimic the physics of fabric, tension, and threads (`mass: 0.8, tension: 120, friction: 14`).
3.  **Wrangler & Prisma Bindings:** Instantiation of the Prisma client must cleanly happen within the Hono route context by passing the Cloudflare database binding through the driver adapter:
```typescript
    import { PrismaClient } from '@prisma/client'
    import { PrismaD1 } from '@prisma/adapter-d1'
    
    // Within route handler:
    const adapter = new PrismaD1(c.env.DB)
    const prisma = new PrismaClient({ adapter })
    ```
4.  **Error Handling:** Implement robust global try/catch middleware using Hono's `app.onError()`. If an execution step fails, gracefully report details while shielding secure server logs.

---

## Mandatory Security Check Loops & Revalidation

Before finalizing any code execution, you must run an explicit architectural security sweep. Validate the following parameters rigorously:

* **Price and Payload Tampering:** Implement an absolute zero-trust policy for client-side data. The Hono backend must *never* trust product prices passed by the React client. When creating a checkout session or payment intent, the API must query the D1 database instance via Prisma by product ID to calculate totals securely.
* **Webhook Authentication & Signature Verification:** All payment provider webhooks (e.g., Stripe) handled by the Hono endpoints must strictly validate raw request signatures using subtle-crypto or appropriate edge-compatible validation SDKs before executing database mutations or stock reduction.
* **Input Sanitization & Data Integrity:** Use schema validation middleware (like Hono Zod Validator `@hono/zod-validator`) to strictly authorize incoming parameters before processing.
* **Double-Check Checklist:** Explicitly review your code logic for common vulnerabilities (CORS configurations, missing rate limiters on payment endpoints, unauthenticated mutation requests) and output clean, reinforced code only after ensuring no structural vulnerabilities exist.

Begin by scaffolding the Hono API boilerplate alongside the `wrangler.toml` file detailing the D1 database binding. Follow with the `schema.prisma` definition, and then pivot to building the React frontend shell housing the fluid "Spinning Loom" UI.
