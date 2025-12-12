# Branch Cleanup Documentation

## Current Branch Status

This repository currently has the following branches:

### Essential Branches (Keep)
- **main**: Default branch containing the source code
- **gh-pages**: Deployment branch used by GitHub Actions workflow for GitHub Pages hosting

### Extra Branches (Remove)
- **copilot/add-new-news-posts**: Completed feature branch that should be removed
- **copilot/add-three-news-posts**: Completed feature branch that should be removed

## Cleanup Instructions

To remove the extra branches, run the following commands:

```bash
# Delete remote branches
git push origin --delete copilot/add-new-news-posts
git push origin --delete copilot/add-three-news-posts

# If you have local copies, delete them too
git branch -d copilot/add-new-news-posts
git branch -d copilot/add-three-news-posts
```

## Using GitHub CLI

Alternatively, you can use the GitHub CLI:

```bash
gh api -X DELETE repos/koeldc/koeldc.github.io/git/refs/heads/copilot/add-new-news-posts
gh api -X DELETE repos/koeldc/koeldc.github.io/git/refs/heads/copilot/add-three-news-posts
```

## Via GitHub Web Interface

1. Go to https://github.com/koeldc/koeldc.github.io/branches
2. Find each branch to delete
3. Click the trash/delete icon next to the branch name
4. Confirm the deletion

## Why Keep gh-pages?

The `gh-pages` branch is automatically maintained by the GitHub Actions workflow defined in `.github/workflows/pages-deploy-fallback.yml`. This workflow deploys the site content from the `main` branch to `gh-pages` for hosting on GitHub Pages.
