---
label: Git Mirror
icon: repo-forked
order: 800
---

# Git Mirror Site Generator

An automated setup that generates a fast, static HTML mirror of your public GitHub repositories, using [`stagit`](https://codemadness.org/stagit.html) and GitHub Actions.

Instead of hitting the GitHub UI, this gives you a lightweight, self-hosted browsing experience for your repos — plain HTML, no JavaScript framework, no tracking, and fast to load.

## What it generates

For each public repo, the build produces:

- Standard `stagit` pages — **Log**, **Files**, **Refs**, plus **README**/**LICENSE** when present
- An added **Activity** page — clone URL, GitHub link, last commit, repo size, and a small commit-activity graph (SVG, dependency-free)
- A recursive, collapsible **folder tree** injected into `files.html` (with hash-based deep links to specific folders)
- Breadcrumb navigation on every individual file page
- A central `stagit-index` landing page listing all mirrored repos
- `sitemap.xml`, a styled `404.html`, and a build-info footer on every page (commit hash, build time, source)

## Get started

- [How to Fork & Deploy](deploy.md)
- [Customization](customization.md)
- [How the Build Works](build-process.md)
