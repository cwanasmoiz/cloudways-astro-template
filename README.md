# Cloudways Astro Template

A minimal [Astro](https://astro.build/) starter you can deploy on [Cloudways](https://www.cloudways.com/) or any static host.

Includes a Cloudways-branded sample home page so you can confirm the deploy worked, then replace it with your own site.

## Features

- Astro 7 with TypeScript
- Static site output (`npm run build` → `dist/`)
- Cloudways-branded sample home page
- Works on Cloudways, Netlify, Vercel, Cloudflare Pages, GitHub Pages, and any Apache/Nginx host

## Quick start (local)

```bash
git clone https://github.com/YOUR_USERNAME/cloudways-astro-template.git
cd cloudways-astro-template
npm install
npm run dev
```

Open [http://localhost:4321](http://localhost:4321) to see the Cloudways-branded sample home page.

| Command           | Description                          |
| ----------------- | ------------------------------------ |
| `npm run dev`     | Start local development server       |
| `npm run build`   | Build production files into `dist/`  |
| `npm run preview` | Preview the production build locally |

## Deploy on Cloudways

Cloudways serves static sites from your application’s `public_html` directory over Apache (ports 80/443).

### 1. Create a Cloudways application

1. Sign in to the [Cloudways dashboard](https://platform.cloudways.com/).
2. Create a server (DigitalOcean, AWS, etc.).
3. Add a new application (PHP/Custom Application is fine for static files).

### 2. Build the site

**Option A — Build locally, then upload**

```bash
npm install
npm run build
```

Upload the contents of `dist/` into `public_html/` via SFTP, or:

```bash
# Example: sync dist to Cloudways public_html
scp -r dist/* master@YOUR_SERVER_IP:~/applications/YOUR_APP/public_html/
```

**Option B — Build on the server (SSH)**

```bash
ssh master@YOUR_SERVER_IP
cd ~/applications/YOUR_APP/public_html
git clone https://github.com/YOUR_USERNAME/cloudways-astro-template.git .
npm install
npm run build
# Move built files to the web root (or point the docroot at dist/)
cp -r dist/* .
```

### 3. Optional Apache rules

If you add client-side routing later, copy `.htaccess.example` to `public_html/.htaccess` so unknown paths fall back to `index.html`.

For a plain Astro static site, Apache can serve the generated HTML files as-is — no Node process or PM2 is required.

### 4. Verify

Visit your Cloudways application URL. You should see the Cloudways-branded sample home page.

## Deploy elsewhere

This template is host-agnostic. Build once, deploy `dist/`.

| Platform | Notes |
| -------- | ----- |
| **Netlify / Vercel / Cloudflare Pages** | Connect the repo; build command `npm run build`, publish directory `dist` |
| **GitHub Pages** | Build in CI and publish `dist/` |
| **Nginx / VPS / Docker** | Serve `dist/` as the document root |

## Project structure

```
.
├── public/                 # Static assets (copied to dist as-is)
│   ├── cloudways-logo.svg
│   ├── favicon.ico
│   └── hero-cloud.svg
├── src/
│   ├── layouts/            # Shared HTML shell
│   ├── pages/              # File-based routes (index.astro = /)
│   └── styles/             # Global CSS tokens
├── astro.config.mjs
└── package.json
```

## Customization

1. Edit `src/pages/index.astro` to replace the sample home page.
2. Add routes by creating files in `src/pages/`.
3. Put images and other static files in `public/`.
4. Update site metadata in `src/layouts/BaseLayout.astro`.

## Troubleshooting (Cloudways)

| Issue | Fix |
| ----- | --- |
| Blank page / old content | Confirm `public_html` contains the latest `dist/` output |
| CSS/images 404 | Deploy the full `dist/` folder, not only `index.html` |
| Build fails on server | Use Node 22+ (`node -v`); upgrade via Cloudways if needed |

## License

MIT — see [LICENSE](LICENSE).

## Contributing

PRs welcome. Fork, branch, and open a pull request.

---

**Use this repo as a GitHub template:** click **Use this template** on GitHub to create your own project from this starter.
