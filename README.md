# Mountain Men: A Year in the Wild

An educational game for 4th grade Utah/Wyoming history. Students create a mountain man character, pack supplies, and survive a year in the 1830s Rocky Mountains through dice-based events.

Based on the Wyoming State Museum's "Year in the Life of the Mountain Men" curriculum.

## Live Demo

Once deployed: `https://YOUR-USERNAME.github.io/mountain-men-game/`

## How to Deploy to GitHub Pages

### Step 1: Create a GitHub Repository

1. Go to https://github.com and sign in (or create a free account)
2. Click the **+** button in the top right, then **New repository**
3. Name it **exactly**: `mountain-men-game`
4. Make it **Public**
5. **Don't** initialize with README (we already have files)
6. Click **Create repository**

### Step 2: Upload Your Files

You have two options:

#### Option A: Upload via GitHub Website (Easiest)

1. On your new repository page, click **uploading an existing file**
2. Drag and drop ALL the files from the `mountain-men-game` folder
3. Write a commit message like "Initial game upload"
4. Click **Commit changes**

#### Option B: Use Git Command Line

If you have Git installed:

```bash
cd mountain-men-game
git init
git add .
git commit -m "Initial commit"
git branch -M main
git remote add origin https://github.com/YOUR-USERNAME/mountain-men-game.git
git push -u origin main
```

### Step 3: Enable GitHub Pages

1. In your repository, click **Settings** (top menu)
2. Click **Pages** in the left sidebar
3. Under **Source**, select **GitHub Actions**
4. You're done! GitHub will now build and deploy automatically.

### Step 4: Set Up Automatic Deployment

Create this file in your repository: `.github/workflows/deploy.yml`

```yaml
name: Deploy to GitHub Pages

on:
  push:
    branches: [ main ]
  workflow_dispatch:

permissions:
  contents: read
  pages: write
  id-token: write

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with:
          node-version: 20
      - run: npm install
      - run: npm run build
      - uses: actions/upload-pages-artifact@v3
        with:
          path: ./dist

  deploy:
    needs: build
    runs-on: ubuntu-latest
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    steps:
      - uses: actions/deploy-pages@v4
        id: deployment
```

### Step 5: Access Your Game

After a few minutes, your game will be live at:

```
https://YOUR-USERNAME.github.io/mountain-men-game/
```

Every time you update files in the repository, GitHub will automatically rebuild and redeploy the game.

## Files Included

- `index.html` - Entry point
- `src/App.jsx` - Game code
- `src/main.jsx` - React mounting
- `package.json` - Dependencies
- `vite.config.js` - Build configuration

## Local Development

To run the game on your computer:

```bash
npm install
npm run dev
```

Then open http://localhost:5173 in your browser.

## Updating the Game

To make changes:

1. Edit the files in your repository
2. Commit the changes
3. GitHub will automatically rebuild and deploy

## Support

For questions about the historical content, see the Wyoming State Museum's original curriculum at:
https://wyomuseum.wyo.gov/index.php/school-programs-list/322-year-in-the-life-of-the-mountain-men
