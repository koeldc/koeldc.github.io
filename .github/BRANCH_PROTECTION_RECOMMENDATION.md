# Recommended Branch Protection Rules

To prevent the issue that occurred with gh-pages (where source code was accidentally pushed),
it's recommended to configure branch protection rules.

## For gh-pages branch

### Option 1: Restrict Push Access (Recommended)
1. Go to Settings → Branches → Add branch protection rule
2. Branch name pattern: `gh-pages`
3. Enable: "Restrict who can push to matching branches"
4. Allow only: GitHub Actions (or specific service accounts)
5. This prevents manual pushes while allowing the deploy.yml workflow to update gh-pages

### Option 2: Require Pull Requests
1. Go to Settings → Branches → Add branch protection rule
2. Branch name pattern: `gh-pages`
3. Enable: "Require a pull request before merging"
4. Enable: "Require status checks to pass"
5. This ensures any changes go through review

### Option 3: Lock the Branch
Since gh-pages should be fully automated:
1. Consider making gh-pages a "deploy branch" only
2. Document that it should never be modified manually
3. Use GitHub Actions bot user for all automated pushes

## For main branch

Consider enabling:
- Require pull request reviews
- Require status checks (deploy, tests, linting)
- Include administrators (enforce rules for everyone)

## Current Deploy Workflow

The `.github/workflows/deploy.yml` workflow:
- Triggers on pushes to main/master
- Builds the Jekyll site with custom plugins
- Deploys to gh-pages using `JamesIves/github-pages-deploy-action@v4`
- The action's `clean` parameter defaults to `true` (force overwrites gh-pages), though it's not explicitly set in the workflow configuration

This workflow has `workflow_dispatch` enabled, so it can be triggered manually if needed.
