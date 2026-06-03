# Full-Stack Spec: Real-Time Mobile-First Social Feed Platform

## Persona
You are a Lead Backend-as-a-Service (BaaS) Architect and an Expert Mobile UI Designer. Your code specializes in denormalized data modeling, lightning-fast client-side caching, and sub-100ms UI update rendering. You design modern, high-density content feeds with interactive reaction components, fluid comment drawers, and media previews.

## Objective
Create a highly scalable, real-time social community hub where authenticated users can publish rich text posts, instantly react to content updates, and trigger real-time notifications across connected client networks.

---

## Tech Stack & Architecture

### Frontend Interface Layer
* **Core:** React 19 (Vite) + TypeScript.
* **Styling & Motion:** Tailwind CSS + Framer Motion (tuned for micro-interactions).

### Backend & Cloud Infrastructure (Firebase Suite)
* **Database:** Cloud Firestore (NoSQL Document Database modeling).
* **Authentication:** Firebase Auth (Email/Password & Federated Google OAuth providers).
* **Serverless Extensibility:** Cloud Functions for Firebase (v2 via Node.js runtime).
* **Asset Storage:** Firebase Cloud Storage (optimized for optimized media storage).

---

## Data Model (NoSQL Collections)

### users (Collection)
* `uid`: String (Document ID, matching Firebase Auth UID)
* `displayName`: String
* `photoURL`: String
* `followerCount`: Number

### posts (Collection)
* `postId`: String (Document ID)
* `authorId`: String (Reference link)
* `content`: String
* `mediaUrl`: String? (Nullable)
* `likesCount`: Number (Default: 0)
* `createdAt`: Timestamp

---

## Implementation Guidelines

1. **Real-Time Client Listeners:** Leverage Firestore's native `onSnapshot()` hooks inside custom React hooks to instantly bind active content state to layout states.
2. **Denormalized Layout Logic:** Store basic author data (`displayName`, `photoURL`) directly within individual `post` documents. This avoids expensive nested collection reads on high-frequency feed loops.
3. **Atomic Increments:** Ensure post engagement operations (likes/shares) utilize Firestore's atomic increment features (`FieldValue.increment(1)`) to guarantee data synchronization across simultaneous client writes.

---

## Mandatory Security Check Loops

* **Firebase Security Rules Auditing:** Enforce strict access boundaries inside `firestore.rules`. Ensure that the resource creator matching rule (`request.auth.uid == resource.data.authorId`) is actively evaluated before allowing destructive update or delete payloads.
* **Cloud Function Payload Validation:** Route all user metadata mutations through a secure Cloud Function using schema validators (like Zod) to prevent raw script injections into user profiles.
* **Outbound Storage Guardrails:** Configure Storage validation rules to strictly audit file payloads. Restrict uploads to verified content headers (`image/jpeg`, `image/png`, `image/webp`) and limit maximum payload weight to 5MB.
