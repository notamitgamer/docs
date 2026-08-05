---
label: Customization
order: 780
---

# Customization

## Filter repositories

Open `build.sh` and find the `gh repo list` command. The `select` statement controls which repos are excluded — by default it skips `git-mirror`, `register`, and `osma`:

```bash
REPOS_JSON=$(gh repo list "$USERNAME" --visibility=public --limit 100 --json name,description -q '.[] | select(.name != "git-mirror" and .name != "register" and .name != "osma")')
```

Edit the `select` conditions to hide forks or other specific project names.

## Styling & assets

Replace or edit the files inside `assets/`:

- `style.css`
- `logo.png`
- `favicon.png`

These get copied into the site root and into every generated repo subfolder during the build.

## Custom domain

If you're using a custom domain, create a file named `CNAME` in the repository root containing your domain name. The build script automatically copies it to the site output and uses it to build `sitemap.xml` URLs.

Continue to [How the Build Works](build-process.md).
