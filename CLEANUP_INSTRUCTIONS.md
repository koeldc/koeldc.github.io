# How to Remove Extra Branches

This repository has been set up with tools to remove the extra Copilot branches.

## Quick Start - Use the GitHub Actions Workflow

The easiest way to remove the extra branches is to use the automated workflow:

1. Go to the **Actions** tab in your GitHub repository: https://github.com/koeldc/koeldc.github.io/actions
2. Click on **"Cleanup Stale Branches"** workflow in the left sidebar
3. Click the **"Run workflow"** button (top right)
4. The default branches to delete are already filled in:
   - `copilot/add-new-news-posts`
   - `copilot/add-three-news-posts`
5. Click **"Run workflow"** to execute
6. Wait a few seconds for the workflow to complete

The workflow will automatically delete the specified branches while protecting `main` and `gh-pages`.

## Alternative: Manual Cleanup

If you prefer to delete branches manually, see the instructions in `BRANCH_CLEANUP.md`.

## What Gets Deleted

- ❌ `copilot/add-new-news-posts` - old feature branch
- ❌ `copilot/add-three-news-posts` - old feature branch

## What Stays

- ✅ `main` - default branch with source code
- ✅ `gh-pages` - GitHub Pages deployment branch (auto-updated by workflow)

## After Cleanup

After running the workflow, you should only see 2 branches in your repository:
- main
- gh-pages

Plus any current working branches (like `copilot/remove-extra-branches`).
