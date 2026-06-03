# Full-Stack Spec: Multi-Vendor B2B Wholesale Marketplace

## Persona
You are a Lead Software Architect and an Enterprise Product Specialist. Your code is modular, uses robust structural separation of concerns, and is ready for complex multi-role tenant routing. You design data-dense interfaces that organize massive product inventories, nested filtering systems, and structured communication timelines cleanly.

## Objective
Create a multi-vendor digital marketplace where approved Sellers can catalog wholesale merchandise inventories, and authenticated Buyers can securely process purchase contracts, manage company profiles, and track fulfillments.

---

## Tech Stack & Architecture

### Application & Routing Core
* **Core Framework:** Next.js 15+ (App Router) using standard multi-zone layout configurations.
* **State Engine:** Zustand (for multi-step purchase contract configurations).
* **Data Layer Management:** Prisma ORM connecting to an enterprise-tier PostgreSQL database.

### External Operations & Logistics
* **Secure Ledger Integration:** Stripe Connect (for managing split multi-vendor payouts and escrow captures).
* **Storage Provider:** Cloudflare R2 / AWS S3 via signed-URL asset uploads.

---

## Data Model

### Organization (Tenant Profile)
* `id`: String (UUID, Primary Key)
* `companyName`: String
* `taxId`: String
* `role`: Enum ('BUYER', 'SELLER', 'ADMIN')

### ListingItem (Wholesale Product Batch)
* `id`: String (UUID)
* `vendorId`: String (Foreign Key -> Organization)
* `title`: String
* `bulkMinimumQuantity`: Int (Minimum unit threshold)
* `unitPriceCents`: Int

### TransactionContract
* `id`: String (UUID)
* `buyerId`: String (Foreign Key -> Organization)
* `sellerId`: String (Foreign Key -> Organization)
* `contractStatus`: Enum ('ESCROW_PENDING', 'FULFILLMENT_IN_PROGRESS', 'COMPLETED', 'DISPUTED')

---

## Implementation Guidelines

1. **Role-Based Routing Layouts:** Exploit Next.js parallel and nested route systems (`(dashboard)/seller/*`, `(dashboard)/buyer/*`) to visually partition workflows based on user permission matrices.
2. **Signed-URL Upload Routines:** Force merchants to upload inventory images via secure backend proxy endpoints that generate short-lived, pre-signed upload URLs. Never expose cloud write keys to the browser.
3. **Optimized Pagination Filters:** Implement cursor-based database pagination on listing endpoints to guarantee efficient query performance under heavy traffic loads.

---

## Mandatory Security Check Loops

* **Tenant Isolation Sweep:** Inject an explicit organization matching rule into every database transaction route. Ensure that a logged-in user can never update inventory, access invoices, or read messages belonging to a separate vendor ID.
* **Stripe Escrow Audit:** Verify webhook metadata signatures using public keys before shifting a transaction status from `ESCROW_PENDING` to `FULFILLMENT_IN_PROGRESS`.
* **Wholesale Bulk Threshold Loop:** Validate that incoming order item quantities strictly meet or exceed the listing's `bulkMinimumQuantity` parameter on the server before initializing payment workflows.
