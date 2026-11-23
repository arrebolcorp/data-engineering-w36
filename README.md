# Data Engineering & Analytics Foundations (`data-engineering-w36`)

## Repository goal
This repository documents my transition and practice as a Data Science student building real skills as an **Analytics Engineer** and then jumping into **Data Engineering**. I work **11 hours per week** building projects in this repository, versioned on GitHub from `v0.1` to `Final`.

## Data Engineering Lifecycle & Approach
Rather than studying isolated tools, I connect each practice to the **data engineering lifecycle** (*Generation, Storage, Ingestion, Transformation, Serving*) and its **undercurrents** (*Security, Data Management, DataOps, Data Architecture, Orchestration, Software Engineering*), evaluating what problem a tool solves, what alternatives exist, and what it costs[cite: 2, 4].

## Three Core Pillars
- ***Fundamentals of Data Engineering* (Reis & Housley):** Systems thinking, lifecycle stages, architecture trade-offs, and cost awareness[cite: 2, 4].
- ***Data Engineering Design Patterns* (Konieczny):** Reusable *pipelines* (automated workflows that move and transform data), *idempotency* (running a job multiple times yields the same result without duplicate records), *CDC* (*Change Data Capture* — tracking row-level changes), incremental processing, event-driven flows, data contracts, and *Medallion* architecture[cite: 2, 4].
- ***Principles* (Dalio):** Systems over motivation, error logging, root-cause diagnosis, and continuous improvement (*Pain + Reflection = Progress*)[cite: 5, 6].

## Repository Structure
- `README.md` — Program goal, lifecycle approach, and repository map.
- `ADR-001.md` — Architecture Decision Record on starting with Git, Docker, and spreadsheet/Power Query profiling before complex *pipelines* (automated data workflows)[cite: 2, 4].
- `LEARNING_LOG.md` — Mistake-based learning log recording root causes and preventive rules[cite: 5, 6].
- `week1/` and `mongoapp-docker-p1/` — Weekly exercises and container labs (Docker / Docker Compose and MongoDB).
- `.gitignore` and `.env.example` — Secret exclusion rules for local `.env` files and placeholder environment templates.

## Security, Cloud Cost & Versioning Habits
- **Security:** Never commit real passwords, tokens, or `.env` files; keep local credentials in `.env` ignored by Git and use `.env.example` with placeholders.
- **Cloud Costs:** Use free tiers where available (such as MongoDB Atlas free tier), enable *Resource Monitor* from day one and *auto-suspend* on *warehouses* (central analytical stores) when starting Snowflake in Week 14 (Feb 22, 2027), and suspend or delete cloud resources when finished with a lab[cite: 4, 5].
- **Versioning & Scope:** Aim each week for a clean commit, updated `README.md`, an `ADR` when making a technical decision, an entry in `LEARNING_LOG.md`, and version tags (`v0.1` through `Final`)—trimming lesson breadth before cutting the weekly deliverable if time gets tight[cite: 5, 6].