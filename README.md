# Bronze Base — Product Hub (`hub`)

Static site for **https://hub.bronzebasehq.workers.dev/** — the product hub.
Homepage = hub (intro + product list: CleanTake free + SIVO coming soon + blog index).
Blog lives here from now on (new posts under `blog/`).

## Architecture (decided 2026-10-13 — do NOT "simplify" this away)

| Domain | Serves | Why separate |
|---|---|---|
| `hub.bronzebasehq.workers.dev` (this repo) | Product hub + new blog | Brand home, not tied to one product |
| `cleantake.bronzebasehq.workers.dev` (repo `product-hub`) | CleanTake product page + docs/changelog | **KEPT as-is, NO redirect.** Pinterest links to this domain root. Old blog posts were DELETED 2026-10-13 per Minh (blog restarts fresh on the hub). |

The hub links OUT to the CleanTake subdomain. The CleanTake site links back to the hub
only where it makes sense. Old blog posts were deleted 2026-10-13 per Minh — no Archive section on the hub.
X handle everywhere is @bronzebase (chốt 2026-10-13, replaces @bronzebase).

## Deploy (Minh — Cloudflare login required, ~10 min)

This repo must be connected as its own Cloudflare Pages project. Rio cannot do
the Cloudflare steps (needs Minh's login).

1. Cloudflare dashboard → **Workers & Pages** → **Create** → tab **Pages** →
   **Connect to Git** → select repo `bronzebasehq-lang/hub` → **Begin setup**.
2. Build settings:
   - **Project name:** `hub` (gives `hub.bronzebasehq.workers.dev`)
   - **Production branch:** `main`
   - **Framework preset:** None
   - **Build command:** (empty)
   - **Build output directory:** `/`
3. **Save and Deploy.** ~30 s later the hub is live.
4. (Optional) Cloudflare dashboard → **Web Analytics** → enable for this project,
   then paste the new beacon token into `index.html` (do NOT reuse the cleantake
   site's token — it would attribute hub traffic to the cleantake site).
5. Google Search Console: add property `https://hub.bronzebasehq.workers.dev`,
   submit `sitemap.xml`.

## Adding a blog post

New file under `blog/<slug>/index.html` (copy the structure of `blog/index.html`),
then add it to the "New posts" section of `blog/index.html` and the Blog section
of the homepage.
