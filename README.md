# The PLA Group — Website

Marketing site for **The Project Leadership Advisory Group**
(`usetheplagroup.com`).

- Framework: [Astro](https://astro.build) (static output)
- Hosting: GitHub Pages
- Design system: adapted from Refero's INVERSA style — INVERSA typography and
  spacing are kept 1:1; only the color palette is swapped to match the PLA
  logo (navy + gold).
- Repo: [teamplagroup/website](https://github.com/teamplagroup/website)

---

## Local development

```bash
npm install
npm run dev
```

Dev server: <http://localhost:4321>.

## Build

```bash
npm run build
```

Output goes to `dist/`. `npm run preview` serves that folder locally.

---

## Deployment (GitHub Pages)

Deployment is automated by `.github/workflows/deploy.yml` using the official
`withastro/action`. Every push to `main` builds the site and publishes it to
GitHub Pages.

**One-time setup after the first push:**

1. Repo → **Settings → Pages → Build and deployment → Source**:
   `GitHub Actions` (required — do not select "Deploy from a branch").
2. First push to `main` (or manually trigger the workflow) will run the
   `Deploy to GitHub Pages` action.

### Custom domain / DNS

`public/CNAME` contains `usetheplagroup.com`, which GitHub Pages picks up
automatically.

At Cloudflare (DNS for `usetheplagroup.com`):

- **CNAME** `@` (or `usetheplagroup.com`) → `teamplagroup.github.io`
- Proxy status: **DNS only** (grey cloud). Cloudflare's orange-cloud proxy
  breaks GitHub Pages' automatic HTTPS provisioning; leave it off, at least
  until Pages has issued a Let's Encrypt cert and the "Enforce HTTPS"
  checkbox in Settings → Pages is ticked.
- Cert provisioning typically takes ~24h after the CNAME propagates.

---

## Design tokens (see `src/styles/global.css`)

| Token              | Value      | Role                                  |
| ------------------ | ---------- | ------------------------------------- |
| `--pla-navy`       | `#1c2b4a`  | Page canvas, dark surfaces            |
| `--pla-gold`       | `#b8935a`  | Sole accent — CTAs, tags, highlights  |
| `--pla-gold-deep`  | `#8a6d3f`  | Gradient shade, hover state           |
| `--pla-vellum`     | `#f4f3e8`  | Primary text / headings               |
| `--pla-iron`       | `#404040`  | Hairlines                             |
| `--pla-ash`        | `#84837b`  | Muted text                            |

## Fonts

**Söhne** (Klim Type Foundry, licensed) is the primary face. Drop the
licensed woff2 files into `public/fonts/`:

- `public/fonts/soehne-buch.woff2` (weight 400)
- `public/fonts/soehne-kraftig.woff2` (weight 600)

Falls back to **Inter / system-ui** until those files are present. See
`public/fonts/README.md` for details.

Mono UI uses **JetBrains Mono**, self-hosted via `@fontsource/jetbrains-mono`.

---

## Contact form

`src/pages/contact.astro` posts to a Formspree placeholder endpoint
(`https://formspree.io/f/REPLACE_ME`). Swap the `action=` attribute for a
real endpoint before launch. A `mailto:` fallback is shown next to the
form in either case.

---

## TODOs

- [ ] License **Söhne** from Klim Type Foundry and drop the woff2 files into
      `public/fonts/`.
- [ ] Replace placeholder Unsplash imagery in `src/components/Hero.astro`,
      `src/pages/index.astro`, and `src/pages/about.astro` with licensed,
      self-hosted photography under `public/images/`.
- [ ] Replace the Formspree placeholder endpoint in
      `src/pages/contact.astro`.
- [ ] Add a real favicon set (`.ico`, apple-touch-icon, OG image).
- [ ] Optional: add an `/insights` route once there is content.
