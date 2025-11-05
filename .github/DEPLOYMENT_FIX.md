# GitHub Pages Deployment Fix

This file was added to trigger a clean deployment and fix the gh-pages branch.

## Issue
The gh-pages branch had manually committed changes that introduced invalid Jekyll templates,
causing the GitHub Pages build to fail with: `Unknown tag 'toc' in /_layouts/post.liquid`

## Solution
This commit triggers the deploy.yml workflow which will:
1. Build the site cleanly from the main branch
2. Force-push the clean content to gh-pages (using JamesIves/github-pages-deploy-action)
3. Overwrite any corrupted commits on the gh-pages branch

## Prevention
- Never commit directly to the gh-pages branch
- The gh-pages branch is automatically managed by the deploy.yml workflow
- Any changes should be made to the main branch and will be automatically deployed
