# 📋 GitHub Pages Deployment - Cheat Sheet

**Author:** Najib Nawabi (SyntaxDevopsSquad-SDS)  
**Date:** March 17, 2026  
**Project:** DevOps Course - KEA Copenhagen

---

## Quick Setup (5 minutter)

### 1. Opret Repository

```bash
# Opret nyt repo
gh repo create

# Clone det
gh repo clone <username>/<repo-name>
cd <repo-name>
```

---

### 2. Opret index.html

```bash
# Opret HTML fil i root
nano index.html
```

**Minimal template:**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>My GitHub Pages Site</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            max-width: 800px;
            margin: 50px auto;
            padding: 20px;
        }
    </style>
</head>
<body>
    <h1> Welcome to My Site</h1>
    <p>Deployed via GitHub Pages!</p>
    <img src="./images/diagram.png" alt="Diagram" />
</body>
</html>
```

---

### 3. Opret Workflow

```bash
# Opret workflow folder
mkdir -p .github/workflows

# Opret workflow fil
nano .github/workflows/deploy_to_github_pages.yml
```

**Workflow template:**

```yaml
name: Deploy to GitHub Pages

on:
  push:
    branches:
      - main

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      - name: Deploy to GitHub Pages
        uses: JamesIves/github-pages-deploy-action@v4
        with:
          branch: gh-pages
          folder: .
```

---

### 4. Tilføj Images (Optional)

```bash
# Opret images folder
mkdir images

# Tilføj billeder
cp /path/to/image.png images/
```

**Link til billeder i HTML:**

```html
<img src="./images/your-image.png" alt="Description" />
```

---

### 5. Commit og Push

```bash
# Add alle filer
git add .

# Commit
git commit -m "feat: initial GitHub Pages deployment"

# Push
git push origin main
```

---

### 6. Enable GitHub Pages på GitHub

1. **Gå til repo → Settings (⚙️)**
2. **Click "Pages" (venstre sidebar)**
3. **Under "Build and deployment":**
   - Source: `Deploy from a branch`
   - Branch: `gh-pages`
   - Folder: `/ (root)`
4. **Click "Save"**

---

### 7. Fix Permissions (hvis deployment fejler)

**Fejl: "Permission denied to github-actions[bot]"**

**Fix:**

1. **Settings → Actions → General**
2. **Scroll til "Workflow permissions"**
3. **Vælg: "Read and write permissions"** ✅
4. **Click "Save"**
5. **Re-run workflow** eller push en ny commit

---

### 8. Access Siden

**URL format:**

```
https://<username>.github.io/<repo-name>/
```

**Eksempel:**

```
https://codebynajib.github.io/github-pages-test/
```

⏱️ **Første deployment:** 1-3 minutter  
⏱️ **Efterfølgende:** 30-60 sekunder

---

## Troubleshooting

### Problem: Site not found (404)

**Fix:**

- Vent 2-3 minutter mere
- Check Settings → Pages viser: "Your site is live at..."
- Verificer `gh-pages` branch eksisterer

---

### Problem: Changes ikke synlige

**Fix:**

```bash
# Force refresh browser
Ctrl + Shift + R  (Windows/Linux)
Cmd + Shift + R   (Mac)

# Clear browser cache
# Eller brug incognito mode
```

---

### Problem: Custom domain redirect

**Fix:**

1. Settings → Pages
2. Under "Custom domain" - **slet domænet**
3. Click "Save"
4. Vent 1 minut og refresh

---

### Problem: Workflow fejler

**Check:**

```bash
# Se workflow logs på GitHub
# Actions tab → Click på failed workflow → Se fejl

# Common fixes:
# 1. Enable write permissions (se step 7)
# 2. Verificer YAML syntax (ingen tabs, kun spaces)
# 3. Check branch name er 'main' ikke 'master'
```

---

## 📁 Project Structure

```
repo-name/
├── .github/
│   └── workflows/
│       └── deploy_to_github_pages.yml
├── images/
│   └── diagram.png
├── index.html
└── README.md
```

---

## ⚡ Pro Tips

### Auto-format HTML

```bash
# Install prettier
npm install -g prettier

# Format HTML
prettier --write index.html
```

---

### Test lokalt før deploy

```bash
# Simple HTTP server
python3 -m http.server 8000

# Åbn browser: http://localhost:8000
```

---

### Deploy subdirectory kun

```yaml
# I workflow yml
with:
  branch: gh-pages
  folder: ./dist  # Deploy kun dist folder
```

---

### Custom 404 page

```bash
# Opret 404.html i root
nano 404.html
```

```html
<!DOCTYPE html>
<html>
<head>
    <title>404 - Page Not Found</title>
</head>
<body>
    <h1> Page Not Found</h1>
    <p><a href="/">Go Home</a></p>
</body>
</html>
```

---

## 🧹 Cleanup

### Slet Repository

```bash
# Via GitHub CLI
gh repo delete <username>/<repo-name>

# Confirm: yes
```

---

### Disable GitHub Pages (behold repo)

1. Settings → Pages
2. Source: `None`
3. Save

---

## Useful Links

- **GitHub Pages Docs:** https://docs.github.com/en/pages
- **Deploy Action:** https://github.com/JamesIves/github-pages-deploy-action
- **Custom Domains:** https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site

---

##  Common Use Cases

### Portfolio Site

```html
<!-- index.html -->
<section id="projects">
    <h2>My Projects</h2>
    <!-- Project cards -->
</section>
```

---

### Documentation

```bash
# Generate from markdown
# Use Jekyll, MkDocs, eller Docusaurus
```

---

### Landing Page

```html
<!-- Hero section -->
<header class="hero">
    <h1>Product Name</h1>
    <p>Tagline</p>
    <button>Get Started</button>
</header>
```

---

##  Notes

- GitHub Pages er kun for **statiske** sites (HTML, CSS, JS)
- Kan ikke køre backend servers (Node.js, Python, etc.)
- Gratis hosting for public repositories
- Custom domains understøttes (kræver DNS opsætning)
- HTTPS er enabled automatisk

---

##  Checklist

- [ ] Repository oprettet
- [ ] index.html created
- [ ] Workflow fil oprettet
- [ ] Committed og pushed
- [ ] GitHub Pages enabled
- [ ] Permissions sat til "Read and write"
- [ ] Workflow kørt succesfuldt
- [ ] Side tilgængelig på URL

---

**Made with ❤️ by SyntaxDevopsSquad**  
**EK Copenhagen - DevOps 2026**
