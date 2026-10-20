# VOID_ARCH // SINGULARITY

> Архитектура нулевого сопротивления. Сингулярность интерфейса.

[![Deploy to GitHub Pages](https://github.com/YOUR_USERNAME/void-arch-singularity/actions/workflows/deploy.yml/badge.svg)](https://github.com/YOUR_USERNAME/void-arch-singularity/actions/workflows/deploy.yml)

## 🌐 Live Demo
**https://YOUR_USERNAME.github.io/void-arch-singularity/**

---

## ✨ Features

- **Pure CSS Quantum Core** — rotating rings, pulse glow, zero JS animations
- **Cursor Parallax** — core follows mouse movement
- **Staggered Reveal Animations** — monument easing (`cubic-bezier(0.16, 1, 0.3, 1)`)
- **Tactical Noise Layer** — SVG fractal noise overlay
- **Swiss Grid Typography** — Space Grotesk + Space Mono
- **Magnetic Data Cells** — hover-activated accent lines
- **Zero Build Step** — pure static HTML, deploy anywhere

---

## 🚀 Quick Start

### Local Development
```bash
# Clone
git clone https://github.com/YOUR_USERNAME/void-arch-singularity.git
cd void-arch-singularity

# Serve locally (any static server)
python -m http.server 8000
# or
npx serve .
# or use VS Code "Live Server" extension
```

Open `http://localhost:8000`

---

## 📦 Deployment (GitHub Pages)

### Automatic (Recommended)
1. **Push to `main`** — GitHub Action builds & deploys automatically
2. **Check Actions tab** — monitor deploy status
3. **Live at** `https://YOUR_USERNAME.github.io/void-arch-singularity/`

### Manual Setup (One-time)
1. Create repo on GitHub
2. Enable **GitHub Pages**: Settings → Pages → Source: "GitHub Actions"
3. Push code — workflow `.github/workflows/deploy.yml` handles the rest

### Workflow File (`.github/workflows/deploy.yml`)
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
      - uses: actions/checkout@v4
      - uses: actions/configure-pages@v4
      - uses: actions/upload-pages-artifact@v3
        with:
          path: '.'
      - uses: actions/deploy-pages@v4
```

---

## 🛠 Tech Stack

| Layer | Technology |
|-------|------------|
| Structure | Semantic HTML5 |
| Styling | Tailwind CSS (CDN) + Custom CSS Variables |
| Fonts | Google Fonts: Space Grotesk, Space Mono |
| Animations | Pure CSS `@keyframes` + `transition` |
| Interactions | Vanilla JS (parallax, reveal trigger) |
| Deploy | GitHub Actions → GitHub Pages |

---

## 📁 Project Structure

```
.
├── index.html              # Single-page application
├── .github/
│   └── workflows/
│       └── deploy.yml      # GitHub Actions workflow
├── README.md               # This file
└── DEPLOY_PLAN.md          # Detailed deployment guide
```

---

## 🎨 Customization

### Colors (CSS Variables in `<style>`)
```css
:root {
  --bg-deep: #050505;      /* Background */
  --text-pure: #F3F4F6;    /* Primary text */
  --text-muted: #6B7280;   /* Secondary text */
  --ease-monument: cubic-bezier(0.16, 1, 0.3, 1);
}
```

### Content
Edit text directly in `index.html`:
- Hero title (`h1`)
- Philosophy / Technology descriptions
- Footer copyright
- Button label

### Animations
Adjust `@keyframes` durations:
- `rotate-ring`: 40s / 60s (ring rotation speed)
- `pulse-glow`: 8s (core breathing)
- `reveal-text`: 1.2s (stagger delay via inline `transition-delay`)

---

## 📱 Browser Support

| Browser | Version |
|---------|---------|
| Chrome | 90+ |
| Firefox | 88+ |
| Safari | 14+ |
| Edge | 90+ |

Requires: CSS Custom Properties, `clamp()`, `cubic-bezier`, IntersectionObserver (not used — load-based reveal)

---

## 📄 License

MIT © 2026 VOID_ARCH INITIATIVE

---

## 🤝 Contributing

1. Fork
2. Create feature branch (`git checkout -b feature/amazing`)
3. Commit (`git commit -m 'feat: amazing'`)
4. Push (`git push origin feature/amazing`)
5. Open Pull Request

---

*Built with precision. Deployed with intent.*