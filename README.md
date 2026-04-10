# walensis-site

Marketing site for [Walensis](https://walensis.com), the Chrome extension that
analyzes resale listings to estimate fair market value.

Built with [Astro](https://astro.build).

## Pages

- `/` — landing page
- `/privacy` — privacy policy
- `/terms` — terms of service
- `/support` — support contact and bug reporting info

## Development

```bash
pnpm install
pnpm dev      # http://localhost:4321
```

## Build

```bash
pnpm build    # outputs to dist/
pnpm preview  # serve the built site locally
```

## Deployment

This site is deployed to Cloudflare Pages, connected to this GitHub repo.
Pushes to `main` deploy automatically.

DNS for `walensis.com` is managed at GoDaddy and points to Cloudflare Pages.
