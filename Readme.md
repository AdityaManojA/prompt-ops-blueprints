# 🧬 Agentic Architecture Specs & Prompt Blueprints

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](CONTRIBUTING.md)
[![IDE Support](https://img.shields.io/badge/Supports-Cursor%20%7C%20Windsurf%20%7C%20Antigravity%20%7C%20Claude%20Code-7057ff)](#-supported-ides--agentic-workflows)

Welcome to the ultimate repository for **Agent-First Software Engineering**. This repository contains a curated collection of structural Markdown (`.md`) blueprints and system specification prompts optimized for next-generation agentic IDEs, autonomous coding agents, and multi-agent developer workflows.

Instead of typing ambiguous instructions into a chat box, these blueprints are designed to be dropped directly into your local workspace as contextual specification files. Agentic models parse these multi-layered technical specs to build comprehensive **Implementation Plans**, manage parallel task agents, and interface securely with Model Context Protocols (MCPs) before touching a single line of code.

---

## 🏛️ Blueprints & Specs Catalog

Below is the complete index of architectural specifications, frontend skill specs, and workflow graphs included in this repository:

| Specification File | Tech Stack / Architecture | Target Application / Focus |
| :--- | :--- | :--- |
| **`nextjs-ai-saas.md`** | Next.js, AI / LLM APIs, Stripe, Tailwind | Full-stack specification for AI-powered Micro-SaaS platforms. |
| **`ecommerce-react-hono-cloudfare.md`** | React, Hono, Cloudflare Workers / Workers KV | Ethereal Atelier E-Commerce architecture & edge deployment spec. |
| **`supabase-sql-saas.md`** | Supabase, PostgreSQL, Next.js, RLS | Production SaaS spec with relational schema, migration scripts, and RLS policies. |
| **`nextjs-b2b-marketplace.md`** | Next.js, Multi-tenancy, Stripe Connect | Enterprise B2B marketplace architecture blueprint. |
| **`react-sql-bi-dashboard.md`** | React, SQL, Charting Engines | Data-dense Business Intelligence dashboard with real-time analytics. |
| **`remult-realtime-collab.md`** | Remult, Full-Stack JS / TS, WebSockets | Real-time collaborative workspace and live document editing platform. |
| **`sveltekit-headless-ecommerce.md`** | SvelteKit, Headless GraphQL / REST API | High-performance, storefront-driven headless e-commerce spec. |
| **`firebase-nosql-social.md`** | Firebase, Firestore NoSQL, Realtime DB | Real-time social application template with serverless security rules. |
| **`FronEnd-Dev-Designers.md`** | UI/UX, Design Systems, CSS/Tailwind | Specialized skill & prompt blueprint for frontend design engineering. |
| **`GRAPHIFY_WORKFLOW.md`** | DAG State Machines, Task Execution | Workflow graph orchestrator specification for agent task loops. |

---

## 📂 Repository Structure

```text
.
├── FronEnd-Dev-Designers.md          # Frontend & design system engineering skill spec
├── GRAPHIFY_WORKFLOW.md              # Agent task graph & execution orchestrator spec
├── README.md                         # Repository documentation
├── ecommerce-react-hono-cloudfare.md # Ethereal Atelier E-Commerce architecture
├── firebase-nosql-social.md          # Firebase-backed social web application spec
├── nextjs-ai-saas.md                # Full-stack AI Micro-SaaS specification
├── nextjs-b2b-marketplace.md         # B2B multi-tenant marketplace specification
├── react-sql-bi-dashboard.md         # SQL-driven BI & analytics dashboard spec
├── remult-realtime-collab.md         # Full-stack spec for real-time collaboration
├── supabase-sql-saas.md              # Supabase & PostgreSQL production SaaS blueprint
└── sveltekit-headless-ecommerce.md   # Headless e-commerce frontend architecture
```

---

## 🚀 How to Use These Blueprints

### 1. Integrate into Your Workspace
Copy the specification file corresponding to your project stack directly into your local project root or rules context folder:

```bash
# Example: Adding the AI SaaS spec to your active project
cp nextjs-ai-saas.md ./my-project/docs/architecture-spec.md
```

### 2. Prompting Your Agentic IDE
Point your Agentic IDE (Cursor, Windsurf, Antigravity, Claude Code, etc.) to the specification file as the single source of truth:

> *"Read `@docs/architecture-spec.md`. Step 1: Generate a step-by-step `implementation_plan.md` breaking down the core database schema and API routes required. Wait for my review before writing code."*

### 3. Workflow Execution Loop
1. **Plan Generation:** The agent parses schema constraints, API endpoints, and guardrails from the spec.
2. **Task Execution:** The agent executes code changes iteratively against the spec's requirements.
3. **Automated Verification:** The agent runs test suites, linting routines, and type checks prescribed by the blueprint.

---

## 💡 Best Practices for Agentic Development

* **Zero Assumptions:** Treat these spec files as immutable contracts. Update the spec file when requirements change rather than giving loose, chat-only instructions.
* **Context Budgeting:** Reference only the specific `.md` blueprint active in your current build context to preserve token budget and optimize agent reasoning.
* **Orchestrate Complex Tasks:** For multi-agent or multi-step execution workflows, combine stack specs with `GRAPHIFY_WORKFLOW.md` to enforce strict state dependencies and execution graphs.

---

## 🛠️ Supported IDEs & Agentic Workflows

This repository is optimized for:
* **Cursor** (`.cursorrules` or context `@files`)
* **Windsurf** (`.windsurfrules` or Cascade agent)
* **Google Antigravity** & Multi-agent IDEs
* **Claude Code** CLI & Autonomous Workflows
* **GitHub Copilot Workspace**

---

## 🤝 Contributing

Contributions of new architecture specs, security guardrails, or skill blueprints are welcome!

1. Fork the repository.
2. Add your specification file following standard structural headers (`# Architecture`, `# Tech Stack`, `# Database Schema`, `# API Specifications`, `# Security & Constraints`).
3. Submit a Pull Request with a short description of the stack.

---

## 📄 License

This project is licensed under the [MIT License](LICENSE).
