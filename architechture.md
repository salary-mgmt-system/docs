# Architecture Overview

## System Overview

The Employee Salary Management System is a web application that enables HR managers to manage employee compensation data, track salary history, and analyze salary trends across the organization.

The application follows a client-server architecture.

## High-Level Architecture

React Frontend
|
| REST API
|
NestJS Backend
|
Service Layer
|
TypeORM
|
PostgreSQL

## Frontend

Technology:

* React
* TypeScript
* React Router
* TanStack Query
* Material UI
* Recharts

Responsibilities:

* Employee management UI
* Salary management UI
* Dashboard & analytics
* Insights interface

## Backend

Technology:

* NestJS
* TypeORM
* PostgreSQL

Responsibilities:

* Business logic
* Validation
* Analytics computation
* Salary history tracking
* Insights query processing

## Database

PostgreSQL is used as the primary data store.

Reasons:

* Relational data model
* Strong aggregation support
* Mature ecosystem
* Easy cloud deployment

## Scalability Considerations

Although the current dataset contains 10,000 employees, the design supports future growth through:

* Database indexing
* Server-side pagination
* Query optimization
* Separation of concerns
* Stateless backend services

## Key Design Decisions

1. Salary history stored separately from employee records.
2. Server-side pagination for employee listing.
3. Analytics generated via database aggregation queries.
4. Rule-based insights engine instead of external AI APIs.
