[README.md](https://github.com/user-attachments/files/30560046/README.md)
# Callandor — Website

The public website for **Callandor** — _Enabling Trusted Technology_.

A single-page, cinematic marketing site built with Next.js (App Router),
TypeScript, Tailwind CSS and Framer Motion. Dark, restrained, engineering-led.

---

## Quick start

You'll need **Node.js 18.17+** (Node 20 LTS recommended) and npm.

```bash
npm install
npm run dev
```

Open <http://localhost:3000>.

> **Note on fonts:** the build fetches the Inter and Cormorant Garamond fonts
> from Google Fonts at build time (via `next/font`). This needs internet access
> the first time you build. Fonts are then cached locally.

### Production build

```bash
npm run build
npm run start
```

---

## Editing content

**Almost everything you'd want to change lives in one file:**

```
content/site.ts
```

Headlines, capabilities, use cases, founder bios, testimonial wording,
contact details and SEO metadata are all there, clearly labelled and typed.
Change the text, save, and the site updates. TypeScript will flag typos in the
structure before they reach the browser.

Items marked `// TODO:` in that file **must** be confirmed before launch
(email, LinkedIn URL, Companies House number, production domain). See
`LAUNCH_CHECKLIST.md`.

---

## Founder photos (placeholder system)

Until real photography is supplied, each founder shows an elegant monogram.

To add a photo, drop a **square** image (ideally 800×800, `.jpg` or `.webp`)
into `public/founders/` using the filename referenced in `content/site.ts`:

```
public/founders/matt-johnston.jpg
public/founders/josh-hilton.jpg
```

No code changes are required — the photo appears automatically, and the
monogram remains a safe fallback if a file is missing.

---

## Adding a case study / use case

Use cases are data-driven. To add one, append an object to `useCases.items`
in `content/site.ts`:

```ts
{
  icon: "rapid",            // one of the keys in UseCases.tsx iconMap
  title: "Your title",
  description: "One or two calm, factual sentences.",
}
```

Available icons: `rapid`, `cross-domain`, `multi-supplier`, `exercise`,
`responsible-ai`. To add a new icon, add an SVG to `components/icons/index.tsx`
and register it in the relevant section's `iconMap`.

---

## Contact form

By default the form uses a **mailto fallback** — no backend required. When a
visitor submits, their mail client opens with the message pre-filled to the
address in `content/site.ts`.

To capture submissions server-side instead (e.g. Formspree, Basin, a custom
endpoint), set `contact.formEndpoint` in `content/site.ts` to your handler URL.
The form will `POST` JSON (`{ name, email, organisation, message }`) to it.

---

## Project structure

```
callandor/
├── app/
│   ├── layout.tsx          # Root layout, fonts, SEO metadata, nav + footer
│   ├── page.tsx            # Homepage — assembles all sections in order
│   ├── globals.css         # Design tokens, base styles, component utilities
│   ├── robots.ts           # robots.txt
│   ├── sitemap.ts          # sitemap.xml
│   ├── privacy/            # Placeholder legal page
│   └── terms/              # Placeholder legal page
├── components/
│   ├── layout/             # Navbar, Footer
│   ├── sections/           # Hero, Evidence, Capabilities, Why, HowWeWork,
│   │                       #   UseCases, Clients, Founders, Contact
│   ├── ui/                 # Logo, Button, Section, Container, Reveal, FounderPhoto
│   └── icons/              # Monochrome line-icon set
├── content/
│   └── site.ts             # ← ALL editable copy lives here
├── lib/
│   └── utils.ts            # cn() className helper
├── public/
│   ├── logo.svg            # Standalone brand mark
│   ├── favicon.svg         # Favicon
│   ├── og-image.svg        # Social share image
│   └── founders/           # Founder photos (drop-in)
├── tailwind.config.ts      # Brand palette, type, tokens
├── LAUNCH_CHECKLIST.md     # Content requiring final approval before go-live
└── README.md
```

---

## Design system

| Token          | Value                          | Use                          |
| -------------- | ------------------------------ | ---------------------------- |
| Navy (base)    | `#070E16` – `#16273A`          | Backgrounds                  |
| Graphite       | `#1A2430` – `#2C3A4A`          | Card surfaces                |
| Silver         | `#E6ECF2` / `#C7D0DA` / `#8A97A6` | Text, headings, mark      |
| Teal (accent)  | `#4FB6B2`                      | Restrained highlights only   |
| Display type   | Cormorant Garamond (light)     | Headings                     |
| Wordmark type  | Cinzel (Trajan-style caps)     | CALLANDOR lettering          |
| Body type      | Inter                          | Body, UI                     |

**Logo.** The mark is a scalable SVG (`components/ui/Logo.tsx`) that matches the
supplied artwork, and the CALLANDOR wordmark is set in **Cinzel** with a
metallic-silver gradient fill (`.metal-text`) to echo the brushed-metal
lettering. This keeps the logo crisp at any size and lets it sit on the dark
theme without a background plate. The original supplied render is kept for
reference at `public/logo-source.png` (note: it has a studio-grey background, so
it isn't used directly on the dark site).

Accessibility: semantic landmarks, a skip link, visible focus states, honours
`prefers-reduced-motion`, and dark-scheme colour contrast tuned for legibility.

---

## Deployment

The site is a standard Next.js app and deploys anywhere Next runs.

### Vercel (recommended, zero-config)

1. Push this repository to GitHub/GitLab.
2. Import it at <https://vercel.com/new>.
3. Framework preset auto-detects **Next.js** — no settings needed.
4. Deploy. Add your custom domain in **Project → Settings → Domains**.

### Other hosts

- **Netlify** — use the official Next.js runtime; build `npm run build`.
- **Node server** — `npm run build && npm run start` behind a reverse proxy.
- **Static export** is _not_ used here because `robots.ts`/`sitemap.ts` and the
  contact interactivity benefit from the standard server runtime. (The site has
  no database and is inexpensive to host.)

Before go-live, set the real domain in `content/site.ts` (`company.url`) so the
canonical URL, sitemap and Open Graph tags are correct.

---

## Licence / ownership

© 2026 Callandor. All rights reserved. This code is proprietary to Callandor.
The brand mark, wordmark and all copy are the property of Callandor.
