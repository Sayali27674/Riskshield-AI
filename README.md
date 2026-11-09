# RiskShield AI

An AI-ready risk management platform that helps organizations monitor and analyze risk across transactions, vendors and alerts. It combines a role-based dashboard, a modular risk scoring engine and behavioral analysis, with a dedicated service planned for ML-based anomaly detection and fraud prediction.

![React](https://img.shields.io/badge/React-Vite-61DAFB?logo=react&logoColor=white)
![Node.js](https://img.shields.io/badge/Node.js-22-339933?logo=node.js&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?logo=postgresql&logoColor=white)
![License](https://img.shields.io/badge/License-MIT-yellow.svg)

**Live demo:** _add link here_ | **Author:** Sayali Khatkar

## Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Screenshots](#screenshots)
- [Tech Stack](#tech-stack)
- [Project Structure](#project-structure)
- [Getting Started](#getting-started)
- [Usage](#usage)
- [Demo Accounts](#demo-accounts)
- [Roles and Access](#roles-and-access)
- [Security Notes](#security-notes)
- [Roadmap](#roadmap)
- [Contributing](#contributing)
- [License](#license)

## Overview

RiskShield AI gives risk and compliance teams one place to track transactions, vendors and alerts, and to see which items need attention. The backend scores risk using a modular, rule-based engine and computes behavioral analysis through a dedicated service. The `ai-service` module is reserved for machine learning models (anomaly detection, fraud probability and explainability) that will plug into the same pipeline.

## Features

| Area | Details |
|---|---|
| Authentication | Secure sign-up and login with JWT, passwords hashed with bcrypt |
| Role-based access control | Three roles: ADMIN, ANALYST and USER |
| Dashboard | Summary of transactions and alerts in one view |
| Transactions, vendors and alerts | Full CRUD operations for each |
| Risk scoring | Modular, rule-based risk scoring engine |
| Behavioral analysis | Behavioral analysis computed through a dedicated backend service |
| Demo data | Idempotent seed script with demo accounts, vendors and 100 sample transactions |

## Screenshots

_Add screenshots here (login, dashboard, transactions table, alerts)._

```md
![Dashboard](docs/screenshots/dashboard.png)
![Transactions](docs/screenshots/transactions.png)
```

## Tech Stack

| Layer | Technology |
|---|---|
| Frontend | React, Vite, JavaScript, Tailwind CSS |
| Backend | Node.js 22, Express.js |
| Database | PostgreSQL |
| Authentication | JWT, bcrypt |
| AI/ML (planned) | Python, FastAPI, XGBoost |

## Project Structure

```
riskshield-ai
├── client                # Frontend application (React + Vite)
│   ├── src
│   ├── package.json
│   ├── vite.config.js
│   ├── tailwind.config.js
│   └── .env.example
├── server                # Backend application (Express + PostgreSQL)
│   ├── src
│   ├── package.json
│   └── .env.example
├── ai-service            # Planned AI/ML service
│   └── README.md
├── README.md             # Project documentation
└── .gitignore
```

## Getting Started

### Prerequisites

- Node.js 22 or higher
- PostgreSQL
- npm or yarn

### Installation

1. Clone the repository:

   ```bash
   git clone <repository-url>
   cd riskshield-ai
   ```

2. Set up the backend:

   ```bash
   cd server
   npm install
   ```

   Create a `.env` file from `.env.example` and set your database connection string and JWT secret.

3. Set up the database and seed demo data:

   ```bash
   # Create the database and apply your schema.
   # Update the schema path to match your project.
   psql -U postgres -c "CREATE DATABASE riskshield;"
   psql -U postgres -d riskshield -f path/to/schema.sql

   # Load demo data
   npm run seed
   ```

   The seed is safe to rerun. It upserts the demo accounts and vendors, and updates the same 100 sample transactions. It does not delete other data, and it is disabled when `NODE_ENV=production`.

4. Start the server:

   ```bash
   npm start
   ```

5. Set up the frontend:

   ```bash
   cd ../client
   npm install
   ```

   Create a `.env` file from `.env.example` and set your API base URL.

6. Start the development server:

   ```bash
   npm run dev
   ```

## Usage

1. Open the app at the address Vite prints in the terminal (for example, `http://localhost:3000` or the port set in `vite.config.js`).
2. Sign in with a demo account, or register a new one.
3. Use the dashboard to review transactions, vendors and alerts.

During development, the registration page offers a role selector for testing. The API accepts a selected role only when `NODE_ENV=development`. In production, registration always creates a `USER` and rejects attempts to choose a role.

## Demo Accounts

`npm run seed` creates one ADMIN, two ANALYST and five USER accounts. All of them use the development-only password `RiskShield-Demo-2026!`.

| Role | Email |
|---|---|
| ADMIN | demo.admin@riskshield.test |
| ANALYST | demo.analyst1@riskshield.test, demo.analyst2@riskshield.test |
| USER | demo.user1@riskshield.test through demo.user5@riskshield.test |

The seed creates rule-based demonstration risk records and computes behavioral analysis using the existing behavioral service. Anomaly scores, fraud probabilities and SHAP explanations are left empty because the seed does not run ML models.

## Roles and Access

| Role | Purpose |
|---|---|
| ADMIN | Full access, including administrative operations |
| ANALYST | Reviews and manages risk data and alerts |
| USER | Standard access to the dashboard and their own data |

## Security Notes

- Do not reuse the demo password outside a local development database.
- Production admin accounts must be provisioned through an authorized operational process, not through public registration or the demo seed.
- Keep `.env` files out of version control and use a strong, unique JWT secret.

## Roadmap

- [x] JWT authentication with role-based access control
- [x] CRUD for transactions, vendors and alerts
- [x] Modular rule-based risk scoring engine
- [x] Behavioral analysis service
- [ ] ML anomaly detection service (`ai-service`)
- [ ] Fraud probability prediction with XGBoost
- [ ] SHAP-based explanations for flagged transactions
- [ ] Automated tests and CI pipeline

## Contributing

Contributions are welcome. To contribute:

1. Fork the repository.
2. Create a feature branch: `git checkout -b feature/your-feature`.
3. Commit your changes and push the branch.
4. Open a pull request describing your changes.

For bugs or ideas, please open an issue first.

## License

MIT License

Copyright (c) 2026 Sayali Khatkar

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
