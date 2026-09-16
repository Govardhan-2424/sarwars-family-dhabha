# Sarwar's Family Dhaba — Website

The public website for **Sarwar's Family Dhaba**, a family restaurant at JPCF+JC, Kohir,
Telangana 502321. It is a single-page site covering the welcome/about section, menu,
photo gallery, location with an interactive map, and contact details.

## Technologies

- Plain HTML and CSS — no framework, no build step, so the page loads fast on mobile data.
- **Netlify Image CDN** (`/.netlify/images`) serves every photo resized and converted to WebP
  on the fly, so full-resolution originals never reach a visitor's phone.
- Custom food and restaurant photography generated with a Gemini image model via
  **Netlify AI Gateway**, stored in `public/img/`.
- `robots.txt`, `sitemap.xml`, canonical/Open Graph tags and Schema.org `Restaurant`
  structured data for Google Search and Google Business Profile.

## Running locally

```bash
netlify dev --port 8889
```

Then open http://localhost:8889. Running through the Netlify CLI matters here because it
emulates the Image CDN — opening `public/index.html` directly leaves the photos blank.

## What the owner can still fill in

The page intentionally shows "to be confirmed" rather than guessed details. When the owner
supplies them, update `public/index.html`:

1. Phone and WhatsApp numbers (Contact section) — turn them into `tel:` / `wa.me` links.
2. Opening hours (About highlights and Contact section), and add `openingHoursSpecification`
   plus `telephone` to the JSON-LD block in `<head>`.
3. Real menu dishes and prices, replacing "Price to be updated".
4. The dhaba's own photographs, replacing the files in `public/img/` (keep the same
   filenames and no markup changes are needed).
5. If a custom domain is added, replace `creative-meringue-f8b387.netlify.app` in
   `public/index.html`, `public/robots.txt` and `public/sitemap.xml`, then submit the
   sitemap in Google Search Console.
