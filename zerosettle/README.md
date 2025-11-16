# Website

This website is built using [Docusaurus](https://docusaurus.io/), a modern static website generator.

## Installation

```bash
yarn
```

## Local Development

```bash
yarn start
```

This command starts a local development server and opens up a browser window. Most changes are reflected live without having to restart the server.

## Build

```bash
yarn build
```

This command generates static content into the `build` directory and can be served using any static contents hosting service.

## Deployment

### Netlify Deployment

This site is deployed using [Netlify](https://www.netlify.com/), which automatically builds and deploys the Docusaurus site when changes are pushed to the repository.

#### Netlify Configuration

Netlify is configured to:
- **Build Command**: `npm run build`
- **Publish Directory**: `build`
- **Base Directory**: `zerosettle` (if the Docusaurus site is in a subdirectory)

#### Custom Domain Setup (docs.zerosettle.io)

To support the custom domain `docs.zerosettle.io`, the following DNS configuration was set up in GoDaddy:

1. **CNAME Record in GoDaddy**:
   - **Type**: CNAME
   - **Name**: `docs`
   - **Value/Points to**: Your Netlify site URL (e.g., `your-site-name.netlify.app`)
   - **TTL**: 1 Hour (or default)

2. **Netlify Domain Settings**:
   - In Netlify site settings, go to **Domain Settings** → **Custom Domains**
   - Add `docs.zerosettle.io` as a custom domain
   - Netlify automatically provisions an SSL certificate via Let's Encrypt

3. **Docusaurus Configuration**:
   - The `url` in `docusaurus.config.js` is set to match the custom domain:
     ```javascript
     url: 'https://docs.zerosettle.io'
     ```
   - This ensures all generated URLs, sitemaps, and metadata use the correct production domain

The CNAME forwarding from GoDaddy routes traffic from `docs.zerosettle.io` to the Netlify-hosted site, while Netlify handles the SSL certificate and serves the built Docusaurus static files.

### Alternative Deployment (GitHub Pages)

If you prefer to use GitHub Pages instead of Netlify:

Using SSH:

```bash
USE_SSH=true yarn deploy
```

Not using SSH:

```bash
GIT_USER=<Your GitHub username> yarn deploy
```

This command builds the website and pushes to the `gh-pages` branch.
