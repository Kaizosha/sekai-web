# Sekai website

The dependency-free static product site for Sekai, Kaizōsha's offline-first
native globe package for SwiftUI.

The root route directly continues the expanded top-right Sekai product cell
from kaizosha.org. It retains the same frame, toolbar, status bar, two-tone
palette, constructed Kaizōsha mark, typography, drafting grid, and restrained
motion. The expanded surface scrolls through product, atlas, installation,
privacy, geographic-data, and open-source details without switching
interfaces.

Sekai's package-specific privacy notice is local to this site. Shared company
pages such as Contact and website Privacy use their canonical kaizosha.org
routes.

## Direct static deployment

This repository is already the public website. There is no generated output,
build script, Worker, Wrangler configuration, package manager, framework, or
dependency installation.

Connect the repository to Cloudflare Pages with these settings:

- production branch: `main`
- framework preset: `None`
- root directory: leave blank
- build command: leave blank
- build output directory: `.`

Cloudflare serves the committed files from the repository root. Every push to
`main` publishes automatically through the Git integration. Attach
`sekai.kaizosha.org` as the Pages project's custom domain after its first
deployment.

## Local preview

No build is needed. To preview the root-relative routes and assets locally,
run:

~~~sh
python3 -m http.server 8000
~~~

Then open `http://localhost:8000/`. The local Python server uses
`/privacy.html`; Cloudflare Pages natively serves that file at the public
canonical route `/privacy`. `_redirects` only normalizes `/privacy/`.

## Public routes

- `/` — permanently expanded Sekai product surface
- `/privacy` — Sekai's canonical package privacy notice
- `/404.html` — unknown-route recovery
- `/site.webmanifest`, `/robots.txt`, and `/sitemap.xml` — product and search
  metadata

## Product source

Sekai itself is open source under the MIT License:

- source: https://github.com/Kaizosha/Sekai
- release: https://github.com/Kaizosha/Sekai/releases/tag/1.1.0
- license: https://github.com/Kaizosha/Sekai/blob/main/LICENSE

## Shared design

Kaizōsha's main website is the source of truth for `BRAND.md`,
`DESIGN_SYSTEM.md`, the brand icon, and the shared CSS and JavaScript
foundations. This site commits synchronized copies so its repository and
Cloudflare Pages deployment remain independent.

Product-specific continuation behavior stays in
`assets/styles/product-continuation.css` and
`assets/scripts/product-continuation.js`. Visible branding always uses the
constructed HTML/CSS mark. The shared Kaizōsha raster icon is reserved for the
favicon, Apple touch icon, manifest, and machine-readable metadata.

## Social preview

Root metadata uses the purpose-built 1200 × 630 card at
`assets/media/social/sekai-social-card.png`. Like the shared raster icon, it is
used only where a metadata consumer requires an image; the visible website
remains constructed HTML and CSS.
