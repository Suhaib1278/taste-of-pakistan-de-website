# 🍛 Taste of Pakistan — Frankfurt am Main

The official website for **Taste of Pakistan**, an authentic Pakistani restaurant located in the heart of Frankfurt am Main, Germany.

**Live Site:** [tasteofpakistan.de](https://tasteofpakistan.de)

---

## Features

- **Bilingual (DE / EN)** — Full German and English versions with a language switcher in the navigation bar.
- **Hero Slideshow** — CSS-only fade-zoom animation cycling through five restaurant photos.
- **Digital Menu** — Links to a downloadable PDF menu (`assets/docs/menu.pdf`).
- **Photo Gallery** — Masonry-style grid showcasing food and restaurant ambiance with hover-zoom effects.
- **Google Maps Embed** — Interactive map with cookie-consent gating via Cookiebot.
- **Uber Eats Integration** — Sticky delivery banner and floating order button linking directly to the Uber Eats store.
- **Legal Compliance** — Impressum and Datenschutzerklärung (privacy policy) pages compliant with German law (TMG / DSGVO).
- **Cookie Consent** — Cookiebot integration for GDPR-compliant consent management.
- **Responsive Design** — Mobile-first layout that adapts seamlessly across all screen sizes.

## Tech Stack

| Layer     | Technology                          |
|-----------|-------------------------------------|
| Structure | HTML5 (semantic)                    |
| Styling   | TailwindCSS (CDN) + custom CSS     |
| Fonts     | Inter · Playfair Display · Montserrat (locally hosted) |
| Consent   | [Cookiebot](https://www.cookiebot.com/) |
| Maps      | Google Maps Embed API               |
| Hosting   | [Netlify](https://www.netlify.com/) |

> **Note:** This is a static site with zero build steps — no bundler, no JavaScript framework, no server.

## Project Structure

```
taste_of_pk_de_website/
├── index.html              # Homepage (German)
├── gallery.html            # Photo gallery (German)
├── legal.html              # Impressum & Datenschutz (German)
├── en/
│   ├── index.html          # Homepage (English)
│   ├── gallery.html        # Photo gallery (English)
│   └── legal.html          # Legal notice & Privacy (English)
├── assets/
│   ├── images/
│   │   ├── logos/          # Favicon, logo, Uber Eats badge
│   │   └── restaurant/    # Slideshow, food, and seating photos
│   └── docs/
│       └── menu.pdf        # Downloadable menu
├── .gitignore
└── readme.md
```

## Local Development

No build tools required. Open any HTML file directly in a browser, or use a simple local server:

```bash
# Python
python3 -m http.server 8000

# Node.js (npx)
npx -y serve .
```

Then visit `http://localhost:8000`.

## Deployment

The site is deployed via **Netlify** from the `main` branch. Every push to `main` triggers an automatic deployment. No build command is needed — Netlify serves the static files directly.
