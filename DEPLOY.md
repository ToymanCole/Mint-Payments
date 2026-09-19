# Publish Mint on GitHub Pages

The app includes Anait’s updated profile and all interactive prototype features. No API keys, installation or build step is needed. This remains a mock payment app after deployment.

## Easiest: upload through GitHub

1. Sign in to https://github.com/new and create a **public** repository named `mint-payments`.
2. Extract the supplied ZIP on your computer.
3. In the repository, choose **Add file → Upload files**. Upload `index.html`, `README.md`, `DEPLOY.md` and `.nojekyll` from the extracted folder to the repository root, then commit to `main`. You can omit `.github` for this method.
4. Open **Settings → Pages**. Under **Build and deployment**, select **Deploy from a branch**, then **main** and **/ (root)**. Click **Save**.
5. Wait for the Pages deployment to finish. Settings → Pages will show the actual published link and a **Visit site** button.

For a repository named `mint-payments`, the usual URL is:
`https://YOUR-GITHUB-USERNAME.github.io/mint-payments/`

This is a URL template, not an already deployed website.

## Alternative: included GitHub Actions workflow

Upload all files, including `.github/workflows/deploy.yml`, to `main`. In **Settings → Pages**, choose **GitHub Actions** instead of branch deployment. Then run **Actions → Deploy Mint to GitHub Pages → Run workflow**. Future pushes to `main` redeploy automatically.

Use either branch publishing or GitHub Actions, not both.

## Command-line upload

After creating an empty repository, run in the extracted project directory:

```sh
git init -b main
git add .
git commit -m "Add Mint payment sandbox"
git remote add origin https://github.com/YOUR-GITHUB-USERNAME/mint-payments.git
git push -u origin main
```

Authenticate directly with GitHub on your own computer. Do not share access tokens, passwords or SSH private keys in chat.

See README.md for the mock-provider boundaries and the security infrastructure required before enabling real payments.
