# Seven Mages website

Use the selected dark design. This is the production repository for sevenmages.com, hosted by GitHub Pages; do not migrate it to another hosting platform.

The owner adds news via prompts. Do not add an admin panel or authentication. Store a post in `content/news/`, add its image in `public/assets/`, generate its social card with `npm ci && node scripts/social.mjs`, run `npm run images` when adding new content imagery (register its source filename in `scripts/images.mjs`), then run `npm test`. Drafts must stay out of all public output, RSS and sitemap. Preserve published slugs and original `legacyPath` routes. Write website copy in British English.

Publishing is authorized when requested: commit and push to main, then monitor the GitHub Pages workflow to completion and verify https://sevenmages.com. Keep the public repository free of credentials, DNS account details and unrelated files. Preserve mail and external-service verification DNS records.

SEO is required for all pages: unique title and description, canonical URL, Open Graph/Twitter image, and appropriate JSON-LD. Images must resolve publicly. Update the build/check scripts if adding a new content type.
