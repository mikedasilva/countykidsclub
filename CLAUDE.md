# County Kids Club website

Static site for countykidsclub.com, hosted on GitHub Pages (no build step; `.nojekyll` keeps
Jekyll off so `.md` files are served raw). Plain HTML pages share `shared.css`. Changes go
straight to `main`.

## Program session details live in four places — keep them in sync

Whenever a session is added, archived, or its dates, times, ages, capacity, gym, price, status,
or register link change, update **all** of these in the same change:

1. **The program page card** — `programs/<program>.html`, "Current & Upcoming Programs" section.
2. **JSON-LD** — the `<script type="application/ld+json">` block in that page's `<head>`.
   Current sessions get an `Event` node (start/end with timezone offset: `-04:00` before Nov 1,
   `-05:00` after, for 2026). Remove `Event` nodes for sessions that are archived or over.
3. **`programs.md`** — the agent-facing summary at the site root. Update the program's entry,
   move it between "open for registration" and "not currently running" as needed, and bump
   **Last updated** (and "Current season being promoted" if the season changes).
4. **The landing page** (`index.html`) — the program's category card status (Active /
   Coming Soon / No Upcoming Events), the hero banner and register CTA wording, and the
   stats strip (seasons, program types) when relevant.

Also update `llms.txt` when a program page is added or removed.

## Archiving a past session

- Move the old session card into the page's **Past Programs** section inside a
  `<details>` / `<summary>` "(view details)" block, newest first.
- Remove the **Cost** row from archived cards and replace the status with
  "Registration for this session is closed." Remove register/waitlist buttons.
- Keep the other original details (ages, capacity, dates, gym) unchanged.

## Pricing rules

- Prices appear only in session detail cards (and `programs.md` / JSON-LD for current
  sessions). **FAQ answers never quote a specific price**; they point to the program details.

## Conventions

- Register links go to `https://countykidsclub.youthmodo.com/register`, with
  `?programId=<id>` when a YouthModo program ID is known.
- Mailing list: `https://countykidsclub.youthmodo.com/mailing-list?list=06232d50-2b18-40d9-9c75-bbaf16a455c7`
- Times are written like `Sundays 11:15 AM–12:15 PM (60 min)`; dates like `November 22, 2026`.
