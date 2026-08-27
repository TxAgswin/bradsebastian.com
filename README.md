# bradsebastian.com

Static résumé site. One HTML file, one PDF, no build step.

## Files
- `index.html` — the site (all CSS, JS, logos, and the photo are embedded).
- `BradSebastian_Resume.pdf` — what the Resume button downloads. Replace this file to update the download; keep the filename.
- `netlify.toml` — Netlify settings (publish root, a few security headers).

## Go live: GitHub → Netlify → GoDaddy DNS

### 1. GitHub (host the code)
1. Create a new repository at github.com/new named `bradsebastian.com` (private is fine).
2. Upload these files (drag and drop on the repo page → "Add file → Upload files", or `git push` from a local clone).
3. Commit to the `main` branch.

### 2. Netlify (serve the site)
1. Sign in at app.netlify.com with your GitHub account.
2. "Add new site" → "Import an existing project" → GitHub → pick `bradsebastian.com`.
3. Settings: branch `main`, build command **empty**, publish directory `.` (netlify.toml already says this). Deploy.
4. You get a URL like `something-123.netlify.app`. Check it. From now on every commit to `main` redeploys automatically in ~30 seconds.

### 3. Custom domain
In Netlify: Site → "Domain management" → "Add a domain" → `bradsebastian.com`. Netlify adds both `bradsebastian.com` and `www.bradsebastian.com`.

Then pick ONE of these at GoDaddy:

**Option A — keep GoDaddy DNS (safest if you have email on this domain).**
GoDaddy → My Products → bradsebastian.com → DNS → add/replace:
| Type  | Name | Value                          |
|-------|------|--------------------------------|
| A     | @    | 75.2.60.5                      |
| CNAME | www  | your-site-name.netlify.app     |

Delete any existing A record for `@` and any "Parked"/"Forwarding" CNAME for `www` first. Leave MX and everything else alone.

**Option B — move DNS to Netlify (best performance).**
Netlify → Domain management → "Set up Netlify DNS" → it gives you 4 nameservers (dns1–dns4.p0N.nsone.net). GoDaddy → DNS → Nameservers → "Change" → enter them. Before you do this, copy every existing DNS record from GoDaddy (especially MX/TXT if you have email on the domain) and re-create them in Netlify DNS, or mail will stop.

### 4. HTTPS
After DNS propagates (minutes to 24 hours), Netlify → Domain management → HTTPS → "Verify DNS configuration" → "Provision certificate". Free, automatic renewal. Set `bradsebastian.com` as the primary domain so `www` redirects to it.

## Updating the site later
Edit `index.html` in GitHub (pencil icon) → commit → live in under a minute. Replace the PDF the same way.
