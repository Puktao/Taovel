# TAOVEL — Hospitality Advisory

Static, single-page website for TAOVEL Hospitality Advisory (Greece).

## Structure

```
index.html        # complete site (HTML + inline CSS/JS, no build step)
privacy.html      # GDPR privacy policy (linked from footer and forms)
assets/           # images (.webp) and Cloudbeds logo (.svg)
.github/workflows/pages.yml  # automatic GitHub Pages deployment
```

## Link preview & icons

- `assets/og-image.jpg` (1200×630) is the image shown when the site is shared (WhatsApp, LinkedIn, email…).
  The `og:image`, `og:url` and `canonical` tags in `index.html` / `privacy.html` use absolute URLs —
  **update them when the site moves to its own domain.**
- `favicon.ico`, `assets/favicon-32.png`, `assets/apple-touch-icon.png`, `assets/icon-512.png`: browser tab and home-screen icons.

## Local preview

Open `index.html` in a browser, or run a local server:

```bash
python3 -m http.server 8000
# http://localhost:8000
```

## Deployment (GitHub Pages)

Every push to the default branch (`Main`) deploys the site via GitHub Actions.
The `github-pages` environment must allow deployments from `Main` (Settings → Environments → github-pages).
One-time setup: **Settings → Pages → Build and deployment → Source: GitHub Actions**.

## Contact form

The contact dialog posts enquiries to [FormSubmit](https://formsubmit.co) (`/ajax/<email>`),
which forwards them by email. No account or API key is needed.

- **First use:** the first submission triggers an activation email from FormSubmit to the
  target inbox. Click the activation link; until then enquiries are not delivered.
- After activation, FormSubmit provides a random alias string. Replace the email in
  `CONTACT_EMAIL` inside `index.html` with that alias to keep the address out of the request URL.
- If the request fails, the visitor is offered a pre-filled `mailto:` link as a fallback.
- A hidden honeypot field (`_honey`) filters basic spam bots.

## Cloudbeds demo form — location data

- **Country** dropdown: ISO 3166 list (from `i18n-iso-countries`, MIT), embedded in `index.html`.
- **City** dropdown: the country's provinces ("il" level), filtered by the selected country and
  loaded from `assets/geo/<ISO2>.json` (one sorted array per country).
  - Default: the lowest official level of **ISO 3166-2** subdivisions (from the `iso-3166`
    package, MIT) — e.g. Turkey's 81 provinces, Italy's 107 provinces, Spain's 52, France's departments.
  - Countries whose ISO names are transliterations (JP, CN, RU, AE, EG …) use English names
    from `country-region-data` (MIT).
  - Greece: the 74 regional units + Mount Athos (ISO only lists the 13 large regions).
  - Countries/territories with no subdivisions list the country itself.
- **State/Province**: optional free-text field.
