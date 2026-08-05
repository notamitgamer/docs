# How to Fork and Deploy

Follow these steps to create and host your own version of this repository mirror.

## 1. Fork the repository

Click **Fork** at the top right of [github.com/notamitgamer/git-mirror](https://github.com/notamitgamer/git-mirror) to create a copy under your own GitHub account.

## 2. Enable GitHub Actions

GitHub automatically disables workflows in forked repositories for security reasons.

1. Navigate to the **Actions** tab in your forked repository.
2. Click **"I understand my workflows, go ahead and enable them"**.

## 3. Configure GitHub Pages

1. Go to your repository **Settings**.
2. Click **Pages** in the left sidebar.
3. Under "Build and deployment", set the source to **GitHub Actions** (or the specific deployment branch, depending on how your workflow is configured to upload the `./site` directory).

## 4. Trigger the first build

1. Go back to the **Actions** tab.
2. Select the build/deploy workflow from the left sidebar.
3. Click **Run workflow** to fetch your repositories, generate the HTML, and deploy the site.

Continue to [Customization](customization.md).
