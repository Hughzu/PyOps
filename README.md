# PyOps

**The "Low-Stack" Framework for DevOps & SREs.**
Build internal dashboards, monitor APIs, and automate tasks without the complexity of a full-blown frontend/backend stack.

![Python](https://img.shields.io/badge/Python-3.11+-blue.svg) ![HTMX](https://img.shields.io/badge/HTMX-Frontend-orange.svg) ![Docker](https://img.shields.io/badge/Docker-Ready-2496ED.svg) ![SQLite](https://img.shields.io/badge/SQLite-Built--in-lightgrey.svg)

## Core Philosophy

As SREs or Ops engineers, we often need to visualize data (cloud costs, certificate expirations, infra metrics) or trigger maintenance scripts. We shouldn't have to configure React, Webpack, Postgres, and Redis just to display three tables.

**PyOps** is a "Locality of Behavior" (LoB) boilerplate designed for speed and maintainability:

* **Python Backend:** FastAPI (Modern, fast, and robust).
* **HTMX Frontend:** High-level interactivity using HTML attributes. No complex JavaScript build steps.
* **SQLite Database:** A full SQL database in a single file. Zero maintenance, easy backups.
* **Integrated Cron:** Schedule your data fetching scripts directly within the application code.
* **Docker First:** One image, one volume. Ready to deploy anywhere.

## The Stack

* **Web Framework:** FastAPI + Jinja2 Templates
* **Interactivity:** HTMX
* **Styling:** TailwindCSS (via CDN for simplicity) or Bootstrap
* **Database:** SQLite + SQLAlchemy (Async)
* **Scheduling:** APScheduler

## Project Structure (WIP)

PyOps is designed as a **skeleton you own**, not just a library you install. To ensure you can easily pull updates from this framework while keeping your custom implementation private, we strictly separate the "Core" from the "App".

```text
pyops/
├── core/                # ⛔ THE ENGINE (Avoid modifying)
│   ├── db.py            # Database connection & session
│   ├── system.py        # Config & Boot logic
│   └── cron.py          # Job scheduler
│
├── app/                 # ✅ YOUR IMPLEMENTATION (Work here)
│   ├── routes/          # Your specific endpoints
│   │   └── domains.py   # e.g., "Lampiris Domain Monitor"
│   ├── templates/       # Your HTML files
│   └── jobs/            # Your background scripts
│       └── fetch_api.py
│
├── Dockerfile           # Production ready
└── main.py              # Entry point

```

## Getting Started (The Git Workflow)

PyOps is designed to be used as an **Upstream** repository. You clone this public repo, but you push your work to your own private repository.

### 1. Initialize your private project

```bash
# 1. Clone the PyOps framework
git clone [https://github.com/your-username/pyops.git](https://github.com/your-username/pyops.git) my-internal-dashboard
cd my-internal-dashboard

# 2. Rename the current origin (to keep a link for future updates)
git remote rename origin upstream

# 3. Add your private repository as the new origin
# (Create an empty private repo on GitHub/GitLab first)
git remote add origin [https://github.com/your-company/my-internal-dashboard.git](https://github.com/your-company/my-internal-dashboard.git)

# 4. Push the base code to your private repo
git push -u origin main

```

### 2. Run Locally

**Using Docker (Recommended):**

```bash
docker compose up --build

```

**Using Python:**

```bash
pip install -r requirements.txt
python main.py

```

*Access the dashboard at `http://localhost:8000*`

## How to Update

If the PyOps framework receives security fixes or new core features, you can merge them into your private project without losing your work (provided you haven't altered the `/core` directory).

```bash
# Fetch changes from the public framework
git fetch upstream

# Merge changes into your current branch
git merge upstream/main

```
