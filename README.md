# TownScout

A local discovery app — find restaurants, events, outdoor spots, shops, and gas stations nearby, with a randomizer for when you can't decide.

## Deploy to GitHub Pages

1. Create a new repository on GitHub named `thetownscout` (or anything you like).
2. Upload every file in this folder to the repository — drag-and-drop on the GitHub website works, or use git (see below).
3. In the repo, go to **Settings → Pages**.
4. Under **Build and deployment**, set **Source** to "Deploy from a branch."
5. Set **Branch** to `main` and the folder to `/ (root)`, then save.
6. Give it a minute, then it'll be live at `https://<your-username>.github.io/<repo-name>/`.

### Using git instead of the web upload

```bash
git init
git add .
git commit -m "Initial commit"
git branch -M main
git remote add origin https://github.com/<your-username>/<repo-name>.git
git push -u origin main
```

## Connecting your thetownscout.com domain

This repo already includes a `CNAME` file set to `thetownscout.com`. To finish connecting it:

1. At your domain registrar, add these DNS records:
   - Four **A records** for the root domain (`thetownscout.com`), pointing to:
     ```
     185.199.108.153
     185.199.109.153
     185.199.110.153
     185.199.111.153
     ```
   - One **CNAME record** for `www`, pointing to `<your-username>.github.io`.
2. In the repo, go to **Settings → Pages**, enter `thetownscout.com` under **Custom domain**, and save.
3. Check **Enforce HTTPS** once it becomes available (can take a few minutes to a few hours after DNS propagates).

If you bought a different extension than `.com` (like `.io` or `.co`), just edit the `CNAME` file to match your actual domain before you push.

## Install it on your phone

Once the site is live, open it on your phone:

- **iPhone**: open the link in Safari → tap the Share icon → "Add to Home Screen."
- **Android**: open the link in Chrome → tap the menu (⋮) → "Install app" (or accept the install prompt if it appears).

It launches full-screen from your home screen icon, like a native app.

## Important: the live search needs a backend

This app currently looks up real nearby places by calling Anthropic's API directly from the browser. That call only works inside Claude's in-chat preview, where it's authenticated for you automatically. Once hosted on GitHub Pages, that search will stop working, because:

- GitHub Pages only serves static files — it can't run a backend or hide an API key.
- An API key can never be safely embedded in client-side code; anyone could read it from the page source.

To make the search work for real, you have two options:

1. **Add a small serverless backend** (e.g. a Cloudflare Worker or Vercel function) that holds your Anthropic API key and proxies the request. GitHub Pages can host the app while a separate free service hosts this one function.
2. **Switch to a client-side-key API** like Google Places, which is designed to be called with a restricted API key directly from the browser.

Let me know if you'd like help building either of those.

## Files

- `index.html` — the app itself
- `manifest.json` — makes it installable as a web app
- `service-worker.js` — caches the app shell for fast, offline-capable loading
- `CNAME` — points GitHub Pages at thetownscout.com
- `icon-*.png` — app icons, cropped and resized from your logo artwork
- `townscout-logo.png` — the full logo, trimmed of extra whitespace

## Brand colors

Pulled directly from the logo artwork, in case you need them elsewhere:

- Navy (text): `#162C37`
- Moss green (primary accent): `#5E6F33`
- Terracotta (call-to-action accent, from the compass needle): `#D15621`
