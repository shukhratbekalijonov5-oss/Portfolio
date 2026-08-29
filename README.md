# Portfolio — Shukhratbek Alijonov

Single-page portfolio. No build step, no dependencies to install: open `index.html`
in a browser and it works.

```
index.html      structure + styles + DATA + render (one file)
assets/         project screenshots
favicon.svg     tab icon
robots.txt      crawler rules
sitemap.xml     single-URL sitemap
```

## Editing content

Everything you will want to change lives in the two `DATA` blocks inside
`index.html` (search for `const DATA` and `Object.assign(DATA`). The render code
below them turns `DATA` into the page — you should not need to touch it.

Every user-facing string is `{ en: "...", ko: "...", uz: "..." }`. `<strong>` and
`<span class="hl">` are allowed inside a string. If a locale key is missing the
renderer falls back to `en`, so the page never shows a raw key.

## Before publishing — required edits

| What | Where | Note |
|---|---|---|
| Domain | `index.html`, `robots.txt`, `sitemap.xml` | replace `REPLACE-WITH-YOUR-DOMAIN` (4 places in `index.html`) |
| Email | `DATA.meta.email` | currently `shukhratbekalijonov4@gmail.com` — confirm this is the address you want public. Single source: the contact card and the hero mail icon both read it |
| LinkedIn | `DATA.meta.linkedin` | `null` → the hero social icon is hidden until set. LinkedIn is deliberately not a contact card |
| Résumé | `DATA.meta.resume` | drop `resume.pdf` beside `index.html`, then set to `"resume.pdf"` — a download button appears in the hero. Résumé is deliberately not a contact card |
| Phone | `DATA.meta.phone` / `phoneHref` | `010 8211 0660` — display value and the `tel:` link are separate fields |
| Photo | `DATA.meta.photo` | set to `"assets/portrait.jpg"` to replace the `SA` monogram |

## Project screenshots

```
assets/hr-copilot/    HR Copilot AI gallery (live production captures)
```

Images are **1400 × 875 (16:10)** — the exact ratio of the gallery frame, so
`object-fit: cover` crops nothing. Source captures were 2940 × 1912 with a 74px
black bar at the top; cropping that bar yields exactly 16:10.

To add one: put the file in `assets/hr-copilot/` and add an entry to that
project's `shots` array:

```js
{ src: "assets/hr-copilot/hr-copilot-ai-job-match.png",
  alt: "HR Copilot AI internal job match with AI explanation",
  caption: { en: "AI Job Match", ko: "AI 채용 매칭", uz: "AI Job Match" } }
```

`alt` is the descriptive text for screen readers; `caption` is the short overlay
shown on hover. The carousel (arrows, dots, captions) appears automatically once
there is more than one image.

Three entries are already written and commented out at the bottom of the HR
Copilot `shots` array, waiting for their files:
`hr-copilot-ai-job-match.png`, `hr-copilot-external-jobs-ko.png`,
`hr-copilot-candidate-home-light.png`. Drop the files in and uncomment.

Motobay still shows a dashed "screenshots not captured yet" slot — same
procedure applies to its `shots` array.

## Locales

Three UI languages: **EN / 한국어 / UZ**. The choice persists in `localStorage`
under `sa-lang` and is restored on reload.

Deliberately **not** translated (§ product and technology names): project titles
(`HR Copilot AI`, `Motobay`, `Burak`), technology tags, domain names, and the
`GitHub` / `LinkedIn` brand labels.

Russian appears only as a spoken-language card in Education & Languages — it is
not a UI locale.

To add a fourth locale: add the key to each string in `DATA` and one more
`<button class="lang-btn" data-lang="xx">` in the nav. Nothing else changes.

## Notes

- Screenshots in `assets/` are real HR Copilot AI UI captures taken from the
  project's verification runs, so they show test-fixture data (`Fixture`,
  `Northwind Labs`). Replace them with production captures if you prefer.
- `prefers-reduced-motion: reduce` disables all animation and smooth scrolling.
- Language choice persists in `localStorage` under `sa-lang`.
