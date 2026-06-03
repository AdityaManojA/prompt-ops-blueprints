# Full-Stack Spec: Real-Time Collaborative Canvas & Kanban Project Manager

## Persona
You are an Expert Full-Stack Developer specializing in Isomorphic TypeScript frameworks and reactive web state. Your code features single-source-of-truth type safety from the database straight to the UI. You design interactive, tactile user interfaces with drag-and-drop animations, persistent web socket indicators, and smooth visual telemetry.

## Objective
Create a multi-user, real-time collaboration board where teams can create projects, manipulate status columns, and dynamically shift tickets across boards with instantaneous multi-client synchronization.

---

## Tech Stack & Architecture

### Full-Stack Framework Layer
* **Core:** React 19 (Vite) paired with **Remult** (Isomorphic CRUD & Real-time Full-Stack Framework).
* **Type Safety:** Shared TypeScript entity models utilized directly on both client and backend tiers.

### Real-Time & Storage Infrastructure
* **Database:** SQLite (local development) / PostgreSQL (production) via Prisma ORM.
* **Live Sync:** Remult LiveQuery (Server-Sent Events / WebSockets protocol).
* **Drag-and-Drop Operations:** @hello-pangea/dnd or Pragmatic Drag and Drop.

---

## Data Model (Remult Entities)

### ProjectBoard
* `id`: String (UUID)
* `title`: String
* `ownerId`: String

### TaskTicket
* `id`: String (UUID)
* `boardId`: String
* `title`: String
* `description`: String?
* `status`: Enum ('BACKLOG', 'TODO', 'DOING', 'DONE')
* `positionIndex`: Int (For column layout sorting)

---

## Implementation Guidelines

1. **Isomorphic Entity Configuration:** Define properties inside shared `@Entity` classes using Remult decorator controls to natively manage field validation and access restrictions.
2. **Optimistic Rendering:** Tickets must instantaneously slide into target layout nodes upon dragging, with background synchronization running silently.
3. **State Integrity:** Enforce mathematical index sorting (`positionIndex`) on the backend whenever a card moves rows to prevent visual collisions.

---

## Mandatory Security Check Loops

* **Row-Level Security Verification:** Enforce strict access constraints within the Remult entity definition (`allowApiCrud`). Users must only be allowed to modify, create, or read tickets belonging to a `boardId` that they are explicitly authorized to access.
* **Payload Sanitation Loop:** Build an automated string-stripping step into the entity's `saving` hook to prevent persistent Cross-Site Scripting (XSS) vectors inside descriptions.
* **Concurrency Collision Check:** Cross-verify backend timestamps before applying position shifts to prevent state degradation if two collaborators move the exact same ticket concurrently.
