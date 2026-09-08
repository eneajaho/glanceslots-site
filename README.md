# Glance Slots website (static)

Landing page, privacy policy and support page for glanceslots.com. Plain HTML + one stylesheet, no JavaScript, no analytics, no cookies. Assets are downscaled copies of the App Store screenshots and the marketing video.

| Path | URL |
|---|---|
| `index.html` | https://glanceslots.com/ |
| `support/index.html` | https://glanceslots.com/support/ |
| `privacy/index.html` | https://glanceslots.com/privacy/ |

## Deploy to GitHub Pages (free, HTTPS included)

1. Push the repo to GitHub (private is fine; Pages works on private repos with a paid plan, on public repos always).
2. Repository → Settings → Pages → **Source: GitHub Actions**. The workflow `marketing/site-deploy/pages.yml (move to .github/workflows/ once the token has the workflow scope, see marketing/site-deploy/README.md)` publishes this folder on every push to `main` that touches it; run it once manually via Actions → "Deploy site" → Run workflow.
3. The site is live at `https://<github-user>.github.io/<repo>/` within a minute. Use those URLs in App Store Connect until the domain is ready.
4. Custom domain, once glanceslots.com is registered: at the registrar add DNS records
   - `A` @ → 185.199.108.153, 185.199.109.153, 185.199.110.153, 185.199.111.153
   - `AAAA` @ → 2606:50c0:8000::153, 2606:50c0:8001::153, 2606:50c0:8002::153, 2606:50c0:8003::153
   - `CNAME` www → `<github-user>.github.io`
   then Settings → Pages → Custom domain `glanceslots.com` → wait for the DNS check → tick **Enforce HTTPS** (GitHub issues the certificate).
5. Verify: `curl -I https://glanceslots.com/support/` returns 200.

Alternative: Cloudflare Pages (connect the repo, build command none, output directory `marketing/site`).

## Changing the domain or e-mail

Everything assumes `glanceslots.com` and `support@glanceslots.com`. To change:

```sh
grep -rl "glanceslots.com" marketing/ apps/glanceable/docs | xargs sed -i '' 's/glanceslots\.app/NEWDOMAIN/g'
```

## Preview locally

```sh
cd marketing/site && python3 -m http.server 8080   # open http://localhost:8080/
```
