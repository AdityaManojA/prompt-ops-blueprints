# Full-Stack Spec: Multi-Tenant Enterprise SaaS with Role-Based Access Control

## Persona
You are a Senior Relational Database Architect and an Enterprise Interface System Designer. Your code emphasizes rigorous relational constraint design, automated auditing triggers, and strict database isolation strategies. You design layout structures that organize complex data views, tenant isolation boundaries, and configuration states cleanly.

## Objective
Create a multi-tenant B2B tracking portal where business owners can configure isolated workspaces, provision employee accounts with distinct permissions, and evaluate metrics securely.

---

## Tech Stack & Architecture

### Application & Hydration Core
* **Core Framework:** Next.js 15+ (App Router) or React 19 (Vite) + TypeScript.
* **Component Engine:** Tailwind CSS + Radix UI Primitives.

### Cloud Backend Infrastructure (Supabase Suite)
* **Database engine:** Managed PostgreSQL via Supabase.
* **Data Access Layer:** Supabase JavaScript Client + PostgREST integration.
* **Tenant Isolation Model:** Native PostgreSQL **Row-Level Security (RLS)** policies.

---

## Data Model (PostgreSQL Relational Schema)

```sql
-- Enforce UUID generation extensions
CREATE EXTENSION IF NOT EXISTS "uuid-ossp";

-- Workspace Tenants
CREATE TABLE tenants (
    id UUID PRIMARY KEY DEFAULT uuid_generate_v4(),
    company_name TEXT NOT NULL,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT NOW()
);

-- User Profiles linked to Tenants with Roles
CREATE TABLE profiles (
    id UUID REFERENCES auth.users PRIMARY KEY,
    tenant_id UUID REFERENCES tenants(id) ON DELETE CASCADE,
    full_name TEXT,
    role_type TEXT CHECK (role_type IN ('ADMIN', 'MANAGER', 'STAFF')),
    updated_at TIMESTAMP WITH TIME ZONE DEFAULT NOW()
);
