# UniShare — Group 10

> **A verified, campus-only peer-to-peer sharing and ride-matching platform for university students in Bangladesh.**

| | |
|---|---|
| 🌐 **Live Site** | [https://unishare.online](https://unishare.online) |
| 📦 **Stack** | Next.js 16 · React 19 · TypeScript · Prisma · Supabase |
| 🚀 **Hosting** | Vercel (serverless) + Supabase PostgreSQL |

---

## 📑 Table of Contents

1. [Project Documents](#-project-documents)
2. [Features](#-features)
3. [Tech Stack](#-tech-stack)
4. [Local Setup Guide](#-local-setup-guide)
5. [Environment Variables](#-environment-variables)
6. [Repository Structure](#-repository-structure)

---

## 📂 Project Documents

All project documentation is in the [`documents/`](documents/) folder:

| Document | File |
|---|---|
| Software Requirements Specification (SRS) | [`documents/UniShare_SRS.pdf`](documents/UniShare_SRS.pdf) |
| Data Flow Diagram (DFD) | [`documents/Group_10_Unishare_DFD (2).pdf`](<documents/Group_10_Unishare_DFD (2).pdf>) |
| Entity Relationship Diagram (ER) | [`documents/Group_10_Unishare_ER Diagram (2).pdf`](<documents/Group_10_Unishare_ER Diagram (2).pdf>) |
| Software Testing & QA Lab Report | [`documents/Software Testing & Quality Assurance Lab Report.pdf`](<documents/Software Testing & Quality Assurance Lab Report.pdf>) |
| SESA Lab Final Report (Autumn 2026) | [`documents/SESALAB_Final_Report_Format_Autumn_2026_LONG.pdf`](documents/SESALAB_Final_Report_Format_Autumn_2026_LONG.pdf) |
| Figma Design File | [`documents/figma/UniShare.fig`](documents/figma/UniShare.fig) |
| Class Diagram (SVG) | [`documents/images/UniShare_Class_Diagram.svg`](documents/images/UniShare_Class_Diagram.svg) |
| DFD Level 0 & 1 (SVG) | [`documents/images/UniShare_DFD_Level_0_and_1.svg`](documents/images/UniShare_DFD_Level_0_and_1.svg) |
| DFD Level 2 (SVG) | [`documents/images/UniShare_DFD_Level_2.svg`](documents/images/UniShare_DFD_Level_2.svg) |
| ER Diagram (SVG) | [`documents/images/UniShare_ER_Diagram.svg`](documents/images/UniShare_ER_Diagram.svg) |
| Sequence Diagram (SVG) | [`documents/images/UniShare_Sequence_Diagram.svg`](documents/images/UniShare_Sequence_Diagram.svg) |
| Database & Storage Architecture | [`docs/DATA_STORAGE.md`](docs/DATA_STORAGE.md) |

---

## ✨ Features

- **Verified University Network** — 178 Bangladeshi universities, email OTP + student ID KYC
- **Peer Marketplace** — Rent/lend lab equipment, books, electronics with token escrow
- **Campus Ride Matching** — Corridor-based ride matching with live chat & GPS tracking
- **Wallet & Escrow** — Internal token economy, peer transfers, refundable deposits
- **Emergency SOS** — One-tap GPS alert, secure tracking link, WhatsApp/SMS dispatch

---

## 🛠 Tech Stack

| Layer | Technology |
|---|---|
| Framework | Next.js 16 (App Router + Turbopack) |
| Language | TypeScript 5 |
| Styling | Tailwind CSS v4, CSS Modules, Lucide Icons |
| ORM | Prisma 6 |
| Database | PostgreSQL (Supabase) · SQLite (local fallback) |
| File Storage | Supabase Storage |
| Email | Resend API |
| Maps | OpenStreetMap Nominatim + Google Maps API |
| SOS Alerts | UltraMsg (WhatsApp) |
| Deployment | Vercel |

---

## 💻 Local Setup Guide

### Prerequisites

- **Node.js 20+** — [Download](https://nodejs.org)
- **npm 10+** (included with Node)
- **Git** — [Download](https://git-scm.com)

### Step 1 — Clone the repository

```bash
git clone https://github.com/xnocode/unishare-group10.git
cd unishare-group10
```

### Step 2 — Install dependencies

```bash
npm install
```

### Step 3 — Set up environment variables

```bash
cp .env.example .env.local
```

Open `.env.local` and fill in the required values (see [Environment Variables](#-environment-variables) below).

> **Quick start (no cloud account needed):** Set `DATABASE_URL="file:./dev.db"` to use a local SQLite database — no Supabase or PostgreSQL setup required. Email OTP and file uploads will not work without their respective API keys.

### Step 4 — Set up the database

```bash
# Auto-selects PostgreSQL or SQLite based on your DATABASE_URL
node scripts/prepare-prisma.js

# Push the schema to your database (creates all tables)
npx prisma db push
```

### Step 5 — Run the development server

```bash
npm run dev
```

Open [http://localhost:3000](http://localhost:3000) in your browser. ✅

---

### Production Build (optional)

```bash
npm run build
npm start
```

### Lint & Type-check

```bash
npm run lint
npx tsc --noEmit
```

---

## 🔑 Environment Variables

Copy [`.env.example`](.env.example) → `.env.local` and fill in the values:

| Variable | Required | Description |
|---|---|---|
| `DATABASE_URL` | ✅ | PostgreSQL URL **or** `file:./dev.db` for local SQLite |
| `DIRECT_URL` | Optional | Direct DB URL (needed if using PgBouncer pooling) |
| `AUTH_SECRET` | ✅ | Random 32+ character secret for signing session cookies |
| `SUPABASE_URL` | For uploads | Your Supabase project URL |
| `SUPABASE_SERVICE_ROLE_KEY` | For uploads | Supabase service role key |
| `RESEND_API_KEY` | For email OTP | [Resend](https://resend.com) API key |
| `RESEND_FROM` | For email OTP | Sender address e.g. `UniShare <no-reply@example.com>` |
| `ULTRAMSG_INSTANCE_ID` | For SOS | UltraMsg WhatsApp instance ID |
| `ULTRAMSG_TOKEN` | For SOS | UltraMsg API token |
| `NEXT_PUBLIC_GOOGLE_MAPS_API_KEY` | For maps | Google Maps JavaScript API key |

---

## 📁 Repository Structure

```
unishare-group10/
│
├── documents/                        ← All project documents (SRS, diagrams, reports)
│   ├── UniShare_SRS.pdf
│   ├── Group_10_Unishare_DFD (2).pdf
│   ├── Group_10_Unishare_ER Diagram (2).pdf
│   ├── Software Testing & Quality Assurance Lab Report.pdf
│   ├── figma/UniShare.fig
│   └── images/                       ← SVG diagrams (Class, DFD, ER, Sequence)
│
├── docs/
│   └── DATA_STORAGE.md               ← Database schema & storage architecture
│
├── prisma/
│   └── schema.prisma                 ← Database schema (all models)
│
├── scripts/
│   └── prepare-prisma.js             ← Auto-switches Prisma between PostgreSQL & SQLite
│
├── src/app/
│   ├── api/                          ← All Next.js API route handlers
│   │   ├── auth/                     ← Login, register, OTP, verification
│   │   ├── marketplace/              ← Listings, rentals, escrow
│   │   ├── rides/                    ← Ride matching, chat, GPS tracking
│   │   ├── wallet/                   ← Token transfers, top-up
│   │   └── sos/                      ← Emergency SOS, WhatsApp dispatch
│   │
│   ├── lib/                          ← Shared server utilities
│   │   ├── auth.ts                   ← Session management, password hashing
│   │   ├── otp-service.ts            ← OTP generation, rate-limiting, HMAC storage
│   │   ├── bd-universities.ts        ← 178 Bangladeshi university records
│   │   ├── db.ts                     ← Prisma client singleton
│   │   └── cloud-storage.ts          ← Supabase Storage helpers
│   │
│   ├── marketplace/                  ← Marketplace UI pages
│   ├── rides/                        ← Ride matching UI
│   ├── wallet/                       ← Wallet & token UI
│   ├── sos/                          ← SOS UI
│   └── ...                           ← Other pages (login, register, settings, etc.)
│
├── public/                           ← Static assets
├── .env.example                      ← Environment variable template
├── next.config.ts
├── package.json
└── README.md
```

---

> Built for CSE Final Year Project — Group 10 | UniShare © 2026
