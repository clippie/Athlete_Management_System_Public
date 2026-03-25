# Athlete_Management_System_Public
This repository displays a proprietary athlete management system I created for the SU Women's Lacrosse Program. This system aggregates data from different sources and stores everything in a centralized database. This allows users to easily access performance data all in one place, giving insights into health, load management, and strength testing.

Login/Authentication:
<img width="959" height="440" alt="image" src="https://github.com/user-attachments/assets/7922e361-7282-4475-98b6-a83c68b19d9b" />

Team Home Page:
<img width="959" height="437" alt="image" src="https://github.com/user-attachments/assets/fe56f9cf-e93f-4e47-a44a-3c9fe2712441" />

25% percetile conditional formatting. 

STatsports:
<img width="944" height="439" alt="image" src="https://github.com/user-attachments/assets/16acb47f-cc73-405b-894a-03130883cd62" />

Daily Readiness:
<img width="949" height="440" alt="image" src="https://github.com/user-attachments/assets/07020f5d-91ff-4f65-8a13-22b038ea5b72" />

Data Management
<img width="949" height="440" alt="image" src="https://github.com/user-attachments/assets/a7bec9a3-a3f6-47a1-a3b2-e007d6d1af97" />

# Athlete Management System (AMS)

A full-stack web dashboard built for a collegiate lacrosse coaching staff to monitor athlete health, daily readiness, and GPS performance data — all in one place.

This was my first full-stack web project. It replaced a workflow where coaches were manually exporting spreadsheets from multiple platforms to make load management decisions. The system connects to GPS wearables, Google Sheets wellness surveys, and baseline athletic testing data, and presents everything through an interactive dashboard.

Built for a program managing 35+ athletes.

---

## Screenshots

| Login | Team Home |
|---|---|
| ![Login](screenshots/login.png) | ![Team Home](screenshots/team_home.png) |

| STATSports GPS Analytics | Daily Readiness Surveys |
|---|---|
| ![STATSports](screenshots/statsports.png) | ![Daily Readiness](screenshots/daily_readiness.png) |

| Data Management |
|---|
| ![Data Management](screenshots/data_management.png) |

---

## What It Does

**For coaching staff (2–5 users):**

- View individual athlete or full-team wellness data across any date range
- See GPS session metrics from wearables (distance, speed zones, sprint counts, load)
- Track daily wellness survey responses (sleep, mood, energy, stress, muscle soreness)
- Review baseline athletic testing results (jump height, strength, sprint times)
- Sync all data sources with one click from the Data Management page

---

## Pages

**Login** — Secure login with JWT authentication. Coaches and athletes have different access levels.

**Team Home** — Side-by-side comparison of all athletes for a selected date range. Shows total distance, wellness scores, sleep, and soreness at a glance.

**Home (Individual)** — Per-athlete view with a wellness radar chart, muscle soreness body diagram, distance per session, and GPS metric cards.

**Daily Readiness** — Survey analytics focused on wellness trends. Radar chart, daily readiness score bars, and a multi-line chart tracking sleep, mood, energy, stress, and soreness over time.

**STATSports** — GPS analytics from wearable devices. Distance zone donut chart (6 speed zones from walking to sprinting), average distance per player bar chart, and metric summary cards.

**Testing Data (Incomplete)** — Strength and speed benchmark results from periodic assessments (countermovement jump, broad jump, strength tests, sprint times). Shows bilateral asymmetry for injury awareness.

**Data Management** — Sync calendar showing which dates have data from each source (GPS, surveys, testing). One-click sync buttons for each data pipeline.

---

## Tech Stack

**Frontend**
- React 19 with Vite
- Recharts (radar, bar, line, donut charts)
- Material-UI (components and icons)
- React Router (page navigation)
- Axios (API requests)

**Backend**
- FastAPI (Python)
- PostgreSQL database
- SQLAlchemy ORM
- JWT authentication
- Google Sheets API integration

---

## How the Data Flows

```
GPS Wearables API  ──→  Session & drill data (60+ metrics per athlete per drill)
Google Sheets (1)  ──→  Daily wellness survey responses (35+ athletes)
Google Sheets (2)  ──→  Baseline athletic testing benchmarks

All three sources sync into PostgreSQL via the backend,
then the React frontend fetches and visualizes the data.
```

---

## Project Structure

```
backend/
├── app/
│   ├── routers/       # API endpoints (auth, surveys, GPS, testing)
│   ├── models/        # Database table definitions
│   ├── services/      # Business logic (sync, aggregation, matching)
│   └── main.py        # App entry point

frontend/ams-frontend/src/
├── pages/             # One file per page (Home, DailyReadiness, STATSports, etc.)
│   └── components/    # Charts, cards, and reusable UI pieces
├── context/           # Auth state management
└── App.jsx            # Route definitions
```

---

## What I Learned

This was my first time building something full-stack from scratch. A few things that took real debugging to figure out:

- **Timezone bugs** — JavaScript's date methods apply local timezone offsets to UTC timestamps from the API, so calendar dates were showing up one day off. Fixed by switching to UTC-specific methods (`getUTCDate()`, etc.) everywhere dates are displayed.
- **Survey date vs. sync date** — Charts were only showing one data point instead of a full date range. The backend was filtering surveys by when they were synced, not when they were actually filled out. Fixing the query column fixed the charts immediately.
- **Player name mismatches** — GPS devices store legal names ("John Doe"), but coaches write nicknames in Google Sheets ("Johnny Doe"). Built a flexible name-matching system to connect data across sources without losing records.

---

*FastAPI · React 19 · PostgreSQL · Recharts · SQLAlchemy*
