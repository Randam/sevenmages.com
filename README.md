# Seven Mages Studio

Official website for **https://sevenmages.com**, published with GitHub Pages. DNS is managed in Cloudflare. The design develops the selected dark “Worlds / After Dark” concept.

## Editing through prompts

Ask Codex to add a studio update, include the facts and an image, and ask it to publish. News is stored as one JSON file per article under `content/news/`. A push to `main` builds, checks and publishes the site automatically. There is no admin panel or CMS.

Example prompt:

> Add a news post about [topic] to the Seven Mages website. Use [facts] and [image], date it [date], and publish it.

Each article has `title`, `date` (YYYY-MM-DD), `slug`, `url` (`/news/<slug>/`), `body` (trusted HTML), `image` (filename in `public/assets/`), `draft` and optionally `description` and `legacyPath`. Do not change a published slug. Set `draft: true` to omit an unpublished article from the website, sitemap and RSS.

After adding an article, generate its share image with `npm ci && node scripts/social.mjs`, then `npm test`, commit and push. Check the deployment in GitHub Actions. Cards are 1200 × 630 JPEGs with deterministic SVG source layouts in `art/social/`.

## Local development

Requires Node.js 22+ and Python 3 for preview. The site build itself has no third-party dependencies.

```
npm run build
npm run check
npm run preview
```

Open http://localhost:4173. `npm ci` is needed only for the optional image-generation script, which uses Sharp. `dist/` is generated and ignored.

## Structure

- `src/templates.mjs`: home sections and navigation
- `src/data.mjs`: game descriptions and seven studio roles
- `src/style.css`, `src/production.css`: selected visual design and article/game layouts
- `scripts/build.mjs`: static HTML pages, metadata, sitemap, RSS and preserved old URLs
- `scripts/check.mjs`: HTML, internal-link, structured-data and content checks
- `content/news/`: news posts
- `content/app-privacy.html`: unchanged original Penguin Panic policy
- `public/assets/`: self-hosted fonts, original logo, game imagery and share cards

## SEO and sharing

Every page is pre-rendered HTML with a unique title, description, canonical URL, Open Graph and Twitter card metadata. The website includes Organization, Website, VideoGame, NewsArticle and Breadcrumb structured data, an XML sitemap, robots.txt and RSS. Existing WordPress news URLs serve the corresponding article with the new canonical URL, preserving inbound links. The former `/game-penguin-panic/` address links to the permanent game page.

All share cards are real, public 1200 × 630 JPEGs. Fonts are hosted locally. No analytics or advertising scripts are included. A real 404 page is provided.

## Hosting

GitHub repository: https://github.com/Randam/sevenmages.com

The workflow `.github/workflows/pages.yml` builds and publishes `dist` to GitHub Pages on a push to `main`. Canonical origin: `https://sevenmages.com`. GitHub Pages should redirect `www.sevenmages.com` to the canonical apex domain.

Cloudflare changes should affect only website records at the apex and `www`. Preserve MX/TXT email records and the Epic Online Services verification TXT record. A pre-migration DNS snapshot is kept locally outside the repository. Original mail/FTP aliases must remain pointed at their previous origin so the apex move does not retarget them.

## Artwork provenance

Brand mark: user-supplied white `sevenmages.png`, preserved in `public/assets/sevenmages-white.png`.

Game artwork and content: existing Seven Mages / Avalon materials. The wide homepage artwork was adapted with the built-in ImageGen tool in the concept phase: remove only the Avalon and Legacy Edition lettering, continue the surrounding forest/mountains/sky, preserve the existing characters, castle, village, colours and composition. The web delivery asset is `public/assets/avalon-world-no-title.webp`; original PNG retained. This is marketing art, not a gameplay screenshot. Social cards use SVG typography with existing artwork and the supplied logo; no additional generated game scenes.

## Responsive image delivery

Run `npm run images` after adding or replacing a source image, then `npm test`. The preprocessing script generates high-quality AVIF and WebP width variants under `public/assets/responsive/` and records them in `content/responsive-images.json`. Add a new source filename to `scripts/images.mjs` when introducing a new content image.

The homepage has a dedicated portrait crop for narrow screens. The crop follows the existing background position; it avoids sending the unused landscape area to phones. Desktop keeps the full landscape composition. Hero/detail/article images load eagerly; below-the-fold imagery loads lazily. All variants retain intrinsic dimensions and async decoding. Original assets and social JPEG cards remain available. The original small pixel-art screenshots stay unchanged when conversion would increase their size.

Search Console: the domain property `sc-domain:sevenmages.com` was verified on 8 November 2026, and `https://sevenmages.com/sitemap.xml` was submitted successfully. The verification TXT record is held in Cloudflare; keep it in place. Search Console periodically rereads the same sitemap URL as pages are added. Successful submission does not guarantee immediate indexing.
