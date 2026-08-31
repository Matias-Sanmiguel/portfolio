# Sashimi in portfolio + editorial refresh + LinkedIn post

Date: 2026-08-31
Status: implemented 2026-08-31

## Goal

Add Sashimi as the featured project on the existing single-page portfolio, refresh the visual language without a redesign, and write one LinkedIn post in Spanish with an engineering angle about the public repo.

Success looks like: a recruiter or engineer lands on the site, sees Sashimi first in Projects, understands dual-rail settlement in one screen, and can open GitHub and docs. The page still reads as the same editorial portfolio, not a new product site. The LinkedIn post can be pasted as-is.

## Stack and constraints

- Single file: `index.html` plus `favicon.svg`. No new framework, build step, or CSS library.
- Keep dark mode (`:root.dark`, `localStorage`, existing toggle).
- Copy on the site stays English. The LinkedIn post is Spanish.
- Do not invent production status, fundraising, or UADE voting CTAs.
- No checkout/dashboard screenshots in this pass. If a screenshot appears later, it can replace the architecture window; it is not required to ship.
- No new project case page. No custom cursor. No neon/glow. No Inter.

## Visual tokens

Keep type: Newsreader (display), DM Sans (body), JetBrains Mono (labels, code).

| Role | Light | Dark |
|---|---|---|
| Paper `--bg` | `#F4F3EF` | `#141312` |
| Surface `--surface` | `#FBFBFA` | `#1C1B19` |
| Border `--border` | `#E4E2DC` | `#2A2926` |
| Ink `--text` | `#1A1916` | `#F0EDE8` |
| Muted `--muted` | `#6B6964` | `#8A8780` |
| Accent `--accent` | `#8F3A32` | `#C46A5A` |
| Accent wash `--accent-bg` | `#F6EBE8` | `#2A1A18` |

Contact section uses dark paper `#141312` (same as dark-mode bg), not pure `#000` or the old `#111111`. Heading italic uses the akami accent.

Colored tag pills (`tag-r/b/g/y`) are removed. Tags become: JetBrains Mono, 10px, uppercase, letter-spacing, 1px `var(--border)`, transparent/surface fill, `var(--muted)` text. The accent color is reserved for section labels, Sashimi chrome, and links.

## Featured Sashimi block

Place at the top of `#projects`, spanning 12 columns. It is not a sibling card in the 7/5 bento; it is a full-width spread above the remaining grid.

Layout (desktop):

- Header row: `01` in mono + muted accent, title “Sashimi”, eyebrow “Payment gateway · LATAM · Open source”, links “GitHub” and “Docs” on the right.
- Thesis (Newsreader, ~28–32px, one block):

  > Shoppers pay in pesos. Merchants settle in USDT. Hosted checkout, HD wallets, signed webhooks — Java 21, Spring Boot, one Docker compose.

- Body: two columns, not three cards.
  - Left: dual rail. Cash-in: shopper pays ARS/BRL (CVU, PIX); merchant receives USDT. Crypto: USDT/USDC on TRON or Solana; settle on-chain or off-ramp to local fiat.
  - Right: faux-OS window (the chrome that today sits on Caché). Window body lists the Maven reactor in mono: `sashimi-core`, `sashimi-api`, `sashimi-blockchain`, `sashimi-fx`, `sashimi-webhooks`, `sashimi-fiat`, plus checkout / sdk / widget as comments.
- Links (must be real, new tab, `rel="noopener"`):
  - GitHub: `https://github.com/Matias-Sanmiguel/sashimi-public`
  - Docs: `https://matias-sanmiguel.github.io/Sashimi/`
- Tags (new style): Java 21, Spring Boot 3.3, PostgreSQL, Redis, TRON, Solana, Next.js, Docker.

Mobile (`max-width: 768px`): stack header, thesis, rails, then window. Full width. No horizontal scroll.

## Remaining projects

Caché becomes `02`, loses the window chrome, stays `bento-card--main`. Pressure `03` side. Honeycomb `04` and CauchoChain `05` half-width. Copy of those four projects does not change except numbering.

## Rest of the page

- Hero: keep current thesis. Tighten tracking on `.hero-name`. `text-wrap: balance` on headings. CTA fill is `--text`; hover is `--accent`; `:active` `scale(0.98)`. Add `:focus-visible` rings on all interactive elements (2px accent, 2px offset).
- About: keep the three paragraphs. Add one sentence at the end of paragraph two: Sashimi is the largest system now public (gateway, checkout, SDK), without turning About into a product pitch. Do not rewrite the hero around Sashimi.
- Experience and Education: content unchanged. Slightly more vertical padding on `.exp-item`. Tags in the new uncolored style.
- Skills: remove `.skill-bar-wrap` / `.skill-bar` and the IntersectionObserver code that animates them. Each group is a label plus a plain list of names. Keep the three existing groups and names. Do not add a Blockchain group or TRON/Solana skill rows; those names appear only as Sashimi tags.
- Nav: sticky, blur, paper-tinted translucent background matching the new `--bg`. `prefers-reduced-motion: reduce` disables ambient drift, reveals (show at rest), and the ambient translate animation.
- Ambient gradients retint to akami + a cool wash; keep low opacity (~0.06).

## LinkedIn post

Deliverable: a finished Spanish draft in the implementation, stored in `docs/linkedin-sashimi-publico.md` so it can be copied. Not published by the agent.

Constraints:

- Engineering angle. Not the UADE product pitch, not a “we open-sourced the future” post.
- ~1,200–1,600 characters including spaces and URLs.
- No emojis. No “seamless / game-changer / next-gen”. No like/vote CTA. Do not claim production or fundraising.
- Structure: (1) repo is public, one-line what it is; (2) the technical problem: two rails, one API, settle USDT/USDC; (3) four decisions with a because: HD wallets per order on TRON+Solana; dual rail cash-in vs crypto with on-chain or off-ramp; HMAC webhooks + idempotency; one Docker Compose bringing API, checkout, Postgres, Redis, Grafana; (4) stack in one line: Java 21, Spring Boot 3.3, Maven multi-module, Next.js, `@sashimi/sdk`; (5) links to GitHub and docs.

## Verification

- Open the local `index.html` (or a static server) in the browser.
- Desktop and a ~390px mobile width: featured Sashimi, remaining grid, nav, contact, dark mode toggle.
- Click GitHub and Docs; they must not be `#`.
- Keyboard: tab through nav, theme toggle, project links, contact; focus ring visible.
- `prefers-reduced-motion`: no drifting ambient, reveals visible immediately.

## Out of scope

- Rewriting Experience bullets, education, or contact email/LinkedIn/GitHub URLs (except if a URL is already wrong; LinkedIn is `https://linkedin.com/in/matías-sanmiguel` as today).
- Screenshots, Remotion, or a Sashimi marketing site.
- Translating the portfolio to Spanish.
- Committing or posting the LinkedIn text anywhere except the local markdown file.
