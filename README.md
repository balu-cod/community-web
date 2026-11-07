<div align="center">

# 🌐 Community Web
### *TECH / COMMONS Platform*

**A decentralized, peer-driven engineering commons powered by autonomous web scraping agents, live Google Sheets cloud database, and W3C Verifiable Credentials.**

<br />

[![Live Platform](https://img.shields.io/badge/Live_App-Standalone_Canvas-10b981?style=for-the-badge&logo=googlechrome&logoColor=white)](#-live-preview)
[![Cloud Database](https://img.shields.io/badge/Google_Sheets-Cloud_Database-34A853?style=for-the-badge&logo=googlesheets&logoColor=white)](https://docs.google.com/spreadsheets/d/1R1Q9qc8DtecND4xfoOzc52HWRBA27gq4ejr5xeWP4ZA/edit)
[![License: MIT](https://img.shields.io/badge/License-MIT-3b82f6?style=for-the-badge)](LICENSE)

<br />

[![Python 3.11+](https://img.shields.io/badge/Python-3.11+-3776AB?style=flat-square&logo=python&logoColor=white)](https://www.python.org/)
[![FastAPI](https://img.shields.io/badge/Backend-FastAPI-009688?style=flat-square&logo=fastapi&logoColor=white)](https://fastapi.tiangolo.com)
[![WebAuthn Passkeys](https://img.shields.io/badge/Security-FIDO2_Passkeys-black?style=flat-square&logo=fido&logoColor=white)](https://fidoalliance.org/)
[![WCAG 2.2 AAA](https://img.shields.io/badge/Accessibility-WCAG_2.2_AAA-6366f1?style=flat-square)](https://www.w3.org/WAI/standards-guidelines/wcag/)
[![Tests Passing](https://img.shields.io/badge/Tests-100%25_Passing_(81/81)-success?style=flat-square)](backend/test_api.py)
[![Code Architecture](https://img.shields.io/badge/Data_Mode-100%25_Pure_Dynamic-emerald?style=flat-square)](#-dynamic-architecture)

<br />

[Explore Platform](#-key-features) • [Architecture](#-system-architecture) • [Database Schema](#-google-sheets-cloud-database) • [API Reference](#-api-endpoints) • [Quick Start](#-quick-start) • [Push to GitHub](#-git-repository-setup)

</div>

---

## 📌 Executive Overview

**Community Web** is an open-source, resilient platform engineered for technical communities, engineering circles, and open-source practitioners. It eliminates all hardcoded simulations and demo placeholders in favor of **100% pure dynamic data**, utilizing **Google Sheets as an accessible, real-time cloud relational database**, backed by **autonomous background web scraping agents** that harvest developer news and accredited free certifications.

### What Sets Community Web Apart

| Capability | Legacy Community Platforms | Community Web (TECH / COMMONS) |
| :--- | :--- | :--- |
| **Data Engine** | Proprietary SQL silos / Mock JSON | **Live Google Sheets Cloud DB** with bidirectional sync & offline replay queue |
| **Authentication** | Passwords stored in server databases | **FIDO2 / WebAuthn Biometric Passkeys**, OAuth 2.0 PKCE & RFC 6238 TOTP MFA |
| **Content Sourcing** | Stale manual admin entry | **Autonomous Live Scraping Agents** (Hacker News Algolia API + Course Catalogs) |
| **Credentials** | Proprietary PDF badges | **W3C Verifiable Credentials (JSON-LD)** with Ed25519 cryptographic signatures |
| **User Interface** | Cluttered sidebars & rigid layouts | **Off-canvas 3-dot (`⋮`) navigation**, zero intrusive animations, responsive `ml-0` |
| **Offline Resilience** | "Offline - Reconnect to view" | **Service Worker Background Sync** with automatic local IndexedDB replay |

---

## 🏗 System Architecture

```text
┌───────────────────────────────────────────────────────────────────────────────────┐
│                                CLIENT WORKSPACE                                   │
│  ┌─────────────────────────┐  ┌─────────────────────────┐  ┌────────────────────┐ │
│  │    Desktop / Mobile     │  │   Service Worker PWA    │  │  Local IndexedDB   │ │
│  │ Single-File Canvas App  │  │   Offline Background    │  │  Encrypted Client  │ │
│  │ (Accessible Fraunces+UI)│  │     Sync Engine         │  │     Store          │ │
│  └───────────┬─────────────┘  └────────────┬────────────┘  └─────────┬──────────┘ │
└──────────────┼─────────────────────────────┼─────────────────────────┼────────────┘
               │ HTTPS REST / SSE Events     │ Offline Sync Replay     │ Read / Write
               ▼                             ▼                         ▼
┌───────────────────────────────────────────────────────────────────────────────────┐
│                         FASTAPI ASYNCHRONOUS BACKEND LAYER                        │
│                                                                                   │
│  ┌───────────────────────┐  ┌───────────────────────┐  ┌───────────────────────┐  │
│  │ News Intelligence     │  │ Web Scraping Agent    │  │ Decentralized Auth    │  │
│  │ Agent (Hacker News)   │  │ (Free Certifications) │  │ (WebAuthn / PKCE)     │  │
│  └───────────┬───────────┘  └───────────┬───────────┘  └───────────┬───────────┘  │
│              │                          │                          │              │
│  ┌───────────▼──────────────────────────▼──────────────────────────▼───────────┐  │
│  │             Google Sheets Two-Way Synchronization Engine                    │  │
│  │               (Batch Writes, Conflict Resolution, Caching)                  │  │
│  └──────────────────────────────────────┬──────────────────────────────────────┘  │
└─────────────────────────────────────────┼─────────────────────────────────────────┘
                                          ▼ Google Sheets REST API v4
┌───────────────────────────────────────────────────────────────────────────────────┐
│                    LIVE GOOGLE SHEETS CLOUD RELATIONAL DATABASE                   │
│                                                                                   │
│  [Sheet ID: 1R1Q9qc8DtecND4xfoOzc52HWRBA27gq4ejr5xeWP4ZA]                         │
│  ├── 👤 Members             (ID, Name, Email, Role, City, Bio, Public Key)        │
│  ├── 🎓 Free_Certifications (ID, Title, Provider, Skills, Hours, Official Link)   │
│  ├── 📰 Daily_Tech_News     (ID, Title, Source, Category, Read Time, Timestamp)  │
│  ├── 🗺️ Learning_Paths      (ID, Title, Domain, Modules Count, Capstone Project)  │
│  ├── 📅 Community_Events    (ID, Title, Date, Host, Format, Attendees, Location)  │
│  ├── 🔄 Offline_Sync_Queue  (Queue ID, Client Action, Payload, Sync Status)       │
│  └── 📡 Community_Reachout  (Channel, City, Syndication Protocol, Active Endpoint)│
└───────────────────────────────────────────────────────────────────────────────────┘
```

---

## ⚡ Key Features

### 1. Pure Dynamic Data (Zero Simulated Placeholders)
* **Real Member Registration**: Complete registration flow capturing real member profiles, disciplines, technical domains, and biometric keys.
* **Member Profiles**: Dynamic role configuration, city identification, active study circle affiliations, and contribution records.
* **Zero Demo Switchers**: Completely removed legacy demo personas, mock challenge banners, and synthetic user mocks.

### 2. Autonomous Web Scraping & News Intelligence
* **Live Developer News Feed**: Queries the [Hacker News Algolia Search API](https://hn.algolia.com/api/v1/search?tags=front_page) in real time to curate breaking architectural, language, and standards developments.
* **Free Online Certifications**: Gathers verified, cost-free technical certifications across top providers:
  - [Harvard University CS50](https://pll.harvard.edu/course/cs50-introduction-computer-science) — Computer Science Foundations
  - [freeCodeCamp](https://www.freecodecamp.org/learn) — Full Stack & Responsive Web Design
  - [Google Cloud Skills Boost](https://www.cloudskillsboost.google/) — Cloud Engineering & Generative AI
  - [The Linux Foundation](https://training.linuxfoundation.org/) — Linux Kernel & Open Source Governance
* **On-Demand Intelligence Scrapes**: Manual or scheduled scraper runs directly from the UI or via `POST /api/agents/scrape-news` and `POST /api/agents/scrape-certifications`.

### 3. Google Sheets as a Cloud Relational Database
* Directly connects to the live platform database: [TECH / COMMONS — Platform Backend Database](https://docs.google.com/spreadsheets/d/1R1Q9qc8DtecND4xfoOzc52HWRBA27gq4ejr5xeWP4ZA/edit).
* Structured into 7 relational sheets with automatic schema mapping:

| Sheet Tab | Purpose | Primary Keys |
| :--- | :--- | :--- |
| `Members` | Dynamic roster of authenticated developers & mentors | `member_id`, `email` |
| `Free_Certifications` | Curated index of accredited 100% free certifications | `cert_id`, `provider` |
| `Daily_Tech_News` | Syndicated developer updates with category tagging | `article_id`, `url` |
| `Learning_Paths` | Engineering syllabi, milestones, and project criteria | `path_id`, `domain` |
| `Community_Events` | Workshops, whiteboarding sessions, and host listings | `event_id`, `host_id` |
| `Offline_Sync_Queue`| Audit log of offline actions replayed during sync | `sync_id`, `timestamp` |
| `Community_Reachout`| Syndication endpoints, RSS feeds, and city chapters | `channel_id`, `city` |

### 4. Enterprise Security & Decentralized Identity
* **FIDO2 / WebAuthn Biometric Authentication**: Native Touch ID, Face ID, and hardware security key support.
* **OAuth 2.0 PKCE Flow**: Proof Key for Code Exchange (RFC 7636) protocol for secure delegated authorization.
* **RFC 6238 TOTP**: Built-in cryptographic multi-factor authentication with authenticator app integration.
* **W3C Verifiable Credentials**: Direct client-side and server-side minting of W3C-compliant JSON-LD credential packages with Ed25519 digital signatures.
* **Decentralized Identifier (DID)**: Resolves `did:web:tech-commons.org` with cryptographic verification methods.

### 5. Accessible, Noise-Free UI/UX Design System
* **Off-Canvas 3-Dot Navigation (`⋮`)**: Replaces cumbersome topbars and floating close buttons. Collapsing the menu completely removes it from layout flow (`ml-0`), maximizing workspace area.
* **Typography**: Editorial display headers set in *Fraunces* paired with clean, accessible body text in *Inter* and monospace data tables in *JetBrains Mono*.
* **Color Palettes**: Four accessible color themes switchable on the fly:
  - ☀️ **Warm Light** — Editorial cream and deep slate
  - 🌙 **Quiet Dark** — Minimalist midnight slate with low-fatigue contrast
  - 🌿 **Soft Sage** — Nature-inspired muted moss and olive tones
  - ⚡ **High Contrast** — Strict WCAG 2.2 AAA black and yellow tokens
* **Formal Progress Indicators**: Replaced distracting bouncy floating animations with calm, accessible loading rings and subtle toast confirmations.

---

## 📂 Repository File Structure

```text
community-web/
├── index.html                   # Main modular portal shell
├── tech_commons_standalone.html # Single-file self-contained application (Canvas preview)
├── manifest.json                # PWA Progressive Web App configuration
├── sw.js                        # Offline service worker & background sync replay
├── Dockerfile                   # Multi-stage production container image
├── docker-compose.yml           # Multi-container orchestration (FastAPI + Nginx)
├── nginx.conf                   # Production reverse proxy & caching rules
├── .gitignore                   # Version control exclusions
│
├── backend/                     # Python asynchronous API & agent services
│   ├── main.py                  # Core FastAPI application & REST routing
│   ├── models.py                # Pydantic validation schemas
│   ├── real_data.py             # Seed data and canonical schemas
│   ├── google_sheets_sync.py    # Google Sheets cloud database sync engine
│   ├── database.py              # Local SQLite aggregation & caching layer
│   ├── test_api.py              # 13 backend unit tests (100% pass)
│   └── agents/                  # Autonomous agent microservices
│       ├── news_intelligence_agent.py   # Live Hacker News search scraper
│       ├── web_scraping_agent.py        # Free certifications directory scraper
│       ├── oauth2_verification_agent.py # RFC 7636 PKCE handshake validator
│       ├── webauthn_agent.py            # FIDO2 Passkey challenge & verify
│       └── credential_ledger_agent.py   # W3C Verifiable Credential issuer
│
├── pages/                       # Modular view templates
│   ├── overview.html            # Main dashboard & active learning pulse
│   ├── learning-paths.html      # Engineering roadmaps & curriculum detail
│   ├── weekly-goals.html        # Intentions, habit tracker & reflections
│   ├── community.html           # Member directory & peer network
│   ├── learning-circles.html    # Asynchronous study circles & forum threads
│   ├── events.html              # Technical workshops & RSVP management
│   ├── certifications.html      # Free certification catalog & VC exporter
│   ├── tech-news.html           # Live developer news & distraction-free reader
│   ├── resources.html           # Curated tools, specifications & bookmarks
│   ├── contributions.html       # Open-source contributions & activity streaks
│   ├── notifications.html       # Actionable alerts & mention center
│   ├── settings.html            # Profile, theme & security preferences
│   └── signin.html              # Passkey & dynamic registration portal
│
├── scripts/                     # Modular frontend architecture
│   ├── app.js                   # Reactive state store, router & action dispatchers
│   ├── db.js                    # Local IndexedDB persistence client
│   ├── sse-client.js            # Server-Sent Events real-time feed handler
│   ├── webauthn.js              # Browser FIDO2 WebAuthn credential client
│   └── vc-export.js             # W3C JSON-LD Verifiable Credential packager
│
└── styles/
    └── main.css                 # Comprehensive design token system & responsive layout
```

---

## 🚀 Quick Start Guide

### Option 1: Run with Docker Compose (Recommended)

Clone or unzip the repository, then launch the full stack with one command:

```bash
docker-compose up --build -d
```

* **Frontend**: Open `http://localhost:80` in your web browser.
* **Backend API & Docs**: Access `http://localhost:8000/docs` for interactive Swagger documentation.

To stop the containers:
```bash
docker-compose down
```

---

### Option 2: Run Locally (Python 3.11+)

#### 1. Setup Virtual Environment & Install Dependencies
```bash
python3 -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
pip install fastapi uvicorn httpx pydantic
```

#### 2. Start the Backend API
```bash
cd backend
python -m uvicorn main:app --host 0.0.0.0 --port 8000 --reload
```

#### 3. Launch the Frontend
Serve the project directory using any static file server:
```bash
# In the project root:
python3 -m http.server 3000
```
Then navigate to `http://localhost:3000` in your browser. Alternatively, simply double-click or open `tech_commons_standalone.html` directly in any web browser.

---

## 📡 REST API Reference

The backend exposes an asynchronous REST API documented via OpenAPI / Swagger:

| Method | Endpoint | Description | Auth Required |
| :--- | :--- | :--- | :---: |
| `GET` | `/` | System health check & active agents manifest | No |
| `GET` | `/.well-known/did.json` | W3C Decentralized Identifier resolution | No |
| `GET` | `/api/news/daily` | Fetch live curated developer news | No |
| `POST`| `/api/agents/scrape-news`| Trigger live Hacker News Algolia scraper | No |
| `GET` | `/api/certifications/free-online`| Fetch catalog of 100% free certifications | No |
| `POST`| `/api/agents/scrape-certifications`| Trigger live certification catalog scraper | No |
| `GET` | `/api/database/sheets` | Inspect connected Google Sheets cloud database | No |
| `POST`| `/api/database/sheets/sync` | Trigger bidirectional cloud database sync | No |
| `GET` | `/api/reachout/channels` | List active city chapters & syndication channels | No |
| `GET` | `/api/reachout/syndication-feeds` | Fetch RSS and Mastodon syndication feeds | No |
| `POST`| `/api/auth/register` | Register a new real community member | No |
| `POST`| `/api/auth/webauthn/register/options`| Generate FIDO2 passkey registration challenge | No |
| `POST`| `/api/auth/webauthn/register/verify` | Verify passkey attestation response | No |
| `POST`| `/api/credentials/w3c/issue` | Mint a signed W3C Verifiable Credential | Yes |
| `POST`| `/api/sync/replay` | Replay offline PWA actions from client queue | No |

---

## 🧪 Testing & Quality Assurance

The codebase includes automated unit tests, action tests, and layout validators:

### 1. Run Python Backend Unit Tests (13 Suites)
```bash
cd backend
python3 test_api.py
```
**Test Results**:
```text
✓ test_root: Platform manifest and registered agents verified
✓ test_did_web_resolution: W3C Ed25519 verification methods verified
✓ test_aggregate_all_endpoint: Full relational dataset integrity checked
✓ test_aggregate_search: Query tokenization and search filtering verified
✓ test_totp_mfa_workflow: RFC 6238 TOTP seed setup and validation passed
✓ test_pwa_sync_replay: Offline queued mutation replay verified
✓ test_real_news_endpoint: Daily tech news structure validated
✓ test_real_certifications_endpoint: Free certification schemas validated
✓ test_oauth2_login: Standard OAuth 2.0 PKCE flow verified
✓ test_oauth2_demo_login: Fallback authorization handshake checked
✓ test_real_user_registration_and_login: Dynamic member lifecycle tested
✓ test_free_online_certifications_scraping: Live scraping agent verified
✓ test_daily_tech_news_scraping: Live news intelligence scraper verified

ALL 13 BACKEND TEST SUITES PASSED SUCCESSFULLY 100%!
```

### 2. Run Comprehensive Frontend Action Tests (68 User Actions)
```bash
node artifacts/file_generation/ttl=63d/intermediate/test_all_actions.js
```
**Test Results**:
```text
Total Actions Tested: 68
Passed: 68
Failed: 0 (100% Pass Rate)
```

---

## 🚢 Pushing to Your GitHub Repository

The project directory is already initialized as a Git repository on the `main` branch. To link it and push to your GitHub account:

### Method 1: Using the GitHub CLI (`gh`)

```bash
cd community-web
gh repo create community-web --public --source=. --remote=origin --push
```

### Method 2: Using Standard Git

1. Go to [GitHub - Create a New Repository](https://github.com/new).
2. Enter `community-web` as the repository name (leave "Initialize with README" unchecked).
3. Run the following commands:

```bash
cd community-web
git remote add origin https://github.com/<YOUR_GITHUB_USERNAME>/community-web.git
git branch -M main
git push -u origin main
```

---

## 📄 License

Distributed under the **MIT License**. See `LICENSE` for more information.

<div align="center">
  <sub>Built for the global open-source community • TECH / COMMONS</sub>
</div>
