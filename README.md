# The PLA Group — Website

Marketing site for **The Project Leadership Advisory Group**
(`usetheplagroup.com`).

- Framework: [Astro](https://astro.build) (static output)
- Hosting: GitHub Pages
- Design system: adapted from Refero's INVERSA style — INVERSA typography and
  spacing are kept 1:1; only the color palette is swapped to match the PLA
  logo (navy + gold).

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

**One-time setup after pushing to a GitHub remote:**

1. Repo → **Settings → Pages → Build and deployment → Source**:
   `GitHub Actions` (required — do not select "Deploy from a branch").
2. First push to `main` (or manually trigger the workflow) will run the
   `Deploy to GitHub Pages` action and expose the site at
   `https://<gh-user>.github.io/<repo>/` — the workflow will then publish it
   at the custom domain below.

### Custom domain / DNS

`public/CNAME` contains `usetheplagroup.com`, which GitHub Pages picks up
automatically.

At Cloudflare (DNS for `usetheplagroup.com`):

- **CNAME** `usetheplagroup.com` → `<gh-user>.github.io`
- Proxy status: **DNS only** (grey cloud). Cloudflare's orange-cloud proxy
  breaks GitHub Pages' automatic HTTPS provisioning; leave it off, at least
  until Pages has issued a Let's Encrypt cert and the "Enforce HTTPS"
  checkbox in Settings → Pages is ticked.
- Apex domain? Use Cloudflare's `CNAME flattening` on the root, or point
  four `A` records at GitHub's Pages IPs (`185.199.108.153`,
  `185.199.109.153`, `185.199.110.153`, `185.199.111.153`).

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

Type: **NB International Pro** primary, **JetBrains Mono** for captions and
UI. NB is a paid Neubau font — the site currently falls back to Söhne /
Inter / system-ui until it's licensed and self-hosted (see TODOs below).

---

## TODOs

- [ ] License **NB International Pro** from Neubau, self-host the woff2
      files under `src/assets/fonts/`, and register them via `@font-face` in
      `global.css`. Currently the primary stack falls back to Söhne / Inter
      / system-ui.
- [ ] Replace the placeholder Unsplash hero and full-bleed band images
      (`src/components/Hero.astro`, `src/pages/index.astro`) with licensed,
      self-hosted photography under `public/images/`.
- [ ] Finalize copy — the current landing text is a rough draft; Juan will
      rewrite for tone.
- [ ] Confirm the GitHub org / repo (likely under `crushcitycoder` — the
      `teamplagroup` org does not exist yet at scaffold time).
- [ ] Set up a form provider (Formspree, Basin, or a Cloudflare Worker) for
      the contact CTA if a `mailto:` link isn't sufficient.
- [ ] Add real favicon set (`.ico`, apple-touch-icon, OG image).
