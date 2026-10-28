# Riverside Community Clinic - DevOps Transformation & CI/CD Pipeline

[![Clinic Content CI](https://github.com/DW100-ops/riverside-clinic-devops/actions/workflows/ci.yml/badge.svg)](https://github.com/DW100-ops/riverside-clinic-devops/actions)

## 📌 Project Overview

Riverside Community Clinic provides vital health services to the local community. Historically, website updates were performed manually on live web servers, leading to operational risks, unverified content deployments, and schedule inaccuracies.

This repository establishes a modern DevOps workflow using **Git version control**, **GitHub Actions CI/CD automation**, and **structured incident response protocols** to ensure all public content updates are verified, peer-reviewed, and traceably deployed.

---

## 📂 Repository Deliverables

| File / Folder                  | Description                                                                                                                               |
| :----------------------------- | :---------------------------------------------------------------------------------------------------------------------------------------- |
| **`PLAN.md`**                  | Operational transformation plan featuring the 8-stage DevOps lifecycle, CALMS framework assessment, user stories, and Definition of Done. |
| **`.github/workflows/ci.yml`** | GitHub Actions pipeline executing automated content checks on push and pull request events.                                               |
| **`hours.md`**                 | Clinic operating hours content file, automatically validated by the CI pipeline for existence and content integrity.                      |
| **`services.md`**              | Primary clinic services summary file.                                                                                                     |
| **`PIPELINE.md`**              | Technical documentation breaking down pipeline execution steps and outlining future automation roadmaps.                                  |
| **`INCIDENT.md`**              | Post-mortem incident analysis using the **5 Whys** method to diagnose past production deployment errors and set preventative controls.    |
| **`REPORT.md`**                | Executive summary tailored for clinic leadership, connecting DevOps controls to business benefits, alongside student project reflections. |

---

## ⚙️ Automated CI/CD Pipeline Overview

The GitHub Actions workflow (`.github/workflows/ci.yml`) enforces quality gates on all proposed changes before they can be merged into `main`:

1. **Trigger:** Executes automatically on pushes and pull requests across all branches.
2. **Environment Setup:** Clones repository source code and initializes the Linux test runner.
3. **Custom Content Check:** Executes a custom bash script that verifies `hours.md` exists and contains non-zero byte content (`[ -s "hours.md" ]`). If the file is missing or empty, the build exits with code `1`, blocking the pull request.

---

## 🚀 Branching & Development Workflow

To maintain a clean production history, direct commits to `main` are restricted. All updates follow a standard feature-branch workflow:

1. Create a feature branch (`git checkout -b feature/your-feature-name`).
2. Make edits and test locally.
3. Push the feature branch and open a **Pull Request (PR)** on GitHub.
4. Verify that the GitHub Actions CI workflow passes **GREEN**.
5. Peer review and merge into `main`.

---

## 👤 Author

**Dennis Walsh**  
_DevOps & AI Foundations Final Project_
