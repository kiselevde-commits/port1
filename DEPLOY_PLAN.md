# VOID_ARCH // SINGULARITY — Deployment Plan

## Project Overview
Single-page landing with pure CSS animations, Tailwind CDN, Google Fonts. No build step required — static HTML ready for GitHub Pages.

---

## File Structure
```
f:/Project/POrtfol4/
├── index.html          # Main entry point (provided)
├── .github/
│   └── workflows/
│       └── deploy.yml  # GitHub Actions workflow
├── README.md           # Project documentation
└── DEPLOY_PLAN.md      # This file
```

---

## 1. GitHub Pages Setup (Manual - One Time)

### Repository Settings
1. Create new repo on GitHub: `void-arch-singularity` (or your preferred name)
2. Go to **Settings → Pages**
3. Source: **Deploy from a branch**
4. Branch: `gh-pages` / `/(root)`
5. Save

### Enable GitHub Actions
- Settings → Actions → General → Allow all actions and reusable workflows

---

## 2. GitHub Actions Workflow (`.github/workflows/deploy.yml`)

```yaml
name: Deploy to GitHub Pages

on:
  push:
    branches: [main]
  workflow_dispatch:

permissions:
  contents: read
  pages: write
  id-token: write

concurrency:
  group: "pages"
  cancel-in-progress: true

jobs:
  deploy:
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v4

      - name: Setup Pages
        uses: actions/configure-pages@v4

      - name: Upload artifact
        uses: actions/upload-pages-artifact@v3
        with:
          path: '.'

      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v4
```

**Note:** Since this is pure static HTML, no build step. The workflow uploads the entire repo root as artifact.

---

## 3. Local Development & Testing

### Quick Preview
```bash
# Option 1: Python (built-in)
python -m http.server 8000

# Option 2: Node.js (npx serve)
npx serve .

# Option 3: VS Code Live Server extension
```

Open `http://localhost:8000` — verify animations, parallax, hover effects.

### Validation Checklist
- [ ] HTML5 valid (W3C Validator)
- [ ] No console errors
- [ ] Animations smooth (60fps)
- [ ] Mobile responsive (375px, 768px, 1440px)
- [ ] Fonts load correctly (Space Grotesk, Space Mono)
- [ ] Tailwind CDN loads (no CSP issues)
- [ ] Parallax works on mousemove
- [ ] Button hover animation works
- [ ] Scroll locked (intentional `overflow: hidden`)

---

## 4. Push to GitHub

```bash
cd f:/Project/POrtfol4
git init
git add .
git commit -m "feat: initial void-arch singularity landing"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/void-arch-singularity.git
git push -u origin main
```

**Trigger:** Push to `main` automatically runs workflow → deploys to `gh-pages` branch → live at `https://YOUR_USERNAME.github.io/void-arch-singularity/`

---

## 5. Custom Domain (Optional)

1. Add `CNAME` file to repo root:
   ```
   void-arch.example.com
   ```
2. DNS: Add CNAME record pointing to `YOUR_USERNAME.github.io`
3. GitHub Settings → Pages → Custom domain → Enforce HTTPS

---

## 6. Performance Notes

| Asset | Source | Optimization |
|-------|--------|--------------|
| Tailwind | CDN | Consider local build for production (remove unused) |
| Fonts | Google Fonts | Preconnect + `display=swap` already in place |
| Noise SVG | Inline data URI | Cached, no extra request |
| JS | Inline | < 1KB, no bundle needed |

**Lighthouse Target:** 100/100/100/100 (Performance, Accessibility, Best Practices, SEO)

---

## 7. Maintenance

- **Update content:** Edit `index.html` → push → auto-deploy
- **Add pages:** Create new `.html` files, link from main
- **Analytics:** Add Plausible/Umami script in `<head>`
- **CSP:** If needed, add `Content-Security-Policy` header via GitHub Pages `_headers` file (Netlify-style, not supported natively — consider Cloudflare Workers)

---

## Quick Commands Reference

```bash
# Clone & run locally
git clone https://github.com/YOUR_USERNAME/void-arch-singularity.git
cd void-arch-singularity
python -m http.server 8000

# Deploy manually (if Actions fail)
git subtree push --prefix . origin gh-pages

# Check workflow status
gh run list --workflow="Deploy to GitHub Pages"
```

---

## Status Tracker

- [x] `index.html` created
- [ ] `.github/workflows/deploy.yml` created
- [ ] `README.md` created
- [ ] Repository created on GitHub
- [ ] GitHub Pages configured
- [ ] First deploy successful
- [ ] Custom domain configured (optional)