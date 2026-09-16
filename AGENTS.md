# Agent notes

## Architecture

A static, dependency-free site. There is no package.json, no bundler and no server code —
Netlify publishes `public/` verbatim (see `netlify.toml`). Do not introduce a build step or
a framework unless the site genuinely outgrows one page.

```
public/
  index.html     entire site: inline <style>, all sections, JSON-LD in <head>
  img/           generated PNG originals (large on purpose, never linked directly)
  robots.txt
  sitemap.xml
netlify.toml     publish dir + long-lived cache headers for /img/*
```

## Conventions

- All CSS lives in the single inline `<style>` block in `index.html`, written in the existing
  compact multi-selector-per-line style with CSS custom properties (`--green`, `--gold`,
  `--cream`) for the palette. Match that density rather than reformatting it.
- Three responsive breakpoints already exist (900px, 600px); extend them instead of adding new ones.
- **Never reference `/img/*.png` directly in markup.** Always go through the Image CDN, e.g.
  `/.netlify/images?url=/img/biryani-chicken.png&w=700&h=520&fit=cover&fm=webp&q=78`.
  In HTML attributes the `&` must be written `&amp;`; inside the `<style>` block it stays raw.
- Below-the-fold images carry `loading="lazy" decoding="async"`; the hero and the first gallery
  image deliberately do not.

## Non-obvious decisions

- The site was converted from an owner-supplied `sarwars_family_dhaba_google_ready.zip`. The
  original hotlinked Unsplash photos and used a placeholder `sarwarsfamilydhaba.example`
  domain; both were replaced with locally generated imagery and the live Netlify domain.
- Unverified business details (phone, hours, prices) are shown as "to be confirmed" rather
  than invented, because they also feed the Schema.org block and the Google Business Profile.
  Do not fabricate them — see the checklist at the end of README.md.
- The Google Maps panel is a keyless `maps.google.com/?output=embed` iframe, replacing a
  decorative fake-map box from the original zip.
- Image originals are committed rather than regenerated at build time, so deploys stay
  deterministic and fast.
