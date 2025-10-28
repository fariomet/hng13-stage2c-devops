## Name: Faridat Suleiman
## Jazzmin.jsx
## Description: TicketApp — Twig (CDN, single-file)

This is the Twig (twig.js) implementation delivered as a single HTML file using the twig.js CDN. No build step is required — open `index.html` directly or serve it via a static server.

## Domaain: https://hng13-stage2c-devops-6a8y.vercel.app/

## Quick Start
- Double-click `twig/index.html` to open in your browser.

## What’s Included
- Landing page with wavy hero, decorative circles, features section
- Auth (Login/Signup) with validation and toasts
- Protected routes (Dashboard, Tickets) using localStorage session key `ticketapp_session`
- Dashboard stats (total, open, resolved)
- Full Ticket CRUD stored in `ticketapp_tickets`
- Responsive, accessible UI consistent with React and Vue versions

## File Structure
```
twig/
  index.html  # All CSS + JS inline; twig.js loaded from CDN
```

## Routes (hash-based)
- `/` Landing
- `/auth/login` Login
- `/auth/signup` Signup
- `/dashboard` Dashboard (protected)
- `/tickets` Ticket Management (protected)

Unauthorized access triggers redirect to `/auth/login` and a toast: “Your session has expired — please log in again.”

## Authentication
- Storage key: `ticketapp_session`, JSON with `{ token, user }`
- Login/Signup accept any valid email and password ≥ 6 characters
- Logout clears the session and returns to the Landing page

## Tickets Data
- Storage key: `ticketapp_tickets`
- Ticket shape: `{ id, title, status, description }`
- Status must be one of `open | in_progress | closed`

## Validation Rules
- Required: `title`, `status`
- Allowed `status`: `open`, `in_progress`, `closed`
- `description` length ≤ 1000
- Inline field errors + toast feedback

## Error Handling
- Invalid inputs → inline error + toast
- Unauthorized access → redirect + toast

## Design & Accessibility
- Max width 1440px centered
- Wavy SVG hero with overlapping circles
- Cards for stats and tickets with rounded corners and shadows
- Status colors: open=green, in_progress=amber, closed=gray
- Semantic markup, focus outlines, high contrast, ARIA for toasts and errors

## How It Works (Twig specifics)
- Templates (layout, hero, features, auth, dashboard, tickets) are defined as strings and rendered via `Twig.twig({ data: tpl }).render(context)`
- The router is a simple `hashchange` listener that re-renders the appropriate template(s) into `#app`
- Form handlers (login/signup, ticket create/update/delete) are plain JS functions attached to `window.*` and referenced by the templates
- This mirrors the React/Vue features without a component runtime

## Test Credentials
- Any new email/password that passes validation
- Example: user@example.com / Passw0rd!

## Known Notes
- Data persists in localStorage; clear to reset
- Global CDN approach is ideal for demos; use a build tool if you need code splitting or testing

## Troubleshooting
- Prefer a local server over file:// if routing appears inconsistent
- Clear `ticketapp_session` and `ticketapp_tickets` if state appears stale
- Use a modern browser (Chromium, Firefox, Safari)
