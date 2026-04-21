# adarshsadanand.in

This repository contains the source code and project documentation for my personal web platform, live at [adarshsadanand.in](https://adarshsadanand.in).

The goal of this project is to build a complete, multi-tiered website that serves as a public portfolio, a private file drive, and a community forum. While it is a solo project, it is structured and documented like a standard development project.

---

## Access and Features

The site is divided into three access levels:

### Public Access
* **Landing Page:** A straightforward portfolio, basic greetings, and an "About Me" section.
* **Public Forum:** A space where visitors can read, write, and discuss topics.

### Friends Login
* **Shared Files:** Access to specific shared folders.
* **Gallery:** A private image gallery.

### Personal Login (Admin)
* **Drive:** Secure cloud storage for personal files, college documents, MTech coursework, and resumes.
* **Personal Blog:** A private space for notes and personal writing.
* **Remote Workspace:** Clientless, web-based remote access to an OCI-hosted Ubuntu system using Apache Guacamole.

---

## Tech Stack

The architecture is split to handle static pages, server-side logic, database management, and remote environments efficiently.

* **Domain:** adarshsadanand.in
* **Frontend Hosting:** GitHub Pages (for static and public-facing pages).
* **Application Hosting:** Vercel (for dynamic routing and API handling).
* **Backend & Database:** Supabase (utilizing PostgreSQL for user authentication, file storage metadata, and forum data).
* **Remote Infrastructure:** Oracle Cloud Infrastructure (OCI) hosting an Ubuntu instance, accessible via Apache Guacamole.
* **Scripting & Logic:** Python and JavaScript/TypeScript (depending on Vercel serverless function requirements).

---

## Project Guidelines

To maintain a clean and usable project, all code, documentation, and user interfaces must adhere to the following rules:

* Write clearly and directly in plain English.
* Use exactly one highly readable font family across the entire site.
* Maintain generous, consistent padding and margin.
* Keep line heights at a minimum of 1.5 for paragraph text to ensure readability.

---

## Documentation Structure

To treat this as a formal development project, the software development lifecycle and governance protocols are documented in the `/docs` folder.

### 1. `/requirements/` (Business & Functional Scope)
* **`BRD.md` (Business Requirements Document):** High-level business goals and target audience.
* **`FRD.md` (Functional Requirements Document):** Detailed user flows and feature logic.
* **`RTM.csv` (Requirements Traceability Matrix):** Grid mapping business goals to test cases to ensure full coverage.

### 2. `/architecture/` (Technical Blueprints)
* **`TRD.md` (Technical Requirements Document):** Tech stack, API endpoints, and infrastructure integration.
* **`CRD.md` (Component Requirements Document):** UI/UX specifications, design system, and typography rules.
* **`SystemDesign.md`:** Data flow diagrams and database schemas.
* **`/ADR/` (Architecture Decision Records):** Logs explaining why specific technical choices were made.

### 3. `/testing/` (Quality Assurance)
* **`QA_TestPlan.csv`:** Checklists for bug tracking and testing the login tiers.
* **`UAT_Signoff.md`:** User Acceptance Testing validation to confirm the system meets business goals.

### 4. `/operations/` (Deployment & Maintenance)
* **`DeploymentRunbook.md`:** Step-by-step CI/CD instructions and rollback procedures.
* **`ChangeLog.md`:** Version history and patch notes for every update.

### 5. `/grc/` (Governance, Risk & Compliance)
* **`RiskMatrix.csv`:** Security threat models and mitigation strategies.
* **`IRP.md` (Incident Response Plan):** Protocols for handling downtime or data loss.
* **`/SOPs/` (Standard Operating Procedures):** Routine maintenance checklists (e.g., database backups, key rotation).

### 6. `/legal/` (Policies & Liability)
* **`TermsOfService.md`:** Acceptable use rules for the public forum and friends tier.
* **`PrivacyPolicy.md`:** Details on user data collection and storage.
* **`DataPolicy.md`:** Rules regarding data retention, lifecycle, and deletion requests.

---

## Local Development

1. Clone the repository.
2. Install dependencies (refer to package manager instructions in the root).
3. Set up your local `.env` file with the Supabase API keys and Vercel environment variables.
4. Run the local development server.