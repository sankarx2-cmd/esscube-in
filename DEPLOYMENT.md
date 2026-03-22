# Esscube Site Deployment

This static site is prepared for the same public-site routine used elsewhere:

- code in GitHub
- public website on Cloudflare Pages
- domain registered at GoDaddy
- authoritative DNS on Cloudflare after nameserver switch
- reserve Render and Resend for a future contact-form backend at `api.esscube.in`

## Public domain plan

- Primary public domain: `esscube.in`
- Secondary domain: `www.esscube.in`
- Future API subdomain: `api.esscube.in`

## GitHub

Create a dedicated GitHub repo for this folder, for example `sankarx2-cmd/esscube-in`, and push the contents of this directory as the repo root.

## Cloudflare Pages

Recommended Pages settings:

- Framework preset: `None`
- Production branch: `main`
- Build command: `exit 0`
- Build output directory: `.`

After Pages is created:

1. Add the custom domain `esscube.in`
2. Add the custom domain `www.esscube.in`
3. Keep `api.esscube.in` free for the future Render service

## GoDaddy to Cloudflare DNS cutover

The current registrar is GoDaddy, but the recommended DNS authority is Cloudflare.

Safe cutover sequence:

1. Add `esscube.in` to Cloudflare
2. Let Cloudflare import the existing DNS zone from GoDaddy
3. Verify these records are still present in Cloudflare before switching nameservers:
   - Zoho MX records
   - Zoho verification CNAME
   - any other mail-related TXT or CNAME records
4. In GoDaddy, change the domain nameservers from GoDaddy defaults to the two Cloudflare nameservers assigned to `esscube.in`

## Important DNS note

The current GoDaddy `A` record for `@` points at the old site (`217.21.81.69`).
Once the domain is active in Cloudflare Pages, that old origin can be removed from the new Cloudflare DNS zone.

## Files that must be in the repo root

- `index.html`
- `Esscube_Logo.png`
- `robots.txt`
- `sitemap.xml`
