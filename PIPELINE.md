# Riverside Community Clinic - CI Pipeline Documentation

## 1. Pipeline Overview

This GitHub Actions workflow automates the validation of all content changes pushed to the repository. It runs automatically on every pull request and push to ensure that updates (such as operating hours or service descriptions) are properly verified before they can be merged into the production branch.

## 2. Step-by-Step Breakdown

- **Trigger (`on:`):** Configured to execute on pushes and pull requests across main and feature branches.
- **Checkout (`actions/checkout@v4`):** Clones the repository code into the runner's virtual environment so validation scripts can access the latest files.
- **Environment Setup (`run:`):** Outputs system confirmation and lists repository contents to verify workspace health.
- **Custom Clinic Check:** A custom bash script that specifically targets `hours.md`. It verifies two critical rules:
  1. That the file physically exists in the repository.
  2. That the file is not empty (size greater than zero bytes). If either condition fails, the script exits with a non-zero code, instantly failing the build and blocking deployment.

## 3. Proposed Next Steps for Pipeline Expansion

1. **Automated Markdown Linting:** Integrate a linter step to ensure all clinic documentation and content files follow consistent style and syntax rules.
2. **Staging Environment Auto-Deployment:** Expand the pipeline to automatically deploy passing changes to a staging URL for the clinic manager to preview before final production release.
