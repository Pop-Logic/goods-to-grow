# Grow Supplies Affiliate

Content site for indoor/controlled-environment growing equipment guides,
monetized via the Amazon Associates program. Built with Astro (static
output), Tailwind, and MDX content collections, meant to deploy on
Cloudflare Pages.

## Project structure

```text
src/
├── components/
│   ├── AffiliateDisclosure.astro   per-post disclosure blurb
│   └── ProductCard.astro           product callout with Amazon CTA
├── content/
│   └── posts/                      MDX guides (frontmatter: title, description,
│                                    pubDate, tags, draft)
├── content.config.ts               content collection schema
├── layouts/
│   └── Layout.astro                shared shell: nav, SEO meta, footer
└── pages/
    ├── index.astro                 post listing (newest first, drafts hidden)
    ├── posts/[...id].astro         individual post route
    ├── about.astro
    └── disclosure.astro
```

## Commands

| Command           | Action                                       |
| ------------------ | --------------------------------------------- |
| `npm run dev`       | Local dev server at `localhost:4321`          |
| `npm run build`     | Build static site to `./dist/`                |
| `npm run preview`   | Preview the production build locally          |

## Writing a post

Add an `.mdx` file to `src/content/posts/`. Set `draft: true` while writing —
draft posts are excluded from the homepage and from the build's static
routes. Flip to `draft: false` when it's ready to publish.

Use the `<ProductCard />` component for Amazon callouts — it sets
`rel="sponsored noopener"` on the link automatically, which Amazon and
Google both expect on affiliate links.

## Before going live — checklist

- [x] Replace `site` in `astro.config.mjs` with your real domain (done — goodstogrow.com)
- [ ] Write real copy for `src/pages/about.astro` and `src/pages/disclosure.astro`
- [ ] Add ~20-30 real posts before applying to Amazon Associates — they reject
      bare/placeholder sites, and once approved you have 180 days to log a
      qualifying sale or the account is closed
- [ ] Get your Amazon affiliate tracking tag and use it in every product link
      (`?tag=yourtag-20`) — never hardcode a tag you don't own
- [ ] Add a real `public/favicon.svg` / OG image (currently Astro defaults)
- [ ] Position content around "indoor/controlled-environment growing" rather
      than explicitly cannabis-branded — same audience via SEO, much lower
      risk of an Amazon Associates ToS strike (the products are legal
      generic horticulture equipment; explicit cannabis framing is the
      compliance risk, not the products themselves)

## Deploying to Cloudflare Pages

**Option A — Git integration (recommended):**
1. Push this repo to GitHub/GitLab.
2. In the Cloudflare dashboard: Workers & Pages → Create → Pages → Connect to Git.
3. Build command: `npm run build`. Build output directory: `dist`.
4. Every push to `main` auto-deploys; every PR gets a preview URL.

**Option B — CLI (Wrangler):**

```sh
npm install -g wrangler
npm run build
wrangler pages deploy dist --project-name=grow-supplies-affiliate
```

No Cloudflare adapter is needed — this site builds to fully static HTML,
which Pages serves directly.
