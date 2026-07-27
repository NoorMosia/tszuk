---
inclusion: fileMatch
fileMatchPattern: '{astro.config.*,wrangler*}'
---

# Deployment — Cloudflare Pages

## Astro Configuration

```js
// astro.config.mjs
import { defineConfig } from 'astro/config';
import cloudflare from '@astrojs/cloudflare';

export default defineConfig({
  output: 'server',
  adapter: cloudflare(),
});
```

- `output: 'server'` is required for the `/api/contact` endpoint to run as a Cloudflare Worker.
- Static pages are still served from the CDN edge — only API routes use the Worker runtime.

## Environment Variables

| Variable | Required | Purpose |
|----------|----------|---------|
| `RESEND_API_KEY` | Yes (production) | Authenticates with Resend email API |

- Local development: store in `.env` file (already in `.gitignore`).
- Production: set in Cloudflare Pages dashboard under Settings → Environment Variables.
- Access in API routes via `import.meta.env.RESEND_API_KEY` or the Cloudflare runtime context.

## Build

- Command: `npm run build`
- Output directory: `dist/` (Cloudflare auto-detects this for Astro)
- Node version: 18+ (set in Cloudflare dashboard or via `.node-version` file)

## Preview Locally

```bash
npm run preview
```

This uses the Cloudflare adapter's local emulation (Wrangler under the hood).

## Deployment Checklist

1. `npm run build` succeeds without errors.
2. `RESEND_API_KEY` is set in the Cloudflare Pages environment.
3. All images are processed by Astro `<Image>` (no raw external URLs).
4. No `.env` file committed to version control.
