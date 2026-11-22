# Scholarship Finder & Application Tracker

A web platform that helps Queen's engineering students find scholarships they are eligible for and keep track of every application in one place. Built by the ESSDev Scholarship Finder team (2026 to 2027), the software development team of the Engineering Society at Queen's University.

**Status:** early development. We are finishing research and setting up the project skeleton.

## Why this exists

Scholarship information is scattered across university pages, government portals, foundations, and databases. Students spend hours working out which awards they actually qualify for, and then lose track of deadlines, required documents, and renewals. Some students simply never find awards they would have won.

Scholarship Finder brings the listings together, matches them to each student's profile, and tracks the whole process. Students still apply on the official provider's website, so we never replace or store sensitive application data.

## What it does

* **Discover:** a database of verified scholarships from official, open, and permission based sources, with Queen's University scholarships and awards at the core. Every listing shows where it came from and when it was last verified.
* **Match:** personalized recommendations with a match score and a plain language explanation of why a scholarship fits, or why a student does not qualify.
* **Track:** save scholarships, follow application statuses from Saved to Awarded, keep document checklists, and get reminders for deadlines and renewals.
* **Trust:** dead link checks, automatic archiving after deadlines, a "report outdated listing" option, and admin review before submitted listings go live.

## How matching works

1. **Hard filters.** Rules remove anything the student cannot qualify for, such as the wrong year of study, program, or residency status.
2. **AI ranking.** An LLM compares the student's profile with each remaining listing and produces a score.
3. **Clear reasons.** Each result explains the match. The AI only uses verified, normalized listing data and never invents eligibility criteria.

## Data principles

* We prefer official APIs, open data, and sources that give us explicit permission.
* We do not scrape sites whose terms forbid it.
* We store a concise listing and link back to the official application page instead of copying whole websites.
* Accuracy and current deadlines matter more than the size of the database.

## Tech stack

* **Frontend:** React with JavaScript, Vite, and Tailwind
* **Backend:** Python with FastAPI
* **Database:** PostgreSQL with pgvector, plus Redis
* **AI:** Claude API
* **Infrastructure:** Docker, GitHub Actions for CI, and Azure for hosting

## Getting started

You need Git and Docker Desktop. Windows users need WSL2 enabled.

    git clone https://github.com/NathanielCheung/ESSDEV_Scholarship_Finder.git
    cd ESSDEV_Scholarship_Finder
    cp .env.example .env
    docker compose up --build

Then open:

* Frontend at http://localhost:5173
* Backend API docs at http://localhost:8000/docs
* Health check at http://localhost:8000/health

When the frontend page shows "Backend status: ok", your setup works.

Never commit your `.env` file or real API keys. The `.env.example` file only holds placeholder values.

## Project structure

    frontend/    React app
    backend/     FastAPI app and tests
      app/       API routes, models, data pipeline, and matching code
    docs/        Data schema and team decisions
    .github/     CI workflow, pull request and issue templates

## Running tests

    cd backend
    pip install -r requirements.txt
    pytest

## Contributing

We work in small pull requests. Pick a task from Linear, create a branch, open a pull request with the template filled in, and get one review before merging. Read [CONTRIBUTING.md](CONTRIBUTING.md) for the full workflow.

## Roadmap

* **Sprint 1:** an end to end skeleton that runs with one command, with seeded scholarships shown in the app
* **MVP:** student profiles, search and filters, AI matching, the application tracker, reminders, and admin verification, with about 100 accurate scholarships from 3 to 5 approved sources
* **Later:** resume and document management, a browser extension for saving scholarships found elsewhere, a scholarship provider portal, application analytics, and support for other faculties and universities
