# AI Usage Documentation

This document outlines how AI-assisted engineering was leveraged during the design, development, and testing of the Employee Salary Management System. 

In this project, AI was utilized as a **pair programmer and architect**, collaborating with the engineer to build a production-quality, fully-tested fullstack system.

---

## 1. Overview of AI Tools & Interaction

- **ChatGPT (OpenAI)**: Leveraged for the comprehensive **project planning, iteration breakdown, and initial structural/architectural mapping**.
- **Claude (Anthropic) & Gemini (Google)**: Leveraged for the **hands-on codebase implementation, feature engineering, styling/UX development, test design, lint resolution, and CI/CD setup**.
- **Role**: Staff Engineer & Architect.
- **Workflow**:
  - Planning implementation details and checklists step-by-step.
  - Automated analysis of TypeScript compile-time checks, ESLint rules, and test coverage outputs.
  - Pair-programming updates to source code, styling modules, test mock integrations, and documentation.

---

## 2. Architectural Design & Database Modeling

AI assisted in defining a clean, normalized relational model with a strong focus on data auditability and database scaling:
- **Normalization**: Separating `Employee` master records, `Salary` (current state), and `SalaryHistory` (audit trail log) to prevent table bloat and lock contention during updates.
- **Index Optimization**:
  - Unique indexes on `employee_code` and `email`.
  - Non-unique search/filter indexes on `department` and `country`.
  - Composite index on `(employee_id, is_current)` and a partial unique index on `(employee_id) WHERE is_current = true` to strictly enforce a single active salary record per employee at the database schema level.

---

## 3. Fullstack Code Generation & Implementation

AI-assisted generation was used to accelerate boilerplate creation while maintaining clean boundaries:
- **Backend (NestJS)**: Scaffolding DTO validations (`class-validator`), controller routes, Swagger documentation decorators (`@ApiProperty`), and TypeORM repositories.
- **Frontend (React)**: Constructing styled-components layout definitions, React Router bindings, TanStack query hooks, and reusable visual states (`ErrorPanel`, `EmptyState`).
- **Seeder Engine**: Building a bulk-insert seeder for 10,000 employees using chunks of 1,000 records to respect PostgreSQL parameter limits and maintain memory limits.

---

## 4. Linting, Quality Checks, & Type Safety

During development, compile checks and ESLint flagged several lint errors. AI assisted in reviewing and resolving these:
- **Type Safety**: Fixed unsafe assignments of `any` types in speculative tests (`http-exception.filter.spec.ts` and others) by defining explicit interfaces or using standard TypeScript assertion techniques.
- **React 19 Compatibility**: Checked styled-components transient props (`$isSelected` and `$isMobile`) to prevent custom styling flags from bleeding down into DOM elements.

---

## 5. Test Engineering & 100% Code Coverage

One of the highlights of this project is achieving **100% test coverage** on both the frontend and backend. AI played a crucial role here:
- **Mock Generation**: Structured mock responses for nested database transactions and queries.
- **Edge-Case Identification**: Generating test cases for invalid salary inputs (negative numbers, empty base values), database failure scenarios, and empty search results.
- **Enforcement**: Integrating Jest (backend) and Vitest (frontend) coverage limits to fail CI builds if coverage drops below the required quality thresholds.

---

## 6. Tradeoffs & Engineering Decisions

AI-assisted documentation helped outline several key trade-offs in the design:
1. **Rule-Based Insights Engine vs. LLM Integration**: Choosing a deterministic regex/SQL query parser to guarantee correctness, security, and low latency for standard HR queries, avoiding cost and non-deterministic text outputs from external APIs.
2. **In-Memory vs. In-Database Analytics Aggregations**:
   - *Current Implementation*: Fetches active employee/salary datasets into node application memory to compute KPIs, median calculations, and bracket distribution.
   - *Tradeoff*: Safe and reliable for 10,000 records, but would hit memory limitations at 100,000+. A future improvement would shift median computation (`PERCENTILE_CONT`) and group aggregations directly onto the database engine.
