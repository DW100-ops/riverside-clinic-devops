# Incident Post-Mortem Report: Incorrect Operating Hours Published

## 1. Executive Summary

On Thursday evening, an emergency schedule update was manually deployed directly to the production server. Due to a typing error and lack of peer review, the website publicly listed the clinic as "Closed" on Friday, causing several patients to miss scheduled morning appointments. The issue was identified Friday morning, and operating hours were restored to normal.

## 2. Root Cause Analysis (5 Whys)

1. **Why were wrong hours displayed on the website?**
   - The live `hours.md` file stated the clinic was closed on Friday.
2. **Why was the wrong file uploaded to production?**
   - A team member manually edited and uploaded an unverified local copy directly to the production server.
3. **Why was the unverified file uploaded directly?**
   - There was no automated CI/CD pipeline or pull request review requirement blocking direct server modifications.
4. **Why was there no automated check or peer review?**
   - Website updates were historically treated as informal document edits rather than managed software releases.
5. **Why was there no formal process in place?**
   - The organization lacked standardized DevOps practices, automated validation checks, and centralized version control workflows.

## 3. Incident Timeline

- **Thursday, 18:00:** Manual file update performed directly on the production web server.
- **Friday, 08:00:** Patients arrive for scheduled appointments to find locked doors and website indicating clinic is closed.
- **Friday, 08:30:** Office staff notify IT of the public content error.
- **Friday, 08:45:** IT manually re-uploads the correct schedule file to production; site displays correct hours.
- **Friday, 10:00:** Incident closed; post-mortem initiated.

## 4. Preventative Measures & Long-Term Solutions

- **Enforce CI/CD Pipeline Controls:** Direct server edits are strictly prohibited. All content changes must go through GitHub feature branches and pull requests.
- **Automated Content Validation:** The GitHub Actions workflow automatically verifies that `hours.md` exists, is populated, and follows standard structural rules before any code can be merged.
- **Peer Review Policy:** Require at least one mandatory review from another team member on all pull requests before merging into `main`.
