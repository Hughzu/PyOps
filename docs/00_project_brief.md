# Project Brief: PyOps Framework & Domain Monitor

## 1. Executive Summary
The goal is to build **PyOps**, a lightweight, "Low-Stack" framework designed for SREs and DevOps engineers. It enables the rapid creation of internal tools and dashboards without the complexity of modern full-stack development (React, microservices, complex DBs).

The **pilot implementation** of this framework will be a **Domain Monitoring Dashboard** for a company. This tool will aggregate domain data from APIs, visualize costs and expiration dates, and highlight the urgency of automation compliance.

## 2. The Core Problem
* **Skill Gap:** SREs need to build tools but often lack the time or desire to maintain complex frontend frameworks (React/Vue) or heavy database servers (Postgres).
* **Visibility:** In the specific case of *Company*, there is a lack of visibility regarding owned domains. We do not know the full extent of the portfolio, the associated costs, or the expiration timelines.
* **Urgency:** Upcoming regulations shorten expiration windows, making manual renewal risky. We need a tool to prove the need for automation.

## 3. Proposed Solution: "PyOps" Framework
A "batteries-included" skeleton repository that provides a standardized way to build internal tools.

* **Philosophy:** "Locality of Behavior" (LoB). Everything needed to run the app is contained within the repo. No external build steps, no external database servers.
* **Deployment:** Docker-first. Easy to push to the cloud with a single persistent volume.
* **Maintainability:** Strong separation between the **Core** (framework engine) and **App** (business logic) to allow upstream updates.

## 4. The Pilot Feature: Domain Monitor
The first app built on PyOps will address the Company domain issue.

### Functional Requirements
1.  **Data Ingestion:** A cron job fetches domain lists from external APIs (Registrars).
2.  **grouping:** Logic to group domains by business unit or purpose (e.g., "Marketing", "Infra", "Legacy").
3.  **Cost Analysis:** Display accumulated costs per group.
4.  **Expiration Alerting:** Visual indicators for domains expiring soon (e.g., Red < 30 days).

## 5. Proposed Technical Stack (To be Challenged)

| Component | Proposal | Rationale |
| :--- | :--- | :--- |
| **Language** | **Python 3.11+** | The native language of Ops/SREs. |
| **Web Framework** | **FastAPI** | Modern, fast, async support, and auto-generated docs (Swagger). |
| **Frontend** | **HTMX + Jinja2** | Server-side rendering with simple interactivity. No JavaScript build pipeline. |
| **Styling** | **TailwindCSS** | Utility-first CSS (via CDN for simplicity in V1). |
| **Database** | **SQLite** | Single file database. Easy to backup, sufficient performance for internal tools. |
| **ORM** | **SQLAlchemy** | Standard Python ORM. |
| **Scheduler** | **APScheduler** | Integrated in-process cron manager (no need for external Celery/Redis). |
| **Container** | **Docker** | Multi-stage build (if needed), running as a non-root user. |

## 6. Questions for the Architect (BMAD Phase)
*Is this stack robust enough?*
* **Concurrency:** Will SQLite lock up if the Cron job writes while the User reads?
* **Security:** Is "Docker Volume" sufficient for persistence in a cloud environment?
* **Frontend:** Is HTMX enough for complex tables (sorting/filtering domain lists)?
* **Scalability:** What happens if we track 10,000 domains?
