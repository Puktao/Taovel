# TAOVEL — Hospitality Advisory

Static, single-page website for TAOVEL Hospitality Advisory (Greece · Europe).

## Structure

```
index.html        # complete site (HTML + inline CSS/JS, no build step)
assets/           # hero, Cloudbeds and Athens concept-study images (.webp)
.github/workflows/pages.yml  # automatic GitHub Pages deployment
```

## Local preview

Open `index.html` in a browser, or run a local server:

```bash
python3 -m http.server 8000
# http://localhost:8000
```

## Deployment (GitHub Pages)

Every push to the default branch deploys the site via GitHub Actions.
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
