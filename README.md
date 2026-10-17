<p align="center">
  <img src="https://img.shields.io/badge/Platform-Code.com-6C63FF?style=for-the-badge&logo=codeforces&logoColor=white" alt="Code.com" />
  <img src="https://img.shields.io/badge/Stack-React%20·%20Node%20·%20PostgreSQL-00D4AA?style=for-the-badge" alt="Stack" />
  <img src="https://img.shields.io/badge/Real--Time-Socket.IO-010101?style=for-the-badge&logo=socketdotio&logoColor=white" alt="Socket.IO" />
  <img src="https://img.shields.io/badge/Judge-Judge0-E8453C?style=for-the-badge" alt="Judge0" />
</p>

<h1 align="center">⚔️ Code.com</h1>

<p align="center">
  <strong>A Chess.com-inspired competitive programming platform where developers compete head-to-head by solving coding problems in real time.</strong>
</p>

<p align="center">
  <a href="#features">Features</a> •
  <a href="#technology-stack">Tech Stack</a> •
  <a href="#system-architecture">Architecture</a> •
  <a href="#database-design">Database</a> •
  <a href="#api-documentation">API</a> •
  <a href="#installation-and-setup">Setup</a> •
  <a href="#matchmaking-and-competitive-matches">Matchmaking</a>
</p>

---

## Table of Contents

