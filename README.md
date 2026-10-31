# KARKA NOVA 3.0 — Careerverse / Competition Masterpiece

A responsive, Gen-Z-oriented redesign concept for Karka AI & Tech Academy. The experience is built around one distinctive idea: **proof over passive learning**. Instead of a conventional course catalogue, visitors move through a visual career journey, explore skill tracks, try a short Career DNA recommender, understand the Pay After Placement model, and submit an enquiry.

> This is an independent hackathon prototype, not an official Karka product. Before public launch, have Karka verify all copy, program names, fees, placement claims, testimonials, project examples, logos and contact details. The site intentionally avoids invented student stories or unverified placement statistics.

## Visual direction: Hybrid / Competition Edition

The visual language combines premium startup restraint, an AI-futurist atmosphere and expressive Gen-Z details: near-black surfaces, editorial typography, violet/cyan/lime accents, modular layouts, glass-like floating UI, subtle motion and clear conversion paths. Motion respects the user’s reduced-motion preference and the core experience remains usable without JavaScript animation.

### 3.0 experience upgrades

- Subtle scroll-reveal transitions for key content blocks.
- Active section state in the sticky navigation.
- Pointer-responsive hero card on fine-pointer devices only.
- Refined hover, focus-visible, form and card feedback.
- Reduced-motion and touch-device fallbacks.

## What makes this concept different

- **Career DNA mini-experience:** four lightweight questions produce a directional track suggestion; it is explicitly not presented as an aptitude test.
- **Careerverse map:** interactive Discover → Learn → Build → Launch navigation with working shortcuts.
- **Project Universe:** filterable case-study cards with explicit concept labels; ready to replace with approved real student work.
- **Karka community spotlight:** editable cards for Infini AI and Spike AI; verify current details before publication.
- **Student Command Center preview:** responsive dashboard mockup clearly marked as sample data, not a real student account.
- **Pay After Placement Explorer:** a four-step terms checklist that avoids inventing fee amounts, salary thresholds or guarantees.
- **Proof-first storytelling:** the page sells practical outputs and portfolio evidence rather than making unsupported placement promises.
- **Transparent PAP explanation:** the model is explained with an eligibility/terms disclaimer instead of implying that every visitor automatically qualifies.
- **Conversion-led UX:** track filters, preselected enquiry form, mobile navigation, accessible form states and clear contact CTA.
- **Working backend:** FastAPI + SQLite lead capture, input validation, basic rate limiting, health endpoint, track endpoint and protected admin lead listing.

## Product integrity

See [`docs/PRODUCT-NOTES.md`](docs/PRODUCT-NOTES.md) for the product thesis, prototype boundaries and launch verification checklist. Demo project cards and dashboard metrics are illustrative only. Current course availability, PAP terms, placement claims, event details and platform integrations must be approved by Karka before publishing.

## Project structure

```text
karka-nova/
├── frontend/
│   ├── index.html
│   ├── styles.css
│   └── app.js
├── backend/
│   ├── app/main.py
│   ├── requirements.txt
│   ├── Dockerfile
│   └── .env.example
├── docker-compose.yml
└── README.md
```

## Run locally (Windows / macOS / Linux)

### 1. Start the API

```bash
cd backend
python -m venv .venv
# Windows PowerShell:
.venv\Scripts\Activate.ps1
# macOS/Linux:
# source .venv/bin/activate
pip install -r requirements.txt
copy .env.example .env   # Windows; on macOS/Linux use: cp .env.example .env
uvicorn app.main:app --reload --port 8000
```

The API runs at `http://localhost:8000`. Interactive API docs: `http://localhost:8000/docs`.

### 2. Serve the frontend

Open a second terminal from the project root:

```bash
cd frontend
python -m http.server 5500
```

Open `http://localhost:5500`.

The frontend calls `http://localhost:8000` by default. For production, set `window.KARKA_API_URL` before `app.js` loads (or replace the `API_BASE` value at the top of `app.js`) with your deployed API URL.

### 3. Test the API

```bash
curl http://localhost:8000/health
curl http://localhost:8000/api/tracks
```

Submit the enquiry form in the browser. Leads are stored in `backend/karka_leads.db` by default. For production, use a persistent volume or managed database.

## Docker

From the project root:

```bash
# Set a strong ADMIN_API_KEY and your deployed frontend origin first.
docker compose up --build
```

The API is available at `http://localhost:8000`; SQLite persists in the `karka_data` Docker volume.

## Admin lead access

Set a long random `ADMIN_API_KEY` in the deployment environment. Then:

```bash
curl -H "X-Admin-Key: YOUR_SECRET" "http://localhost:8000/api/admin/leads?limit=100"
```

Never put this key in frontend JavaScript or commit it to GitHub. For production, add authenticated staff accounts, audit logging and export controls.

## Deploy / publish checklist

1. **GitHub:** create a repository, commit the project (do not commit `.env`, database files or secrets), and push the source.
2. **Backend:** deploy `backend/` to Render, Railway, Fly.io or another Python host. Set `ADMIN_API_KEY`, `ALLOWED_ORIGINS` and a persistent `DATABASE_PATH`/volume. SQLite is fine for a prototype; use PostgreSQL for a real admissions workflow.
3. **Frontend:** deploy `frontend/` to Netlify, Vercel or Cloudflare Pages. Set `API_BASE` in `frontend/app.js` to the live API origin before deployment.
4. **CORS:** set `ALLOWED_ORIGINS` to the exact production frontend origin(s), comma-separated. Do not use `*` with credentialed requests.
5. **Domain + HTTPS:** connect the approved domain and verify HTTPS, redirects and mobile layout.
6. **Operational readiness:** add privacy policy/consent wording approved by Karka, retention/deletion process, spam protection (Turnstile/reCAPTCHA), monitoring, backups and a real database.
7. **Content sign-off:** verify every factual statement and replace concept visuals with approved brand assets, actual student work and permissioned photos.

## Before production

- Add a privacy policy and data-retention notice; the form currently captures name, email, phone and selected interest.
- Add server-side email/CRM notifications if Karka wants leads routed to a team inbox or CRM.
- Add robust distributed rate limiting and bot protection. Current in-memory rate limiting is a prototype safeguard and resets on restart.
- Configure a production database and backups. SQLite is used here to keep the hackathon prototype easy to run.
- Add analytics only with appropriate consent and a clear privacy notice.
- Ensure the PAP contract language, eligibility and fee details are approved by Karka.
- Replace illustrative project mockup art with genuine, approved student internship work before claiming it as a real student project.

## Brand / content notes

The visual system uses a dark near-black canvas, electric violet, cyan and lime accents, editorial typography, compact mono labels and modular cards. It is designed as a fresh visual direction rather than a pixel-copy of the existing website. Official site: https://www.karka.academy/.
