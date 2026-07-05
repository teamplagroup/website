# The PLA Group — Website

Marketing site for **The Project Leadership Advisory Group**
(`usetheplagroup.com`).

- Framework: [Astro](https://astro.build) (static output)
- Hosting: **Cloudflare Pages** (project `theplagroup`)
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

## Deployment (Cloudflare Pages)

The Pages project `theplagroup` is a **Direct Upload** project. Deploys are
pushed from the maintainer's machine with Wrangler:

```bash
CLOUDFLARE_ACCOUNT_ID=<acct> \
CLOUDFLARE_API_TOKEN=<token> \
npx wrangler pages deploy dist --project-name=theplagroup --branch=main
```

To flip to git-integrated deploys (build on push), reconnect the Pages
project to the GitHub repo in the Cloudflare dashboard — the CF GitHub App
must first be authorized on the `teamplagroup` org.

### Custom domain / DNS

Attached in the Cloudflare Pages dashboard (`theplagroup` project → Custom
domains) — CF auto-creates the DNS records on the `usetheplagroup.com` zone.
No manual CNAME needed.

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

**General Sans** (Fontshare, Indian Type Foundry — free commercial license)
is the primary face, loaded via the Fontshare CDN in
`src/layouts/BaseLayout.astro`. Fallback: Inter / system-ui.

Mono UI uses **JetBrains Mono**, self-hosted via `@fontsource/jetbrains-mono`.

---

## Contact form

`src/pages/contact.astro` posts to a Formspree placeholder endpoint
(`https://formspree.io/f/REPLACE_ME`). Swap the `action=` attribute for a
real endpoint before launch. A `mailto:` fallback is shown next to the
form in either case.

---

## TODOs

- [ ] Replace placeholder Unsplash imagery in `src/components/Hero.astro`,
      `src/pages/index.astro`, and `src/pages/about.astro` with licensed,
      self-hosted photography under `public/images/`.
- [ ] Replace the Formspree placeholder endpoint in
      `src/pages/contact.astro`.
- [ ] Add a real favicon set (`.ico`, apple-touch-icon, OG image).
- [ ] Optional: add an `/insights` route once there is content.
