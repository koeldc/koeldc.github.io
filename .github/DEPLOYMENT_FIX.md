# GitHub Pages Deployment Fix

This file was added to trigger a clean deployment and fix the gh-pages branch.

## Issue

The gh-pages branch had source code (Jekyll templates, \_layouts, \_config.yml, etc.) pushed to it directly,
causing the GitHub Pages build to fail with: `Unknown tag 'toc' in /_layouts/post.liquid`

### Root Cause

- gh-pages should only contain **built/compiled static HTML files**
- Someone pushed the **source code** from main branch to gh-pages
- GitHub Pages then tried to build these source files using standard Jekyll (without custom plugins)
- The site uses custom Jekyll plugins (like `{% toc %}` tag) that aren't available in GitHub's standard build environment
- This caused the build to fail

### Timeline

- **Last working commit** (2b825ffc): Contains only built static files (HTML, CSS, JS, assets)
- **Problematic commits** (8648994, e2234cd): Contains entire source code (\_layouts, \_config.yml, Gemfile, etc.)

## Solution

This commit triggers the deploy.yml workflow which will:

1. Build the site cleanly from the main branch using the custom Jekyll environment
2. Force-push the clean **built site** (\_site folder) to gh-pages (using JamesIves/github-pages-deploy-action)
3. Overwrite the corrupted source code commits on the gh-pages branch

## Prevention

**CRITICAL**: Never commit source code directly to the gh-pages branch!

- The gh-pages branch is automatically managed by the deploy.yml workflow
- gh-pages should only contain the **built site** (static HTML files)
- All changes should be made to the **main branch** only
- The deploy.yml workflow automatically builds and deploys to gh-pages
- To fix any deployment issues, trigger a rebuild from main (don't touch gh-pages!)

## How to Manually Trigger a Rebuild

If you need to force a rebuild without code changes:

1. Go to Actions tab
2. Select "Deploy site" workflow
3. Click "Run workflow" (requires workflow_dispatch to be enabled)
