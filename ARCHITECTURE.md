# Sekai Site Architecture

Sekai uses the same dependency-free static visual contract as kaizosha.org,
with every public file served directly from the repository root.

## Public routes

| Route | Source file | Role | Page family |
| --- | --- | --- | --- |
| `/` | `index.html` | Expanded Sekai product continuation | `directory` |
| `/privacy` | `privacy.html` | Canonical Sekai package privacy notice | `document` |
| `/404.html` | `404.html` | Unknown-route recovery | `error` |

Cloudflare Pages reads `_headers` for response policy and `_redirects` for
trailing-slash canonicalization. Its native static handling serves
`privacy.html` at `/privacy` and `404.html` for unknown paths.

## Root experience

The Kaizōsha homepage expands Sekai in the top-right physical product cell
before the scroll handoff. The destination renders that settled state
immediately:

- the shared frame, top and bottom bars, drafting grid, tokens, and compact
  constructed Kaizōsha mark;
- the same active-cell grid geometry without a separate entry interface;
- Sekai's atlas, composition, Swift Package Manager installation, privacy,
  geographic-data limits, release, and MIT source links;
- one accessible scroll region that continues through the complete product
  content.

The main site may pass the active product slot as `?slot=top-left`,
`?slot=top-right`, `?slot=bottom-left`, or `?slot=bottom-right`. The small
plain-JavaScript controller swaps the static grid slots and removes that
temporary query parameter. Direct visits use Sekai's canonical top-right slot.

## Shared layers

- `assets/styles/brand.css` and `assets/styles/markdown.css` are synchronized
  from the Kaizōsha shared-design source.
- `assets/styles/product-continuation.css` adds only the generic long
  active-cell continuation, data-list, terminal, and notice primitives.
- `assets/scripts/site-motion.js` and `document-navigation.js` are shared
  progressive enhancements.
- `assets/scripts/product-continuation.js` handles the static product-slot
  handoff and URL cleanup.

The visible Kaizōsha mark is semantic HTML styled with `brand.css`. `icon.png`
is used only where a browser, operating system, PWA, or metadata consumer
requires a raster image.

## Zero-build hosting

There is no compilation or transformation boundary. HTML, CSS, JavaScript,
headers, redirects, metadata, and the icon are committed in their final public
form. Cloudflare Pages Git integration publishes the repository root with no
framework preset and a blank build command.

The project has no Worker, Wrangler file, package manifest, lockfile, generated
directory, runtime API, database, account, analytics service, or third-party
frontend dependency. A change becomes deployable as soon as the edited static
files are committed and pushed.

## Product boundary

The website documents the public Sekai 1.1.0 package. It does not render the
native SwiftUI/Metal globe in the browser, request location, import GeoJSON, or
simulate a host application's storage and network behavior. The geographic
data disclaimer remains visible in both the product continuation and privacy
notice.
