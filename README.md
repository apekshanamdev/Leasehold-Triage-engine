
## Live Prototype

[View Prototype Here](https://leaseholdarrearstriageengine.netlify.app/)

## Overview
A working tool that runs a portfolio of accounts through a ten-gate decision engine grounded in UK credit control rules, and tells you exactly what to do with each one.

<div align="center">

# Leasehold Arrears Triage Engine

**AI-assisted ground rent arrears triage for UK leasehold property management**

Built from two years of operational credit control experience processing 80+ accounts daily at a London property management firm.

[![React](https://img.shields.io/badge/React-18-61DAFB?style=flat-square&logo=react&logoColor=white)](https://react.dev)
[![License](https://img.shields.io/badge/License-MIT-D4805A?style=flat-square)](LICENSE)
[![Status](https://img.shields.io/badge/Status-Prototype-C9A84C?style=flat-square)]()
[![Built by](https://img.shields.io/badge/Built%20by-Apeksha%20Namdev-9B8EC4?style=flat-square)](https://linkedin.com/in/apekshanamdev)

[View Live Demo](https://leaseholdarrearstriageengine.netlify.app/) · [Report a Bug](https://github.com/apekshanamdev/leasehold-triage-engine/issues) · [Request a Feature](https://github.com/apekshanamdev/leasehold-triage-engine/issues)

---

</div>


## Table of Contents

- [About the Project](#about-the-project)
  - [The Problem](#the-problem)
  - [The Solution](#the-solution)
  - [Built With](#built-with)
- [How It Works](#how-it-works)
  - [The 10-Point Decision Engine](#the-10-point-decision-engine)
  - [Output Buckets](#output-buckets)
- [Features](#features)
- [Screenshots](#screenshots)
- [Getting Started](#getting-started)
  - [Prerequisites](#prerequisites)
  - [Installation](#installation)
  - [CSV Import Format](#csv-import-format)
- [Roadmap](#roadmap)
- [Background](#background)
- [Author](#author)
- [License](#license)

---

## About the Project

### The Problem

UK leasehold ground rent credit control is a heavily manual process. A team of four credit controllers at a typical property management firm will process **80+ accounts per working day**, each requiring the same sequence of stop-gate checks before any escalation action can be taken. Miss a check  like an active legal case, an estate account, an address change after reminders were sent and you've either issued a letter to the wrong address, duplicated a forfeiture filing, or breached process entirely.

The existing workflow lives across a property management CRM (QUBE), a shared spreadsheet for resets, and institutional memory. There is no decision log, no prioritisation logic, and no audit trail beyond manually initialled Credit Control tab entries.

### The Solution

The **Leasehold Arrears Triage Engine** replicates the full arrears triage decision tree in code running 10 sequential stop-gate checks on each account and routing it to one of four clearly defined action buckets in under a second. What previously took a trained credit controller 2–3 minutes per account becomes instantaneous, auditable, and consistent.

This is **Artifact №1** in a three-part portfolio demonstrating the application of AI-native operations tooling to UK property and financial services workflows.

> **Note:** This is a working prototype. It uses synthetic data by default and is not connected to a live CRM. See [Roadmap](#roadmap) for planned production integrations.

### Built With

| Technology | Purpose |
|---|---|
| React 18 | UI framework |
| JavaScript (ES2022) | Decision engine logic |
| CSS-in-JS (inline styles) | Theming & layout |
| Blob API | CSV export / download |
| FileReader API | CSV import |

No external dependencies beyond React. Runs entirely in the browser.

---

## How It Works

### The 10-Point Decision Engine

Every account passes through the following checks **in order**. The engine stops at the first triggered condition and routes accordingly — no check is skipped.

```
 1.  Outstanding < £100?              →  No action (below threshold)
 2.  Reminder sequence incomplete?    →  Review (complete reminders first)
 3.  Forfeiture already filed?        →  Refer → Legal (do not duplicate)
 4.  Estate account?                  →  Refer → Ground Rent (6-month hold)
 5.  Active legal case on unit?       →  Refer → Legal Team
 6.  Active property transfer?        →  Refer → PT Team
 7.  Address changed post-reminder?   →  Reset (re-run full arrears sequence)
 8.  Contact within 30 days?          →  Review (log reason, set review date)
 9.  Active complaint on file?        →  Review (resolve before LBA)
10.  Sublet charges outstanding?      →  Review (notify Sublet team)
     All 10 checks clear              →  Issue LBA ✓
```

If all 10 checks clear, the account is cleared for a **Letter Before Action** and assigned a priority tier based on outstanding balance.

### Output Buckets

| Bucket | Colour | Trigger | Action |
|---|---|---|---|
| Issue LBA | Copper | All checks clear | Draft LBA + £90 admin charge |
| Review | Gold | Stop gate: contact/complaint/sublet/incomplete | Log reason, set review date |
| Reset | Slate Blue | Address changed after reminders sent | Submit reset entry to Ops team |
| Refer | Lavender | Estate / legal / forfeiture / transfer | Route to named team |

**LBA priority tiers:**

| Tier | Outstanding Balance |
|---|---|
| HIGH | ≥ £1,000 |
| MEDIUM | £500 – £999 |
| STANDARD | £100 – £499 |

---

## Features

- **10-point automated triage** — replicates the full credit control decision tree with zero manual input
- **CSV import** — drop in your own dataset; flexible column name matching handles non-standard headers
- **Synthetic dataset** — 50 realistic accounts generated on load for immediate exploration; regenerate at any time
- **Expandable account cards** — full decision reasoning, stop-gate badges, and Credit Control log entries per account
- **Draft LBA preview** — letter generated inline per account, ready to copy to template
- **Reset entry formatter** — auto-generates Ops reset spreadsheet row for each flagged account
- **Dedicated Exports view** with four downloadable CSVs:
  - LBA-ready accounts (sorted by outstanding)
  - Arrears reset sheet
  - Team referrals list
  - Full Credit Control log
- **Filter by bucket** — isolate LBA, Review, Reset, or Refer accounts
- **Sort by** — outstanding balance, days overdue, or priority
- **Total outstanding** — live aggregate across all loaded accounts
- **Obsidian & Copper dark theme** — designed for extended daily use

---

## Screenshots

### Dashboard — Triage View 

[Triage view showing stat cards and account list]<img width="2523" height="1304" alt="screenshot-dashboard" src="https://github.com/user-attachments/assets/aa6fe56e-7624-47f3-a0c4-05e8b9506cfa" />


*Stat cards at top show live counts per bucket with proportional fill bars. Account list is filterable and sortable. Each row shows account ID, leaseholder name, address, outstanding balance, days overdue, and decision badge.*

---

### Expanded Account Card 

[Expanded account card with decision reasoning and CC log] <img width="1729" height="635" alt="screenshot-expanded-card" src="https://github.com/user-attachments/assets/9bb5db2a-cf48-409f-bed0-4205aead8a7a" />

*Clicking any account expands a detail card showing full account information, the decision reasoning with stop-gate badges where triggered, and a pre-filled Credit Control log entry. LBA accounts also show a draft letter preview.*

---

### Exports View


[Exports view showing four downloadable tables] <img width="1860" height="1248" alt="screenshot-exports" src="https://github.com/user-attachments/assets/42c3f242-ab15-4ec4-a0a4-35febadec974" />

*Switching to Exports shows four independently downloadable tables: LBA-ready accounts, reset sheet, team referrals, and the full Credit Control log.*

---

### CSV Import

[CSV import and loaded dataset confirmation] <img width="1535" height="497" alt="screenshot-csv-import" src="https://github.com/user-attachments/assets/e1a7ba5d-c1fa-4b43-a985-c370c7464e72" />

*Use the Import CSV button to load your own data. The engine matches column names flexibly — see [CSV Import Format](#csv-import-format) for accepted headers.*

---

## Getting Started

### Prerequisites

- Node.js 18+
- npm or yarn

### Installation

1. Clone the repository

```bash
git clone https://github.com/apekshanamdev/leasehold-triage-engine.git
cd leasehold-triage-engine
```

2. Install dependencies

```bash
npm install
```

3. Start the development server

```bash
npm start
```

4. Open [http://localhost:3000](http://localhost:3000)

The app loads with 50 synthetic accounts immediately. No API keys, no database, no configuration needed.

---

### CSV Import Format

The engine accepts `.csv` files with flexible column naming. The following headers are recognised (case-insensitive, special characters ignored):

| Field | Accepted Column Names | Required |
|---|---|---|
| Account ID | `accountId`, `id`, `account` | No (auto-generated if absent) |
| Leaseholder name | `name`, `leaseholder`, `tenant` | Yes |
| Property address | `address`, `property` | Yes |
| Outstanding balance | `outstanding`, `balance`, `arrears` | Yes |
| Ground rent amount | `groundRent`, `grAmount`, `gr` | Yes |
| Ground rent frequency | `frequency`, `grFreq` | No (defaults to Annual) |
| Due date | `dueDate`, `grDue` | Yes |
| Days overdue | `daysOverdue` | No (calculated from due date) |
| Service charge outstanding | `serviceCharge`, `scOut` | No |
| Reminders complete | `remindersComplete`, `remDone` | No (defaults to true) |
| Recent contact | `recentContact`, `hasContact` | No |
| Contact date | `contactDate` | No |
| Contact type | `contactType` | No |
| Contact note | `contactNote`, `contactSummary` | No |
| Correspondence address | `correspondenceAddress`, `corrAddr` | No |
| Address changed | `addressChanged` | No |
| Address change date | `addressChangeDate` | No |
| Forfeiture filed | `forfeiture`, `forfeit` | No |
| Legal case active | `legalCase`, `legal` | No |
| Property transfer active | `transfer`, `propertyTransfer` | No |
| Active complaint | `complaint`, `activeComplaint` | No |
| Estate account | `estate` | No (also auto-detected if name starts with "Estate of") |
| Sublet charges | `sublet` | No |

Boolean fields accept `true`/`false` or `yes`/`no`.

**Example CSV row:**

```csv
accountId,name,address,outstanding,groundRent,dueDate,remindersComplete,recentContact
HO45698611,J. Hargreaves,"Flat 4, 32 Pemberton Court SE15 3TQ",350,350,2025-03-01,true,false
```

---

## Roadmap

The following integrations are planned for a production version of this tool:

- [ ] **HM Land Registry API** — title register verification and registered address matching (requires Business Gateway subscription)
- [ ] **Companies House API** — corporate leaseholder verification for non-individual accounts
- [ ] **QUBE / property CRM write-back** — auto-fill the Credit Control tab on sourced accounts, eliminating manual logging
- [ ] **Solicitor referral portal** — package LBA-cleared accounts with supporting documents for external solicitor handoff
- [ ] **Service charge integration** — unified arrears view combining ground rent and service charge balances
- [ ] **Bulk LBA generation** — produce a full batch of LBA letters in one action, formatted for post or digital delivery
- [ ] **Review date tracker** — surface accounts whose review dates have lapsed

---

## Background

This project emerged from direct operational experience in UK leasehold credit control. The decision logic encoded in the triage engine is not theoretical, it is the exact sequence of checks performed manually on every account, documented and translated into code.

The broader context is a career pivot from regulated financial operations (credit control, collections, property management) toward AI-native fintech and proptech. This artifact is the first in a three-part series:

| Artifact | Description | Status |
|---|---|---|
| **№1 — Leasehold Arrears Triage Engine** | Automates ground rent arrears routing | ✅ Prototype complete |
| **№2 — BACS Reconciliation Copilot** | Matches incoming BACS payments to leaseholder accounts with exception flagging | 🔄 In development |

---

## Author

**Apeksha Namdev**

BSc Business with Economics (First Class) · Anglia Ruskin University, Cambridge   
Former Credit Controller · Estates & Management, London  
Co-founder · AppealEdge

- LinkedIn: [linkedin.com/in/apekshanamdev](https://linkedin.com/in/apekshanamdev)
- GitHub: [@apekshanamdev](https://github.com/apekshanamdev)

---

## License

Distributed under the MIT Licence. See `LICENSE` for more information.

---

<div align="center">
<sub>Built with intent. Not a template.</sub>
</div>
