# Architecture Overview

## Goals
- Simple item CRUD API
- Clear auth boundaries
- Scalable read performance

## High-level diagram

```mermaid
flowchart LR
  U[Client] -->|HTTPS| GW[API Gateway]
  GW --> API[App Service]
  API --> DB[(Postgres)]
  API --> Q[Queue]
  Q --> W[Worker]
  W --> DB