- [Project Overview](#project-overview)
- [Features](#features)
- [Technology Stack](#technology-stack)
- [System Architecture](#system-architecture)
- [Project Structure](#project-structure)
- [Database Design](#database-design)
- [API Documentation](#api-documentation)
- [Socket.IO and Real-Time Communication](#socketio-and-real-time-communication)
- [Matchmaking and Competitive Matches](#matchmaking-and-competitive-matches)
- [Code Execution and Judging](#code-execution-and-judging)
- [Rating System and Leaderboards](#rating-system-and-leaderboards)
- [Installation and Setup](#installation-and-setup)
- [Example Usage](#example-usage)
- [Testing and Verification](#testing-and-verification)
- [Security and Reliability](#security-and-reliability)
- [Limitations and Future Roadmap](#limitations-and-future-roadmap)
- [Contributing](#contributing)
- [Acknowledgements](#acknowledgements)

---

## Project Overview

**Code.com** is a competitive programming platform inspired by [Chess.com](https://www.chess.com/), where the competition is not chess — it is code. Instead of playing timed chess games, users compete in **real-time 1v1 coding matches**, solving algorithmic problems under time pressure while racing against an opponent of similar skill.

### The Problem It Solves

Traditional coding practice platforms (LeetCode, HackerRank) focus on solo problem solving. While valuable for skill-building, they lack the **competitive adrenaline** of directly facing another human in a timed contest. Platforms like Codeforces offer periodic contests, but these are scheduled events — you can't simply log in and immediately compete.

Code.com bridges this gap by offering **on-demand competitive programming matches**, available any time, against opponents matched to your rating.

### How It Works

1. A player queues for a match, choosing a duration (15, 30, or 45 minutes).
2. The matchmaking system finds an opponent with a similar competitive rating.
3. Both players enter a countdown lobby, then the match begins.
4. Both players receive the **same set of problems** and race to solve them.
5. Submissions are evaluated by an automated judge (Judge0).
6. The player who solves more problems — with time-based penalty as the tiebreaker — wins.
7. Ratings are updated based on the match outcome.

### What Makes It Different

| Feature | Traditional Platforms | Code.com |
|---|---|---|
| Competition format | Solo practice or scheduled contests | On-demand 1v1 matches |
| Opponent matching | None | Rating-based matchmaking |
| Problem difficulty | Easy / Medium / Hard labels | Codeforces-style numeric ratings (800–2000+) |
| Real-time feedback | Delayed | Live via Socket.IO |
| Private matches | Rarely supported | Private rooms with custom settings |

### Intended Users

- Competitive programmers looking for quick, rated practice matches.
- Developers who want to sharpen algorithmic skills in a competitive setting.
- Friends who want to challenge each other in private coding rooms.
- Anyone preparing for technical interviews who wants pressure-tested practice.

---

## Features

### ✅ Designed and Schema-Ready

The following features have fully designed database schemas and architectural plans, ready for implementation:

#### Authentication & Profiles
- **User registration and login** — email/password authentication with secure password hashing.
- **User profiles** — username, full name, photo URL, and competitive statistics.
- **Player statistics** — problems solved, matches played/won/drawn/lost.

#### Problems & Test Cases
- **Codeforces-style problem ratings** — numeric difficulty ratings (e.g., 800, 1200, 1600), not simplified Easy/Medium/Hard categories.
- **Rich problem statements** — title, statement, input/output format, and constraints.
- **Sample and hidden test cases** — sample test cases visible to users; hidden test cases used only during judging.
- **Problem lifecycle** — draft, published, and archived statuses with filtered indexing.
- **Configurable execution limits** — per-problem time limits (default 2000ms) and memory limits (default 256MB).

#### Matchmaking & Competition
- **Public matchmaking** — rating-based pairing that matches players of similar skill within the same match mode.
- **Three match modes** — 1v1 Quick Duel (15 min, 3 problems), 1v1 Standard (30 min, 4 problems), 1v1 Marathon (45 min, 6 problems).
- **Configurable match durations** — 15, 30, and 45 minutes with appropriate problem counts and difficulty ranges.
- **Rating-range problem selection** — each mode defines a min/max problem rating for selecting appropriately difficult problems.
- **Match countdown** — a 10-second countdown before the match begins.
- **Private rooms** — custom competitions with configurable participants (2–8), durations, and problem settings via shareable room codes.
- **Room lifecycle** — WAITING → COUNTDOWN → RUNNING → COMPLETED / CANCELLED.

#### Code Execution & Judging
- **Submission tracking** — source code, language, verdict, execution time, and memory usage.
- **Automated judging via Judge0** — asynchronous job queue with retry support.
- **Standard verdicts** — ACCEPTED, WRONG_ANSWER, TIME_LIMIT_EXCEEDED, MEMORY_LIMIT_EXCEEDED, RUNTIME_ERROR, COMPILATION_ERROR, INTERNAL_ERROR.
- **Per-problem progress tracking** — attempts, first solve time, and penalty calculation.

#### Scoring & Ratings
- **ICPC-style scoring** — problems solved as the primary ranking metric; total penalty seconds as the tiebreaker.
- **Match results** — WIN, LOSS, DRAW, ABANDONED outcomes with final rankings.
- **Rating history** — complete audit trail of rating changes per match, with computed `rating_change` column.
- **Dynamic leaderboard** — ranked by current rating using indexed queries, not stored positions.
- **Highest rating tracking** — preserved separately from the current rating.

#### Social
- **Friendships** — friend request system with PENDING, ACCEPTED, REJECTED, and BLOCKED statuses.
- **Private room invitations** — room codes for inviting friends to custom matches.

### 🔮 Planned Enhancements

- **React frontend** with Monaco Editor for an integrated code editing experience.
- **Multi-player match modes** — the schema supports 2–8 players per match, enabling future 4-player Battle formats.
- **Advanced matchmaking** — gradually expanding rating tolerance as queue wait time increases.
- **Real-time match updates** — live submission verdicts and opponent progress via Socket.IO.
- **Match reconnection** — handling disconnections and re-joining active matches.
- **Rating analytics** — rating history charts and performance trends.

---

## Technology Stack

| Layer | Technology | Purpose |
|---|---|---|
| **Frontend** | React, JavaScript | Single-page application UI |
| **Code Editor** | Monaco Editor | In-browser code editing with syntax highlighting and language support |
| **Backend** | Node.js, Express | REST API server and business logic |
| **Database** | PostgreSQL | Relational data storage with ACID transactions |
| **Real-Time** | Socket.IO | Bidirectional event-based communication for live match updates |
| **Code Judging** | Judge0 (CE) | Sandboxed code execution and automated verdict evaluation |
| **Version Control** | Git, GitHub | Source control and collaboration |

### How Components Interact

- **React frontend** communicates with the Express backend via REST APIs for authentication, problem retrieval, and match management.
- **Socket.IO** provides a persistent WebSocket connection for real-time events: matchmaking status, countdown ticks, submission verdicts, and opponent progress.
- **Express backend** manages all business logic, enforces constraints, and coordinates between the database and Judge0.
- **PostgreSQL** stores all persistent state — users, problems, matches, submissions, and ratings — with referential integrity and transactional safety.
- **Judge0** executes submitted code in isolated containers, comparing output against test case expected output to produce verdicts.

---

## System Architecture

```mermaid
graph TB
    subgraph Client["Frontend (React)"]
        UI[React UI]
        ME[Monaco Editor]
        SC[Socket.IO Client]
    end

    subgraph Server["Backend (Node.js + Express)"]
        API[REST API Routes]
        AUTH[Auth Middleware]
        MM[Matchmaking Service]
        MS[Match Service]
        JS[Judging Service]
        SIO[Socket.IO Server]
    end

    subgraph Data["Data Layer"]
        PG[(PostgreSQL)]
    end

    subgraph Judge["Code Execution"]
        J0[Judge0 CE]
    end

    UI -->|HTTP| API
    ME -->|Submit Code| API
    SC <-->|WebSocket| SIO

    API --> AUTH
    AUTH --> MM
    AUTH --> MS
    AUTH --> JS

    MM --> PG
    MS --> PG
    JS --> PG
    JS -->|Execute Code| J0
    J0 -->|Verdict| JS

    SIO -->|Match Events| SC
    JS -->|Verdict Notification| SIO
    MM -->|Match Found| SIO
```

### Key Request Flows

#### Authentication Flow
```
Client → POST /api/auth/register → Validate input → Hash password → Insert user → Return JWT
Client → POST /api/auth/login → Verify credentials → Return JWT
Client → Attach JWT to subsequent requests via Authorization header
```

#### Matchmaking Flow
```
Client → POST /api/matchmaking/queue (with mode_id) → Insert into matchmaking_queue
Matchmaking Service → Poll queue → Find two QUEUED entries for same mode with close ratings
→ Create room (PUBLIC) → Create match → Insert match_participants → Select match_problems
→ Transition to COUNTDOWN → Emit Socket.IO event to both players
→ After countdown → Transition to RUNNING → Emit match:start event
```

#### Code Submission Flow
```
Client → POST /api/submissions (source_code, language, problem_id, match_id)
→ Validate match is RUNNING and deadline not passed
→ Insert submission (verdict: QUEUED) → Create judge_job
→ Worker picks up job → Send to Judge0 API → Poll for result
→ Update submission verdict → Update participant_problem_progress
→ Update match_participants score → Emit verdict via Socket.IO
```

#### Match Completion Flow
```
Timer expires OR all problems solved by all participants
→ Transition match to COMPLETED → Calculate final rankings
→ Determine WIN/LOSS/DRAW results → Compute rating changes
→ Update users.rating, users.highest_rating, match stats
→ Insert rating_history records → Emit match:complete via Socket.IO
```

---

## Project Structure

```
Code.com/
├── README.md                                          # This documentation
├── competitive_coding_platform_database_schema.docx   # Database schema design document
│
├── client/                          # React frontend (planned)
│   ├── public/
│   ├── src/
│   │   ├── components/              # Reusable UI components
│   │   │   ├── CodeEditor/          # Monaco Editor wrapper
│   │   │   ├── Navbar/              # Navigation bar
│   │   │   ├── MatchCard/           # Match summary cards
│   │   │   ├── ProblemPanel/        # Problem statement display
│   │   │   └── Leaderboard/         # Rankings table
│   │   ├── pages/                   # Route-level page components
│   │   │   ├── Home/                # Landing page
│   │   │   ├── Login/               # Authentication pages
│   │   │   ├── Problems/            # Problem browser
│   │   │   ├── Match/               # Active match interface
│   │   │   ├── Profile/             # User profile and stats
│   │   │   └── Leaderboard/         # Global rankings
│   │   ├── context/                 # React context providers
│   │   ├── hooks/                   # Custom hooks (auth, socket)
│   │   ├── services/                # API client functions
│   │   └── App.jsx                  # Root component with routing
│   └── package.json
│
├── server/                          # Node.js + Express backend (planned)
│   ├── src/
│   │   ├── config/                  # Database and environment config
│   │   ├── middleware/              # Auth, validation, error handling
│   │   ├── routes/                  # Express route definitions
│   │   │   ├── auth.routes.js
│   │   │   ├── users.routes.js
│   │   │   ├── problems.routes.js
│   │   │   ├── matches.routes.js
│   │   │   ├── submissions.routes.js
│   │   │   └── matchmaking.routes.js
│   │   ├── controllers/            # Request handlers
│   │   ├── services/               # Business logic
│   │   │   ├── matchmaking.service.js
│   │   │   ├── match.service.js
│   │   │   ├── judging.service.js
│   │   │   └── rating.service.js
│   │   ├── socket/                 # Socket.IO event handlers
│   │   ├── db/                     # Database client, migrations, seeds
│   │   │   ├── migrations/
│   │   │   └── seeds/
│   │   └── app.js                  # Express + Socket.IO server setup
│   └── package.json
│
└── .env.example                     # Environment variable template
```

> **Note:** The project is currently in the **design and schema phase**. The directory structure above represents the planned architecture. The database schema has been fully designed and is documented in the `.docx` file and in this README.

---

## Database Design

The database uses **PostgreSQL** and consists of **15 tables** organized into four functional groups. All tables use `BIGINT GENERATED ALWAYS AS IDENTITY` primary keys and `TIMESTAMPTZ` timestamps.

### Entity Relationship Diagram

```mermaid
erDiagram
    users {
        bigint id PK
        varchar username UK
        varchar full_name
        varchar email UK
        text password_hash
        text photo_url
        integer rating
        integer highest_rating
        integer problems_solved
        integer matches_played
        integer matches_won
        integer matches_drawn
        integer matches_lost
        timestamptz created_at
    }

    match_modes {
        bigint id PK
        varchar name UK
        integer participant_count
        integer duration_seconds
        integer problem_count
        integer min_problem_rating
        integer max_problem_rating
        integer countdown_seconds
        boolean is_ranked
        boolean is_active
        timestamptz created_at
    }

    problems {
        bigint id PK
        varchar slug UK
        varchar title
        text statement
        text input_format
        text output_format
        text constraints_text
        integer rating
        integer time_limit_ms
        integer memory_limit_mb
        varchar status
        bigint created_by FK
        timestamptz created_at
    }

    test_cases {
        bigint id PK
        bigint problem_id FK
        text input_data
        text expected_output
        boolean is_sample
        integer display_order
        timestamptz created_at
    }

    rooms {
        bigint id PK
        varchar room_code UK
        varchar name
        bigint created_by FK
        varchar visibility
        bigint mode_id FK
        integer max_participants
        integer duration_seconds
        integer problem_count
        integer min_problem_rating
        integer max_problem_rating
        varchar status
        timestamptz countdown_started_at
        timestamptz countdown_deadline
        timestamptz created_at
        timestamptz started_at
        timestamptz completed_at
    }

    room_participants {
        bigint room_id PK, FK
        bigint user_id PK, FK
        varchar membership_status
        boolean is_ready
        timestamptz joined_at
        timestamptz left_at
    }

    matchmaking_queue {
        bigint id PK
        bigint user_id FK
        bigint mode_id FK
        integer rating_snapshot
        varchar status
        bigint room_id FK
        timestamptz queued_at
        timestamptz matched_at
        timestamptz cancelled_at
    }

    matches {
        bigint id PK
        bigint room_id FK, UK
        varchar status
        integer participant_count
        integer duration_seconds
        integer problem_count
        timestamptz started_at
        timestamptz ends_at
        timestamptz completed_at
    }

    match_participants {
        bigint match_id PK, FK
        bigint user_id PK, FK
        integer rating_before
        integer rating_after
        integer problems_solved
        integer total_penalty_seconds
        integer score
        integer final_rank
        varchar result
        timestamptz joined_at
    }

    match_problems {
        bigint match_id PK, FK
        bigint problem_id PK, FK
        integer display_order
    }

    submissions {
        bigint id PK
        bigint match_id FK
        bigint user_id FK
        bigint problem_id FK
        varchar language
        text source_code
        varchar verdict
        integer execution_time_ms
        bigint memory_used_kb
        text error_message
        timestamptz submitted_at
        timestamptz judged_at
    }

    participant_problem_progress {
        bigint match_id PK, FK
        bigint user_id PK, FK
        bigint problem_id PK, FK
        integer attempts
        timestamptz solved_at
        integer penalty_seconds
    }

    judge_jobs {
        bigint id PK
        bigint submission_id FK, UK
        varchar status
        integer attempt_count
        varchar worker_id
        text error_details
        timestamptz created_at
        timestamptz started_at
        timestamptz completed_at
    }

    rating_history {
        bigint id PK
        bigint user_id FK
        bigint match_id FK
        integer old_rating
        integer new_rating
        integer rating_change
        timestamptz created_at
    }

    friendships {
        bigint requester_id PK, FK
        bigint addressee_id PK, FK
        varchar status
        timestamptz created_at
    }

    users ||--o{ problems : "created_by"
    users ||--o{ rooms : "created_by"
    users ||--o{ room_participants : "joins"
    users ||--o{ matchmaking_queue : "queues in"
    users ||--o{ match_participants : "competes in"
    users ||--o{ submissions : "submits"
    users ||--o{ rating_history : "has"
    users ||--o{ friendships : "requester"
    users ||--o{ friendships : "addressee"

    match_modes ||--o{ rooms : "configures"
    match_modes ||--o{ matchmaking_queue : "queued for"

    problems ||--o{ test_cases : "has"
    problems ||--o{ match_problems : "assigned to"

    rooms ||--o{ room_participants : "has"
    rooms ||--|| matches : "produces"
    rooms ||--o{ matchmaking_queue : "created from"

    matches ||--o{ match_participants : "has"
    matches ||--o{ match_problems : "includes"
    matches ||--o{ rating_history : "triggers"

    match_participants ||--o{ submissions : "submits"
    match_participants ||--o{ participant_problem_progress : "tracks"

    match_problems ||--o{ submissions : "for"
    match_problems ||--o{ participant_problem_progress : "tracks"

    submissions ||--|| judge_jobs : "judged by"
```

### Table Details

#### Users and Configuration

| Table | Purpose | Key Constraints |
|---|---|---|
| `users` | Player accounts, profiles, and statistics | `username` and `email` UNIQUE; `rating >= 0`; `highest_rating >= rating` |
| `match_modes` | Predefined public match configurations | `name` UNIQUE; `participant_count` 2–8; each duration is a separate row |
| `problems` | Coding problems with numeric difficulty ratings | `slug` UNIQUE; `status` IN (DRAFT, PUBLISHED, ARCHIVED); `rating > 0` |
| `test_cases` | Input/output pairs for each problem | `is_sample` flag separates visible samples from hidden tests |

#### Rooms and Matchmaking

| Table | Purpose | Key Constraints |
|---|---|---|
| `rooms` | Lobbies for both public and private matches | PUBLIC rooms require `mode_id`; PRIVATE rooms have `mode_id IS NULL`; Status: WAITING → COUNTDOWN → RUNNING → COMPLETED/CANCELLED |
| `room_participants` | Users in a room with readiness tracking | Composite PK `(room_id, user_id)`; unique index enforces **one active room per user** |
| `matchmaking_queue` | Queue entries for rating-based 1v1 matching | Unique index ensures **one queued entry per user**; `rating_snapshot` captured at enqueue time |

#### Competition

| Table | Purpose | Key Constraints |
|---|---|---|
| `matches` | The actual competition record | One-to-one with `rooms` via UNIQUE `room_id`; Status: SCHEDULED → RUNNING → COMPLETED/CANCELLED |
| `match_participants` | Per-player results and rating changes | Composite PK `(match_id, user_id)`; `result` IN (IN_PROGRESS, WIN, LOSS, DRAW, ABANDONED) |
| `match_problems` | Problems assigned to a specific match | Composite PK `(match_id, problem_id)`; UNIQUE on `(match_id, display_order)` |

#### Judging and Scoring

| Table | Purpose | Key Constraints |
|---|---|---|
| `submissions` | Source code and judge results | Composite FKs to `match_participants` AND `match_problems` for referential integrity |
| `participant_problem_progress` | Per-problem solve tracking per player | Composite PK `(match_id, user_id, problem_id)`; tracks `attempts`, `solved_at`, `penalty_seconds` |
| `judge_jobs` | Asynchronous code execution queue | One-to-one with `submissions` (UNIQUE `submission_id`); Status: QUEUED → RUNNING → COMPLETED/FAILED |
| `rating_history` | Historical rating changes per match | UNIQUE on `(user_id, match_id)` prevents duplicate rating applications; `rating_change` is a computed stored column |

#### Social

| Table | Purpose | Key Constraints |
|---|---|---|
| `friendships` | Friend requests and blocks | Composite PK `(requester_id, addressee_id)`; `requester_id <> addressee_id` enforced |

### Important Design Decisions

1. **Rooms vs. Matches** — A room represents the lobby; a match represents the competition. This separation allows countdown management, participant readiness, and future spectator support.
2. **Configuration snapshots** — Room settings are copied from the mode at creation time, so modifying a mode later does not alter existing matches.
3. **Dynamic leaderboard** — Rank is computed via `ORDER BY rating DESC` on indexed queries, not stored, preventing stale positions.
4. **Composite foreign keys** — Submissions reference both `match_participants(match_id, user_id)` and `match_problems(match_id, problem_id)`, ensuring referential integrity at the database level.
5. **Concurrent safety** — Unique partial indexes prevent users from being in multiple active rooms or queue entries simultaneously.

### Seed Data — Match Modes

The schema includes three initial match modes:

| Mode Name | Players | Duration | Problems | Problem Rating Range | Countdown |
|---|---|---|---|---|---|
| 1v1 Quick Duel | 2 | 15 min (900s) | 3 | 800–1400 | 10s |
| 1v1 Standard | 2 | 30 min (1800s) | 4 | 1000–1700 | 10s |
| 1v1 Marathon | 2 | 45 min (2700s) | 6 | 1200–2000 | 10s |

---

## API Documentation

The following API endpoints are planned for the backend. All authenticated endpoints require a JWT Bearer token.

### Authentication

| Method | Endpoint | Purpose | Auth |
|---|---|---|---|
| `POST` | `/api/auth/register` | Create a new user account | No |
| `POST` | `/api/auth/login` | Authenticate and receive JWT | No |
| `GET` | `/api/auth/me` | Get current user profile | Yes |

<details>
<summary><strong>POST /api/auth/register</strong></summary>

**Request:**
```json
{
  "username": "coder42",
  "email": "coder42@example.com",
  "password": "securePassword123",
  "full_name": "Jane Doe"
}
```

**Response (201):**
```json
{
  "token": "eyJhbGciOiJIUzI1NiIs...",
  "user": {
    "id": 1,
    "username": "coder42",
    "email": "coder42@example.com",
    "rating": 1000,
    "created_at": "2026-10-17T10:30:00Z"
  }
}
```

**Validation:**
- `username`: 1–30 characters, unique
- `email`: valid email format, unique
- `password`: minimum 8 characters, hashed before storage
</details>

### Users & Profiles

| Method | Endpoint | Purpose | Auth |
|---|---|---|---|
| `GET` | `/api/users/:id` | Get user profile and statistics | No |
| `GET` | `/api/users/:id/matches` | Get user's match history | No |
| `GET` | `/api/users/:id/rating-history` | Get user's rating change history | No |
| `PUT` | `/api/users/me` | Update own profile | Yes |

### Problems

| Method | Endpoint | Purpose | Auth |
|---|---|---|---|
| `GET` | `/api/problems` | List published problems (paginated) | No |
| `GET` | `/api/problems/:slug` | Get problem details with sample test cases | No |
| `POST` | `/api/problems` | Create a new problem (admin) | Yes |
| `PUT` | `/api/problems/:id` | Update problem (admin) | Yes |

<details>
<summary><strong>GET /api/problems/:slug</strong></summary>

**Response (200):**
```json
{
  "id": 42,
  "slug": "two-sum",
  "title": "Two Sum",
  "statement": "Given an array of integers...",
  "input_format": "First line contains N...",
  "output_format": "Print two indices...",
  "constraints_text": "1 <= N <= 10^5",
  "rating": 1200,
  "time_limit_ms": 2000,
  "memory_limit_mb": 256,
  "sample_test_cases": [
    {
      "input_data": "4\n2 7 11 15\n9",
      "expected_output": "0 1",
      "display_order": 1
    }
  ]
}
```

> **Note:** Hidden test cases are never returned in API responses.
</details>

### Matchmaking

| Method | Endpoint | Purpose | Auth |
|---|---|---|---|
| `GET` | `/api/match-modes` | List active match modes | No |
| `POST` | `/api/matchmaking/queue` | Join the matchmaking queue | Yes |
| `DELETE` | `/api/matchmaking/queue` | Leave the matchmaking queue | Yes |
| `GET` | `/api/matchmaking/status` | Check current queue status | Yes |

<details>
<summary><strong>POST /api/matchmaking/queue</strong></summary>

**Request:**
```json
{
  "mode_id": 2
}
```

**Response (201):**
```json
{
  "queue_entry": {
    "id": 15,
    "mode_id": 2,
    "rating_snapshot": 1250,
    "status": "QUEUED",
    "queued_at": "2026-10-17T10:30:00Z"
  }
}
```

**Errors:**
- `409` — User already in queue or active match
- `400` — Invalid or inactive mode
</details>

### Private Rooms

| Method | Endpoint | Purpose | Auth |
|---|---|---|---|
| `POST` | `/api/rooms` | Create a private room | Yes |
| `GET` | `/api/rooms/:code` | Get room details by room code | Yes |
| `POST` | `/api/rooms/:code/join` | Join a private room | Yes |
| `POST` | `/api/rooms/:code/ready` | Toggle ready status | Yes |
| `POST` | `/api/rooms/:code/leave` | Leave a room | Yes |

### Matches

| Method | Endpoint | Purpose | Auth |
|---|---|---|---|
| `GET` | `/api/matches/:id` | Get match details, problems, and participants | Yes |
| `GET` | `/api/matches/:id/problems` | Get problems assigned to a match | Yes |
| `GET` | `/api/matches/:id/results` | Get match results and rating changes | Yes |

### Submissions

| Method | Endpoint | Purpose | Auth |
|---|---|---|---|
| `POST` | `/api/submissions` | Submit code for judging | Yes |
| `GET` | `/api/submissions/:id` | Get submission details and verdict | Yes |
| `GET` | `/api/matches/:id/submissions` | Get all submissions for a match (own only) | Yes |

<details>
<summary><strong>POST /api/submissions</strong></summary>

**Request:**
```json
{
  "match_id": 7,
  "problem_id": 42,
  "language": "cpp",
  "source_code": "#include <iostream>\nusing namespace std;\nint main() { ... }"
}
```

**Response (201):**
```json
{
  "submission": {
    "id": 128,
    "verdict": "QUEUED",
    "submitted_at": "2026-10-17T10:35:22Z"
  }
}
```

**Validation:**
- Match must be RUNNING
- Current time must be before `match.ends_at`
- User must be a participant of the match
- Problem must be assigned to the match
</details>

### Leaderboard

| Method | Endpoint | Purpose | Auth |
|---|---|---|---|
| `GET` | `/api/leaderboard` | Get global rankings (paginated) | No |

---

## Socket.IO and Real-Time Communication

Socket.IO powers all real-time features. The client establishes a persistent WebSocket connection upon login.

### Connection

```javascript
const socket = io('http://localhost:5000', {
  auth: { token: 'Bearer <JWT>' }
});
```

### Event Reference

| Event | Direction | Purpose | Payload |
|---|---|---|---|
| `matchmaking:queued` | Server → Client | Confirmed queue entry | `{ queue_id, mode_id }` |
| `matchmaking:found` | Server → Client | Opponent found, entering countdown | `{ room_id, opponent, countdown_seconds }` |
| `match:countdown` | Server → Client | Countdown tick | `{ seconds_remaining }` |
| `match:start` | Server → Client | Match has begun | `{ match_id, problems, ends_at }` |
| `submission:verdict` | Server → Client | Judging result for a submission | `{ submission_id, verdict, execution_time_ms }` |
| `match:progress` | Server → Client | Opponent solved a problem | `{ user_id, problems_solved, score }` |
| `match:complete` | Server → Client | Match ended | `{ results, rating_changes }` |
| `room:join` | Client → Server | Join a private room | `{ room_code }` |
| `room:ready` | Client → Server | Toggle ready status | `{ room_id }` |
| `room:player_joined` | Server → Client | Another player joined the room | `{ user_id, username }` |
| `room:player_ready` | Server → Client | Player readiness changed | `{ user_id, is_ready }` |

### REST vs. Socket.IO Boundary

| Operation | Protocol | Reason |
|---|---|---|
| Authentication, problem listing, profile updates | REST | Standard CRUD, cacheable |
| Code submission | REST | Request-response with validation |
| Queue status, matchmaking notifications | Socket.IO | Push-based, real-time |
| Countdown ticks, match start/end | Socket.IO | Time-critical, multi-client sync |
| Submission verdicts, progress updates | Socket.IO | Low-latency push notifications |

---

## Matchmaking and Competitive Matches

### Complete Match Lifecycle

```mermaid
stateDiagram-v2
    [*] --> Queued: Player joins queue
    Queued --> Matched: Opponent found
    Queued --> Cancelled: Player cancels

    Matched --> Countdown: Room created
    Countdown --> Running: Countdown expires
    Countdown --> Cancelled: Player disconnects

    Running --> Completed: Timer expires / All problems solved
    Running --> Completed: Player abandons (opponent wins)

    Completed --> [*]: Ratings updated
    Cancelled --> [*]: Queue entries cleaned up
```

### Matchmaking Algorithm

1. **Queue Entry** — Player selects a mode (e.g., "1v1 Standard") and enters the queue. Their current `rating` is snapshotted as `rating_snapshot`.

2. **Opponent Search** — The matchmaking service looks for another `QUEUED` entry in the **same mode** with the closest `rating_snapshot`. The allowed rating difference starts small and **expands as wait time increases**.

3. **Atomic Match Creation** — When two compatible players are found, a PostgreSQL transaction:
   - Marks both queue entries as `MATCHED`
   - Creates a `rooms` record (PUBLIC, COUNTDOWN status)
   - Creates a `matches` record (SCHEDULED)
   - Inserts both `match_participants` with `rating_before`
   - Selects `problem_count` published problems within the mode's rating range
   - Inserts `match_problems` records

4. **Countdown** — Both players receive a `matchmaking:found` event. A 10-second countdown begins. At expiration, the match transitions to `RUNNING` with authoritative `started_at` and `ends_at` timestamps.

5. **Competition** — Both players see the same problems and submit solutions. Each submission creates a `judge_job` processed asynchronously.

6. **Scoring** — Primary: number of problems solved. Tiebreaker: total penalty (time from match start to first accepted submission, plus penalty for failed attempts).

7. **Completion** — When the timer expires (or all problems are solved by all participants), the match moves to `COMPLETED`, results are determined (WIN/LOSS/DRAW), and ratings are updated.

### Private Room Flow

1. **Create** — A user creates a private room, specifying `max_participants`, `duration_seconds`, `problem_count`, and difficulty range. A random `room_code` is generated.

2. **Invite** — The creator shares the `room_code` with friends.

3. **Join** — Invited users join via the room code. The backend verifies capacity in a transaction.

4. **Ready** — Participants toggle `is_ready`. When all participants are ready, the countdown begins.

5. **Match** — Same flow as public matches from this point forward, but the match is **unranked** (private rooms set `is_ranked = FALSE` by default).

---

## Code Execution and Judging

### Submission Pipeline

```mermaid
sequenceDiagram
    participant C as Client
    participant API as Express API
    participant DB as PostgreSQL
    participant W as Judge Worker
    participant J0 as Judge0

    C->>API: POST /api/submissions
    API->>DB: Validate match state & Insert submission
    API->>DB: Create judge_job (QUEUED)
    API->>C: 201 Created (verdict: QUEUED)

    W->>DB: Poll for QUEUED judge_jobs
    W->>DB: Mark job as RUNNING
    W->>J0: Submit source_code + test_cases
    J0-->>W: Execution result per test case
    W->>DB: Update submission verdict
    W->>DB: Update participant_problem_progress
    W->>DB: Update match_participants score
    W->>DB: Mark job as COMPLETED
    W-->>C: Socket.IO submission:verdict event
```

### Supported Languages

Languages are determined by the Judge0 instance. Common supported languages include:

| Language | Judge0 ID | File Extension |
|---|---|---|
| C++ (GCC) | 54 | `.cpp` |
| Python 3 | 71 | `.py` |
| Java | 62 | `.java` |
| JavaScript (Node.js) | 63 | `.js` |
| C (GCC) | 50 | `.c` |

### Verdict Types

| Verdict | Code | Description |
|---|---|---|
| `QUEUED` | — | Submission is waiting to be judged |
| `RUNNING` | — | Code is being executed |
| `ACCEPTED` | AC | Output matches expected output for all test cases |
| `WRONG_ANSWER` | WA | Output differs from expected output |
| `TIME_LIMIT_EXCEEDED` | TLE | Execution exceeded the problem's time limit |
| `MEMORY_LIMIT_EXCEEDED` | MLE | Execution exceeded the problem's memory limit |
| `RUNTIME_ERROR` | RE | Code crashed during execution |
| `COMPILATION_ERROR` | CE | Code failed to compile |
| `INTERNAL_ERROR` | IE | Judge system error (triggers job retry) |

### Execution Limits

- **Time limit:** Per-problem, default 2000ms (configurable in `problems.time_limit_ms`)
- **Memory limit:** Per-problem, default 256MB (configurable in `problems.memory_limit_mb`)
- **Code execution:** Fully sandboxed inside Judge0 containers — **no code runs inside the Express process**

### Hidden Test Case Protection

- The API **only returns** test cases where `is_sample = TRUE`.
- Hidden test inputs and expected outputs are sent exclusively to Judge0 during evaluation.
- Users never see hidden test data, even after the match concludes.

---

## Rating System and Leaderboards

### Rating Overview

- **Initial rating:** 1000 for all new users
- **Rating range:** Minimum 0 (enforced by CHECK constraint), no upper bound
- **Highest rating:** Separately tracked in `users.highest_rating`, updated whenever `rating` exceeds the previous high

### Rating Updates

When a ranked match completes:

1. Determine each participant's `result` (WIN, LOSS, DRAW) based on problems solved and penalty time.
2. Calculate new ratings (algorithm to be implemented — likely Elo-based for 1v1 matches).
3. In a single transaction:
   - Update `match_participants.rating_after`
   - Update `users.rating` and `users.highest_rating`
   - Update `users.matches_played`, `matches_won`, `matches_drawn`, `matches_lost`
   - Update `users.problems_solved`
   - Insert a `rating_history` record per participant

The `rating_history` table includes a `rating_change` computed column (`new_rating - old_rating`), providing an automatic audit trail.

### Leaderboard

The leaderboard is calculated dynamically:

```sql
SELECT id, username, rating, highest_rating,
       problems_solved, matches_played, matches_won,
       ROW_NUMBER() OVER (ORDER BY rating DESC, id ASC) AS rank
FROM users
ORDER BY rating DESC, id ASC
LIMIT 50 OFFSET 0;
```

Supported by the index: `idx_users_leaderboard ON users(rating DESC, id)`.

> **Note:** The specific rating algorithm (Elo, Glicko, or custom) is not yet finalized in the codebase. The schema supports any algorithm that produces integer rating updates.

---

## Installation and Setup

### Prerequisites

| Software | Minimum Version | Purpose |
|---|---|---|
| Node.js | 18.x | Backend runtime |
| npm | 9.x | Package management |
| PostgreSQL | 14.x | Database |
| Judge0 CE | Latest | Code execution (Docker required) |
| Git | 2.x | Version control |

### 1. Clone the Repository

```bash
git clone https://github.com/Divyam-112/Code.com.git
cd Code.com
```

### 2. Environment Configuration

Create a `.env` file in the `server/` directory:

```env
# Server
PORT=5000
NODE_ENV=development

# Database
DATABASE_URL=postgresql://postgres:your_password@localhost:5432/codecom
DB_HOST=localhost
DB_PORT=5432
DB_NAME=codecom
DB_USER=postgres
DB_PASSWORD=your_password

# Authentication
JWT_SECRET=your-secret-key-change-in-production
JWT_EXPIRES_IN=7d

# Judge0
JUDGE0_API_URL=http://localhost:2358
JUDGE0_API_KEY=your-judge0-api-key

# Client
CLIENT_URL=http://localhost:3000
```

> ⚠️ **Never commit real secrets.** The values above are templates only.

### 3. Database Setup

```bash
# Create the database
psql -U postgres -c "CREATE DATABASE codecom;"

# Run migrations (once implemented)
cd server
npm run db:migrate

# Seed match modes
npm run db:seed
```

### 4. Install Dependencies

```bash
# Backend
cd server
npm install

# Frontend
cd ../client
npm install
```

### 5. Start Judge0 (Docker)

```bash
# Follow Judge0 CE setup: https://github.com/judge0/judge0
# Ensure it's accessible at http://localhost:2358
```

### 6. Start the Application

```bash
# Terminal 1 — Backend
cd server
npm run dev    # Starts on http://localhost:5000

# Terminal 2 — Frontend
cd client
npm run dev    # Starts on http://localhost:3000
```

### 7. Verify

- Frontend: [http://localhost:3000](http://localhost:3000)
- Backend API: [http://localhost:5000/api/health](http://localhost:5000/api/health)
- Judge0: [http://localhost:2358](http://localhost:2358)

> **Current Status:** The project is in its **design and schema phase**. The database schema is fully designed. Application code (frontend and backend) is under active development. The commands above represent the planned setup workflow.

---

## Example Usage

### 1. Register and Log In

```bash
# Register
curl -X POST http://localhost:5000/api/auth/register \
  -H "Content-Type: application/json" \
  -d '{
    "username": "speedcoder",
    "email": "speed@example.com",
    "password": "securePass123",
    "full_name": "Speed Coder"
  }'

# Login
curl -X POST http://localhost:5000/api/auth/login \
  -H "Content-Type: application/json" \
  -d '{
    "email": "speed@example.com",
    "password": "securePass123"
  }'
# → Returns JWT token
```

### 2. Browse Problems

```bash
curl http://localhost:5000/api/problems?page=1&limit=20
# → List of published problems with ratings
```

### 3. Join Matchmaking

```bash
# Get available modes
curl http://localhost:5000/api/match-modes

# Queue for 1v1 Standard (30 min)
curl -X POST http://localhost:5000/api/matchmaking/queue \
  -H "Authorization: Bearer <token>" \
  -H "Content-Type: application/json" \
  -d '{ "mode_id": 2 }'

# Wait for matchmaking:found Socket.IO event...
```

### 4. Submit Code During a Match

```bash
curl -X POST http://localhost:5000/api/submissions \
  -H "Authorization: Bearer <token>" \
  -H "Content-Type: application/json" \
  -d '{
    "match_id": 7,
    "problem_id": 42,
    "language": "python",
    "source_code": "n = int(input())\nnums = list(map(int, input().split()))\ntarget = int(input())\nfor i in range(n):\n    for j in range(i+1, n):\n        if nums[i] + nums[j] == target:\n            print(i, j)\n            exit()"
  }'
# → Verdict delivered via Socket.IO
```

### 5. Create a Private Room

```bash
curl -X POST http://localhost:5000/api/rooms \
  -H "Authorization: Bearer <token>" \
  -H "Content-Type: application/json" \
  -d '{
    "max_participants": 4,
    "duration_seconds": 1800,
    "problem_count": 5,
    "min_problem_rating": 900,
    "max_problem_rating": 1500
  }'
# → Returns room_code to share with friends
```

---

## Testing and Verification

### Planned Testing Strategy

| Layer | Tool | Scope |
|---|---|---|
| Unit Tests | Jest | Service functions, utility functions, rating calculations |
| Integration Tests | Jest + Supertest | API endpoints, database operations, auth flows |
| Database Tests | Jest + pg | Schema constraints, unique indexes, cascade behavior |
| Socket.IO Tests | Jest + socket.io-client | Event emission, room management, real-time flows |
| E2E Tests | Cypress / Playwright | Full user flows: register → queue → match → submit → result |

### Running Tests (Once Implemented)

```bash
cd server
npm test                 # Run all tests
npm run test:unit        # Unit tests only
npm run test:integration # Integration tests
npm run test:coverage    # Coverage report
```

> **Current Status:** The test framework and test suites are not yet implemented. The testing strategy above is planned for development.

---

## Security and Reliability

### Implemented Safeguards (Schema Level)

| Area | Measure |
|---|---|
| **Password storage** | `password_hash` column — plaintext passwords are never stored; bcrypt hashing is required at the application layer |
| **SQL injection** | Parameterized queries via Node.js PostgreSQL client (pg) |
| **Hidden test cases** | `is_sample` flag; API must filter to only return sample test cases |
| **Code execution isolation** | Judge0 containers — submitted code never executes inside the Express process |
| **Concurrent match prevention** | Unique partial index `idx_one_active_room_per_user` prevents joining multiple rooms |
| **Duplicate queue prevention** | Unique partial index `idx_one_queued_entry_per_user` prevents multiple queue entries |
| **Rating manipulation** | `rating_history` UNIQUE constraint on `(user_id, match_id)` prevents applying rating changes twice |
| **Data integrity** | CHECK constraints on all status fields, ratings, and counts; composite foreign keys on submissions |

### Recommended (Not Yet Implemented)

| Area | Recommendation |
|---|---|
| **JWT security** | Short-lived access tokens + refresh token rotation |
| **Rate limiting** | Express rate limiter on auth and submission endpoints |
| **Input validation** | Request body validation middleware (e.g., Joi, Zod) |
| **Socket.IO auth** | Validate JWT on WebSocket handshake; reject unauthorized connections |
| **Private room auth** | Verify room code ownership; prevent unauthorized room discovery |
| **HTTPS** | TLS termination in production |
| **Environment secrets** | Use a secret manager; never commit `.env` files |
| **Logging** | Structured logging with request correlation IDs |
| **Error handling** | Centralized error handler that never leaks stack traces to clients |

> ⚠️ **This application is not production-ready.** The schema provides a strong foundation, but application-layer security measures must be implemented during development.

---

## Limitations and Future Roadmap

### Current Status

| Feature | Status |
|---|---|
| Database schema design | ✅ Complete |
| Schema documentation | ✅ Complete |
| Match mode seed data | ✅ Designed |
| Frontend application | ❌ Not yet implemented |
| Backend API | ❌ Not yet implemented |
| Socket.IO integration | ❌ Not yet implemented |
| Judge0 integration | ❌ Not yet implemented |
| Rating algorithm | ❌ Not yet implemented |
| Test suite | ❌ Not yet implemented |

### Planned Development Phases

#### Phase 1 — Core Backend
- [ ] Express server setup with PostgreSQL connection
- [ ] Database migration system
- [ ] User authentication (register, login, JWT)
- [ ] Problem CRUD and test case management
- [ ] Submission endpoint and Judge0 integration

#### Phase 2 — Matchmaking & Matches
- [ ] Match mode API
- [ ] Matchmaking queue with rating-based pairing
- [ ] Room and match lifecycle management
- [ ] Match countdown and timer management
- [ ] Scoring and result calculation

#### Phase 3 — Real-Time Features
- [ ] Socket.IO server setup
- [ ] Live matchmaking notifications
- [ ] Live submission verdicts
- [ ] Opponent progress updates
- [ ] Match completion events

#### Phase 4 — Frontend
- [ ] React application scaffold
- [ ] Authentication pages
- [ ] Problem browser and viewer
- [ ] Match interface with Monaco Editor
- [ ] Live match dashboard
- [ ] User profiles and leaderboard

#### Phase 5 — Polish & Scale
- [ ] Rating algorithm implementation (Elo or Glicko-2)
- [ ] Rating history charts
- [ ] Match reconnection handling
- [ ] Comprehensive test suite
- [ ] Production deployment configuration
- [ ] Performance optimization

### Future Enhancements

| Enhancement | Description |
|---|---|
| **4-Player Battle Mode** | `participant_count = 4`, 20 min, mixed difficulty — schema already supports this via `match_modes` |
| **Spectator Mode** | Watch live matches via Socket.IO room subscriptions |
| **Problem Tags & Filters** | Topic-based problem categorization (DP, Graphs, etc.) |
| **Advanced Matchmaking** | Expanding rating tolerance over wait time; anti-stalling measures |
| **Match Replay** | View submission history and progress timeline after a match |
| **Tournament System** | Bracket-based elimination tournaments using the rooms/matches infrastructure |
| **Admin Dashboard** | Problem management, user moderation, and system monitoring |
| **Mobile Support** | Responsive UI or dedicated mobile application |

---

## Contributing

Contributions are welcome! This project is in its early stages, making it an ideal time to get involved.

### Development Workflow

1. **Fork** the repository
2. **Create** a feature branch: `git checkout -b feature/your-feature`
3. **Commit** your changes: `git commit -m "Add your feature"`
4. **Push** to the branch: `git push origin feature/your-feature`
5. **Open** a Pull Request

### Guidelines

- Follow existing code style and naming conventions.
- Write meaningful commit messages.
- Add tests for new features.
- Update documentation for API or schema changes.
- Ensure all schema modifications maintain backward compatibility.

---

## Acknowledgements

- **[Chess.com](https://www.chess.com/)** — Inspiration for the platform's competitive matchmaking model.
- **[Codeforces](https://codeforces.com/)** — Inspiration for the numeric rating system and problem difficulty model.
- **[Judge0](https://judge0.com/)** — Open-source online code execution system used for sandboxed judging.
- **[Monaco Editor](https://microsoft.github.io/monaco-editor/)** — The code editor that powers VS Code, used for the in-browser coding experience.

---

<p align="center">
  <strong>Code.com</strong> — Where every line of code is a move in the game. ⚔️
</p>
