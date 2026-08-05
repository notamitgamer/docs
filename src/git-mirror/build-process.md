---
label: How the Build Works
icon: gear
order: 770
---

# How the Build Works

`build.sh` runs the whole pipeline, driven by GitHub Actions. Here's what it does, step by step.

## 1. Setup & metadata

- Detects the repo owner (`GITHUB_REPOSITORY_OWNER`, falling back to `notamitgamer` locally)
- Resolves the site's base URL from a configured Pages CNAME, or falls back to `https://<username>.github.io`
- Captures the git-mirror repo's own commit hash and build timestamp for the footer

## 2. Copy root assets

`style.css`, `favicon.png`, `logo.png`, and `icon.png` are copied from `assets/` into the site root (with `favicon.png` also duplicated as `favicon.ico`).

## 3. Fetch & process each public repository

For every public repo (minus the filtered ones):

1. Clone it as a **bare repo** into `raw_repos/`
2. Overwrite stagit's placeholder `description` and `owner` files
3. Run `stagit` to generate the standard Log / Files / Refs / README / LICENSE pages
4. Copy `style.css`, `logo.png`, and `favicon.png` into that repo's subfolder
5. Inject an **Activity** link into stagit's nav bar on every generated page
6. Generate a custom `activity.html` page with:
   - Clone URL and GitHub link
   - Last commit hash + timestamp
   - Approximate repo size
   - A small dependency-free SVG bar graph of weekly commit activity
7. Inject a recursive, collapsible **folder tree** script into `files.html`, with hash-based URLs (`#folder=path/to/dir`) so specific folders can be linked directly and auto-expanded
8. Add a static **breadcrumb** to every individual file page under `file/`, built by walking the file's path
9. Write a `last_commit` file into the repo subfolder recording the mirror's build metadata

## 4. Generate the central index

`stagit-index` runs over all the bare repos to produce the root `site/index.html` landing page, listing every mirrored repository.

## 5. Site-wide finishing touches

- Injects a formatted build-info footer (owner, build time, git-mirror commit, stagit credit) into every generated HTML page
- Copies `CNAME` into the site output, if present
- Injects a mobile viewport meta tag into every page's `<head>`
- Generates `sitemap.xml` from every HTML file in the output
- Generates a styled `404.html`

The final output lands in `./site`, ready to be deployed via GitHub Pages.
