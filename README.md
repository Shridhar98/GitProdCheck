# GitProdCheck

GitProdCheck is a minimal, production-check workflow for a static website. The repository contains a simple static site (`index.html`) and a GitHub Actions workflow that automatically deploys the site to GitHub Pages whenever `index.html` is changed on the `main` branch.

This project is useful as a tiny starter for experimenting with GitHub Pages, testing automatic deployments, and learning how to wire a repository so changes to a single file trigger a production deployment.

## Contents

- `index.html` — A simple responsive HTML5 starter page (the site that will be published).
- `.github/workflows/static.yml` — GitHub Actions workflow that uploads the repository and deploys it to GitHub Pages when `index.html` is changed on `main`.

## Quickstart (local)

1. Preview the site locally by opening `index.html` in your browser (no server required for basic HTML/CSS/JS):

	 - In File Explorer: double-click `index.html`.
	 - Or from PowerShell:

		 ```powershell
		 start .\index.html
		 ```

2. Make changes to `index.html` (or other files).

3. Commit and push your changes to the repository. Example PowerShell commands:

	 ```powershell
	 git add index.html
	 git commit -m "Update index.html: <short description>"
	 git push origin main
	 ```

	 If this is the first time pushing the branch to the remote, use:

	 ```powershell
	 git push -u origin main
	 ```

## CI / Deployment (GitHub Pages)

- The workflow `.github/workflows/static.yml` is configured to run on pushes to `main` that include changes to `index.html`.
- When triggered, the workflow checks out the repo, builds/uploads an artifact (in this case the repository contents), and uses the `actions/deploy-pages` action to publish the site to GitHub Pages.
- The published site URL will appear in the Actions job output and the repository's Pages settings.

Notes:

- Ensure the repository's `main` branch is the branch configured for the workflow (the workflow currently listens to `branches: ["main"]`). If you use a different default branch, update the workflow accordingly.
- The workflow requires that GitHub Pages is enabled for the repository and that the `GITHUB_TOKEN` has Pages permissions (the workflow sets the required permissions already).

## Troubleshooting

- If the workflow does not run after pushing changes to `index.html`:
	- Confirm the change was pushed to `main` (check `git status` and `git log -n 3`).
	- Go to the repository's **Actions** tab on GitHub and inspect the most recent run for errors.
	- Check **Settings → Pages** in the repository to ensure Pages is enabled and the published site has the expected source.

- If the published site shows a previous version or 404:
	- Make sure `index.html` is at the repository root and that the workflow successfully completed.
	- Re-run the workflow manually from the Actions tab (workflow_dispatch is enabled).

## Development notes

- The HTML uses simple CSS variables (in `:root`) for quick styling changes. Edit `--bg` or `--accent` to change site colors.
- This repo is intentionally minimal so the Pages workflow publishes the repository as-is. If you need a build step (Sass, bundling, or static site generator), modify the workflow to run the build and upload only the build output.

## Author

Repository maintained by the project owner.

---

If you want, I can:

- update the workflow to deploy on changes to any file (not just `index.html`),
- add a simple local preview server command (Node, Python), or
- change the Pages workflow to publish a specific `build/` folder after running a build step.

Tell me which of these you'd like and I'll update the repo.
