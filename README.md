# 🌿 Verdant BI
### AI-Powered Self-Service Business Intelligence Platform

**Verdant BI** is a zero-configuration, AI-powered Business Intelligence platform that transforms raw sales spreadsheets into actionable business insights. It enables business owners and non-technical users to upload datasets, automate data cleaning, explore interactive dashboards, generate sales forecasts, segment customers, detect anomalies, and interact with their data through a grounded AI assistant.

The platform aims to simplify business analytics by combining data processing, machine learning, visualization, and natural-language interaction into a unified workspace.

## 🌐 Live Demo

Experience Verdant BI:

**verdant-bi.netlify.app**

Explore automated data cleaning, interactive dashboards,
machine learning insights, and AI-powered analytics.
---

## 📌 Table of Contents

- [Overview](#-overview)
- [Key Features](#-key-features)
- [Technology Stack](#-technology-stack)
- [System Architecture](#-system-architecture)
- [Project Structure](#-project-structure)
- [Getting Started](#-getting-started)
- [Application Modules](#-application-modules)
- [Testing and Validation](#-testing-and-validation)
- [Security and Data Protection](#-security-and-data-protection)
- [Deployment](#-deployment)
- [Current Implementation Status](#-current-implementation-status)
- [Future Improvements](#-future-improvements)

---

## 🚀 Overview

Traditional business intelligence tools often require technical knowledge, manual data preparation, and complex dashboard configuration.

Verdant BI addresses these challenges through an automated analytics workflow.

**How it works:**

1. **Upload Data:** Upload sales datasets in CSV or Excel format.
2. **Automated Cleaning:** Normalize columns, remove duplicate and empty records, parse dates, and handle missing values.
3. **Intelligent Column Detection:** Automatically identify important dataset columns and their analytical roles.
4. **Business Analytics:** Generate KPIs, interactive dashboards, and sales performance insights.
5. **Machine Learning:** Apply forecasting, customer segmentation, and anomaly detection algorithms.
6. **AI-Powered Interaction:** Ask natural-language questions and receive answers grounded in actual dataset information.
7. **Reporting and Sharing:** Export analytical reports and securely share results.

The platform is designed around a workspace-based architecture to support individual users and collaborative business teams.

---

## ✨ Key Features

### 1. Authentication and Workspace Management
- User registration and login.
- JWT-based session management.
- Automatically provisioned personal workspaces.
- Workspace membership isolation.
- Team workspace creation and management.
- Role-based access control.

### 2. Automated Data Cleaning
- CSV and XLSX file uploads.
- Drag-and-drop upload interface.
- Column name normalization.
- Empty and duplicate row removal.
- Date parsing and numeric conversion.
- Missing-value imputation.
- Automatic column-role detection.
- Manual column-role overrides.
- Idempotent uploads using content hashing.

### 3. Interactive Business Intelligence Dashboard
- Total Revenue.
- Total Orders.
- Average Order Value (AOV).
- Active Customers.
- Revenue trend visualization.
- Category-wise sales distribution.
- Date-range and regional filtering.
- Server-side aggregation and filtering.

### 4. Machine Learning and Advanced Analytics

**Sales Forecasting**
- Blended linear-trend and moving-average forecasting.
- Configurable prediction horizons: 7, 30, and 90 days.
- Non-negative forecast values.
- Dataset-specific forecast history.

**Customer Segmentation**
- RFM (Recency, Frequency, Monetary) analysis.
- Quantile-based scoring from 1 to 5.
- Six customer segment classifications.
- Customer distribution and revenue analysis.

**Anomaly Detection**
- Isolation Forest algorithm implemented from scratch.
- Revenue-based anomaly detection.
- Optional quantity-based analysis.
- Configurable anomaly contamination rate.
- Deterministic results using a fixed-seed pseudo-random generator.
- Anomaly scores and flagged-record visualization.

### 5. AI Business Intelligence Assistant
- Natural-language interaction with uploaded datasets.
- Data-grounded answers using actual dataset aggregates.
- Conversation history persistence.
- AI-generated chart specifications.
- Independent chart-grounding verification.
- Rejection of unverified chart specifications.
- Per-workspace rate limiting.
- Approximate context-token limits.

The current default implementation uses a deterministic mock LLM provider. A Groq-powered provider is also implemented but requires live API-key testing.

### 6. Reports and Secure Sharing
- Analytics Summary PDF.
- Sales Forecast PDF.
- Customer Segmentation PDF.
- Cleaned dataset XLSX export.
- Secure report-sharing links.
- Share-link expiration.
- Share-link revocation.
- Server-side authorization and access validation.

### 7. Team Collaboration
- Create collaborative workspaces.
- Invite team members through email.
- Invitation acceptance workflow.
- Owner and member roles.
- Server-side role enforcement.
- Workspace-level data isolation.

---

## 🛠️ Technology Stack

| Category | Technologies |
|---|---|
| Frontend | HTML5, CSS3, JavaScript |
| Backend | Node.js, Express-style local HTTP server |
| Database | SQLite-compatible local mock storage; PostgreSQL target schema |
| Authentication | JWT |
| AI Integration | Groq API (implemented, live testing pending), Mock LLM Provider |
| Machine Learning | Linear Trend, Moving Average, RFM Analysis, Isolation Forest |
| Data Processing | JavaScript-based cleaning and spreadsheet parsing |
| Data Visualization | Chart.js |
| PDF Generation | pdf-lib |
| Excel Processing | ExcelJS |
| Testing | Node.js Test Runner, Playwright |
| Deployment Target | InsForge Hosting / Vercel |
| Development Tools | Git, GitHub, VS Code, npm |

---

## 🏗️ System Architecture

Verdant BI follows a modular architecture that separates the frontend, application logic, analytics pipeline, and data storage.

### Current Architecture

The current implementation uses a local mock backend to simulate the target InsForge infrastructure.

```text
                 USER
                   |
                   v
        FRONTEND APPLICATION
          HTML / CSS / JS
                   |
                   v
          LOCAL MOCK SERVER
               (server/)
                   |
       +-----------+-----------+
       |           |           |
       v           v           v
   AUTHENTICATION DATA       AI CHAT
       |       PIPELINE         |
       |           |            |
       +-----------+------------+
                   |
                   v
           ANALYTICS ENGINE
                   |
       +-----------+-----------+
       |           |           |
       v           v           v
   FORECASTING   RFM       ISOLATION
                 ANALYSIS    FOREST
                   |
                   v
             DATA STORAGE
```

### Target Architecture

The planned production architecture uses:

- InsForge Authentication for user identity and sessions.
- InsForge PostgreSQL for structured application data.
- InsForge Storage for uploaded datasets and generated files.
- InsForge Edge Functions for backend processing.
- InsForge AI Gateway for LLM integration.

The migration is documented in `docs/architecture.md`.

---

## 📂 Project Structure

```text
VERDANT-AI/
│
├── public/
│   ├── index.html
│   ├── login.html
│   ├── upload.html
│   ├── dashboard.html
│   ├── insights.html
│   ├── chat.html
│   ├── reports.html
│   ├── shares.html
│   ├── team.html
│   ├── profile.html
│   ├── css/
│   └── js/
│       └── lib/
│           └── dom-safe.js
│
├── server/
│   ├── pipeline/
│   │   ├── clean-dataset.js
│   │   ├── detect-columns.js
│   │   └── parse-spreadsheet.js
│   ├── llm/
│   │   ├── mock-provider.js
│   │   └── groq-provider.js
│   └── storage.js
│
├── functions/
│   └── InsForge Edge Function placeholders
│
├── db/
│   └── schema.sql
│
├── tests/
│   ├── fixtures/
│   └── *.test.js
│
├── docs/
│   ├── architecture.md
│   └── edge-function-contracts.md
│
├── .env.example
├── package.json
└── README.md
```

---

## ⚙️ Getting Started

### Prerequisites

Make sure you have the following installed:

- Node.js
- npm
- Git
- A code editor such as Visual Studio Code

### 1. Clone the Repository

```bash
git clone https://github.com/itsnikh10dev/Verdant-BI.git
```

### 2. Navigate to the Project Directory

```bash
cd Verdant-BI
```

### 3. Install Dependencies

```bash
npm install
```

### 4. Configure Environment Variables

Create your local environment file:

```bash
cp .env.example .env
```

Configure at least the required `JWT_SECRET` value in `.env`.

For Windows PowerShell, you can also use:

```powershell
Copy-Item .env.example .env
```

### 5. Start the Application

```bash
npm run dev
```

The application starts the local mock backend and serves the frontend on port `5175`.

### 6. Open the Application

Navigate to:

```text
http://localhost:5175/login.html
```

Register a new account and start exploring Verdant BI.

---

## 📊 Application Modules

| Module | Page | Description |
|---|---|---|
| Authentication | login.html | Registration and login |
| Home | index.html | Main application workspace |
| Data Upload | upload.html | Dataset upload and cleaning |
| Dashboard | dashboard.html | KPIs and business visualizations |
| Insights | insights.html | Forecasting, RFM, and anomaly detection |
| AI Assistant | chat.html | Natural-language data interaction |
| Reports | reports.html | PDF and Excel report generation |
| Sharing | shares.html | Secure report sharing |
| Team | team.html | Team workspace and invitations |
| Profile | profile.html | Account information and activity |

---

## 🧪 Testing and Validation

Verdant BI includes an automated testing suite built using Node.js's native test runner.

Run the complete test suite:

```bash
npm test
```

**Current test coverage: 86 automated tests**

The test suite covers:

- Authentication and workspace isolation.
- Data cleaning and column detection.
- Upload validation and edge cases.
- KPI calculations and dashboard filtering.
- Sales forecasting.
- RFM customer segmentation.
- Isolation Forest anomaly detection.
- AI response grounding.
- Chart verification.
- Report generation and file integrity.
- Secure sharing and expiration.
- Team invitations and role enforcement.
- Cross-site scripting (XSS) protection.

A consolidated Playwright browser test also validates the main application workflow, from registration and dataset upload through analytics, AI chat, reporting, and team management.

The documented test results are against the local mock backend.

---

## 🔐 Security and Data Protection

Security is integrated into the application's architecture.

Key measures include:

- JWT-based authentication.
- Workspace-level data isolation.
- Server-side membership validation.
- Owner-based authorization for sensitive operations.
- Secure share-link expiration and revocation.
- Server-side validation of uploaded files.
- Frontend XSS protection using safe DOM rendering.
- No exposure of the Groq API key through public configuration.
- Environment-based secret management.

**Important:** Never commit `.env` files, API keys, service-role credentials, or other sensitive configuration to GitHub.

---

## ☁️ Deployment

The current application is designed to run locally using the mock backend.

The production deployment target is InsForge, with its managed hosting, PostgreSQL database, authentication, storage, and Edge Functions.

The documented deployment workflow is:

```bash
npx @insforge/cli
```

Configure browser-safe environment values:

```bash
npx @insforge/cli deployments env set PROJECT_URL=... ANON_KEY=...
```

Deploy the static frontend:

```bash
npx @insforge/cli deployments deploy ./public
```

**Deployment status:** These commands are documented as the planned deployment workflow but have not yet been executed against a live InsForge project. Verify the current CLI syntax and configuration against InsForge documentation before deployment.

A separate Vercel deployment of the static frontend is also possible, subject to configuring the backend's allowed CORS origins.

---

## 📍 Current Implementation Status

The project has completed all 10 planned development milestones against the local mock backend.

| Component | Status |
|---|---|
| Authentication | Implemented |
| Workspace Management | Implemented |
| Data Upload and Cleaning | Implemented |
| Column Detection | Implemented |
| Interactive Dashboard | Implemented |
| Sales Forecasting | Implemented |
| RFM Segmentation | Implemented |
| Isolation Forest | Implemented |
| AI Chat | Mock provider implemented |
| Chart Grounding | Implemented |
| PDF and Excel Reports | Implemented |
| Secure Sharing | Implemented |
| Team Collaboration | Implemented |
| Automated Testing | 86 tests |
| Responsive UI | Implemented |
| InsForge Integration | Pending |
| Live Groq API Validation | Pending |

### Important Implementation Notes

The current build is functional against its local mock backend. The following production integrations remain:

1. **InsForge:** No live InsForge project is connected. The PostgreSQL schema and Edge Function contracts are prepared, but actual backend migration and deployment remain pending.
2. **Groq:** The Groq provider is implemented, but it has not been validated using a live API key.
3. **Edge Functions:** The `functions/` directory contains placeholders. Equivalent backend logic currently runs through `server/pipeline/`.

For additional technical details, refer to:

- `docs/architecture.md`
- `docs/edge-function-contracts.md`

---

## 🔮 Future Improvements

Potential future development directions include:

- Complete migration to the production InsForge backend.
- Live LLM integration and validation.
- Advanced AI-driven business recommendations.
- Additional forecasting models and evaluation metrics.
- More advanced customer analytics.
- Expanded visualization and reporting capabilities.
- Production deployment and performance optimization.

---

## 👨‍💻 Author

**Nikhil Sharma**

GitHub: [@itsnikh10dev](https://github.com/itsnikh10dev)

---

## 📄 License

Add an appropriate open-source license to the repository before distributing the project. Until then, no specific license is declared.

---

**Verdant BI — Transforming Business Data into Actionable Intelligence.** 🌿
