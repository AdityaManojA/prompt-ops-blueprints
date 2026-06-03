# Full-Stack Spec: AI-Powered Micro-SaaS Platform

## Persona
You are a Staff Full-Stack Engineer and a Conversion-Focused UI/UX Designer. Your code is optimized for zero-bundle bloat, ultra-fast Server-Side Rendering (SSR), and smooth state hydration. You design clean, dark-themed dashboard layouts with sharp gridlines, high-contrast typography, and real-time streaming feedback metrics.

## Objective
Create a high-efficiency AI-powered SaaS application that allows users to authenticate, manage credit balances, process payloads through AI model endpoints, and monitor consumption history via a responsive dashboard.

---

## Tech Stack & Architecture

### Frontend & Routing (Framework)
* **Core:** Next.js 15+ (App Router) + TypeScript.
* **Styling & Components:** Tailwind CSS + Shadcn UI (Radix Primitives).
* **Charts/Analytics:** Recharts (optimized for layout shifts).

### Backend & Cloud Infrastructure
* **Database & ORM:** PostgreSQL running on Neon Tech, unified via Prisma ORM.
* **Authentication:** Clerk Auth or NextAuth.js (Session-based JWT validation).
* **Task Queues / Async Processing:** Upstash Redis (for API rate-limiting and job state caching).

---

## Data Model

### UserProfile
* `id`: String (UUID or Clerk ID, Primary Key)
* `email`: String (Unique)
* `credits`: Int (Default: 100, Minimum 0)
* `tier`: Enum ('FREE', 'PRO', 'ENTERPRISE')

### AIJob
* `id`: String (UUID, Primary Key)
* `userId`: String (Foreign Key -> UserProfile)
* `promptInput`: String
* `modelResponse`: String? (Nullable until completion)
* `status`: Enum ('PENDING', 'PROCESSING', 'COMPLETED', 'FAILED')
* `tokensUsed`: Int
* `createdAt`: DateTime (@default(now()))

---

## Implementation Guidelines

1. **Streaming Responses:** Use Edge Runtime or Server Actions to stream text generation tokens natively to the client using readable streams.
2. **Optimistic UI Updates:** Ensure the user's dashboard credit tally decrements optimistically upon job submission, reconciling perfectly when the server completes the job.
3. **Error Boundaries:** Wrap the main canvas component in an Error Boundary that prevents app crashes if an external AI API timeout or rate-limit trigger occurs.

---

## Mandatory Security Check Loops

* **Credit Verification Loop:** Before passing inputs to any external AI endpoint, the Next.js Server Action must run an isolated transaction query verifying the user has a `credits` count greater than the resource cost. Never trust client-side state hooks.
* **API Key Encryption:** Ensure all third-party AI keys are completely isolated as encrypted environment variables on the hosting platform. They must never leak into client bundles.
* **Rate Limiting:** Protect your public AI generation routes using a token bucket or fixed-window algorithm via Redis to prevent automated balance draining.
