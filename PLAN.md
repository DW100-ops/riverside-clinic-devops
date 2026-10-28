# Riverside Community Clinic - DevOps & Process Plan

## 1. Current Process Description

Currently, the Riverside Community Clinic's public website updates are handled manually on Thursday evenings by a part-time contractor who edits files directly on the live server. There is no version control system or staging environment. The only backup mechanism consists of manual folder copies named haphazardly (`site-old`, `site-old2`, and `site-old-FINAL`). Because changes lack documentation, automated verification, or rollback mechanisms, roughly one in four releases breaks the site and requires manually re-uploading an old backup folder.

## 2. Eight-Stage Lifecycle Mapping Table

| Lifecycle Stage  | Status | Notes / Evidence                                                                                           |
| :--------------- | :----- | :--------------------------------------------------------------------------------------------------------- |
| **1. Plan**      | Manual | Requirements and content changes are ad-hoc; no issue tracking or change management tickets.               |
| **2. Create**    | Manual | Contractor edits website files directly on the production server without a local development environment.  |
| **3. Verify**    | Absent | No automated testing or pre-deployment validation; errors are only discovered after going live.            |
| **4. Package**   | Absent | No artifact packaging or builds; files are individual raw text/HTML documents.                             |
| **5. Release**   | Manual | Manual file replacement on the production server every Thursday evening.                                   |
| **6. Configure** | Manual | Server configuration and environment setup are unmanaged and undocumented.                                 |
| **7. Monitor**   | Manual | Monitoring consists solely of patient complaints (e.g., discovering wrong opening hours the next morning). |
| **8. Respond**   | Manual | Incidents are resolved reactively by guessing and re-uploading an old backup folder (`site-old-FINAL`).    |

## 3. CALMS Assessment

- **Culture:** Weakest element. Operational knowledge is completely siloed with a single contractor, creating a culture of risk, fear of breaking changes, and lack of shared responsibility.
- **Automation:** Absent. Every phase from editing to deployment and backup recovery relies entirely on manual execution.
- **Lean:** Inefficient and wasteful. Frequent failures require rework, and roughly one in four changes must be reversed, wasting time and risking patient trust.
- **Measurement:** Absent. There are no tracking mechanisms, metrics, or logs to measure deployment frequency or failure rates.
- **Sharing:** Absent. No documentation, collaborative workflows, or knowledge transfer exist between staff, the contractor, and management.

## 4. User Stories

### Story 1 (Clinic Manager)

- **As a** clinic manager,
- **I want** all website content changes to be tracked and audited through version control,
- **So that** I can provide required operational documentation for our grant application and ensure accountability.
- **Acceptance Criteria:**
  1. Every change to website content must be committed to a version-controlled repository with a clear description of who made it and why.
  2. A designated second staff member must be able to review and inspect the history of changes at any time.

### Story 2 (Patient)

- **As a** patient,
- **I want** the online opening hours and service details to always be accurate,
- **So that** I never travel to the clinic when it is closed.
- **Acceptance Criteria:**
  1. Automated checks must validate that operating hours files are present and properly formatted before updates are published.
  2. Incorrect or empty schedule files must be caught and blocked prior to release.

### Story 3 (Office Coordinator)

- **As an** office coordinator,
- **I want** a reliable way to propose content updates without editing live production files directly,
- **So that** I can safely update opening hours or forms without fear of breaking the website.
- **Acceptance Criteria:**
  1. Content updates must be submitted via branches and pull requests rather than direct server edits.
  2. Automated validation checks must confirm the file structure is correct before merging.

### Story 4 (Contractor / System Operator)

- **As a contractor**,
- **I want** an automated pipeline that verifies content updates,
- **So that** syntax or missing files are caught automatically before reaching production.
- **Acceptance Criteria:**
  1. A GitHub Actions workflow must automatically run on every pull request and push.
  2. A failed verification check must block deployment and alert the author instantly.

## 5. Definition of Done

A website content change is considered "Done" when:

1. The content changes are written in Markdown and stored in the version-controlled repository.
2. A feature branch and pull request were used, avoiding direct edits to the main branch.
3. The automated CI pipeline runs successfully with all checks passing green.
4. The changes have been reviewed and approved by at least one other team member.
5. No confidential data, real patient info, or credentials exist anywhere in the commit history.
