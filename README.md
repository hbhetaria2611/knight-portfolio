This is just a personal website code

## Analytics Setup

This portfolio uses **Cloudflare Web Analytics** for privacy-preserving visitor tracking.

### Quick Setup

1. Go to [Cloudflare Dashboard](https://dash.cloudflare.com)
2. Navigate to: **Analytics & Logs** > **Web Analytics**
3. Click **"Add a site"** and enter your domain
4. Copy your analytics token
5. In `index.html`, replace `YOUR_CLOUDFLARE_WEB_ANALYTICS_TOKEN` with your token

### What Gets Tracked

**Automatic Tracking:**
- Page views and unique visitors
- Referrer sources
- Geographic location (country-level)
- Browser/device info
- Performance metrics

**Custom Events:**
- Dark/light mode toggles
- Resume checksum copies
- GPG key interactions (copy/download)
- Easter egg discoveries
- Console command usage

View analytics at: https://dash.cloudflare.com > Analytics & Logs > Web Analytics
