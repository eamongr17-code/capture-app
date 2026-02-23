# Deploy Capture to GitHub Pages

## Quick Setup

1. Go to [GitHub repo settings](https://github.com/eamongr17-code/Dexter-personal-/settings/pages)
2. Under "Build and deployment":
   - **Source**: Deploy from a branch
   - **Branch**: `main`
   - **Folder**: `/capture`
3. Click **Save**
4. Wait ~1 minute for deployment
5. App will be live at: **https://eamongr17-code.github.io/Dexter-personal-/capture/**

## Alternative: Deploy from Root

If the above doesn't work (GitHub Pages doesn't always support subfolder deployment):

1. In repo settings, set:
   - **Branch**: `main`
   - **Folder**: `/ (root)`
2. Create a redirect at root:

```html
<!-- /index.html -->
<!DOCTYPE html>
<html>
<head>
  <meta http-equiv="refresh" content="0; url=capture/" />
</head>
<body>
  Redirecting to Capture...
</body>
</html>
```

3. Save and wait for deployment

## Manual Deployment (Alternative)

If you prefer a dedicated `gh-pages` branch:

```bash
cd /Users/dexterprimary/.openclaw/workspace

# Create gh-pages branch
git checkout -b gh-pages

# Copy only capture files to root
git rm -rf .
git checkout main -- capture/
mv capture/* .
rmdir capture

# Commit and push
git add -A
git commit -m "Deploy Capture to GitHub Pages"
git push origin gh-pages

# Switch back to main
git checkout main
```

Then in repo settings, set branch to `gh-pages` and folder to `/ (root)`.

## Test Locally

Before deploying, test locally:

```bash
cd /Users/dexterprimary/.openclaw/workspace/capture
python3 -m http.server 8000
```

Open: http://localhost:8000

## Troubleshooting

**404 on GitHub Pages?**
- Wait 1-2 minutes after enabling
- Check repo is public (or GitHub Pages is enabled for private repos)
- Verify branch and folder settings

**App loads but can't write to GitHub?**
- Check GitHub token has `repo` scope
- Verify token hasn't expired
- Check browser console for errors

**Offline mode not working?**
- Service worker needs HTTPS (works on localhost or GitHub Pages)
- Check browser dev tools > Application > Service Workers

---

**Once deployed**, the app will be at:
**https://eamongr17-code.github.io/Dexter-personal-/capture/**

Add to iPhone home screen for native-like experience!
