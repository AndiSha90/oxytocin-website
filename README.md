# Oxytocin Website — Deployment Guide

This folder contains the Oxytocin coming-soon website.

## What's in here

| File | Purpose |
|---|---|
| `index.html` | Coming-soon landing page (homepage) |
| `privacy.html` | GDPR-compliant Privacy Policy |
| `terms.html` | Terms of Service for an 18+ dating app |
| `README.md` | This file (not deployed) |

All three pages share the same brand identity — coral pink (#C9184A), Fraunces serif headlines, Inter Tight body text. They link to each other through the navigation and footer.

---

## How to put this online (45 minutes total)

### Step 1 — Buy a domain (~$15/year, 5 minutes)

1. Go to **Cloudflare Registrar** (https://www.cloudflare.com/products/registrar/) — cheapest, no markup
   - Alternative: Namecheap, Porkbun, or Google Domains all work too
2. Search for `oxytocinapp.com`
   - If taken, try: `oxytocin.love`, `getoxytocin.com`, `oxytocinapp.com`
3. Buy it (.app domains are about $14/year on Cloudflare)
4. **Important:** enable WHOIS privacy (free on Cloudflare) so your name and address aren't publicly searchable

### Step 2 — Create a Vercel account (free, 5 minutes)

1. Go to **https://vercel.com**
2. Sign up with your GitHub account (recommended — same one you use for Oxytocin)
3. No credit card needed for the Hobby (free) tier

### Step 3 — Deploy the site (5 minutes)

**Option A: Drag and drop (easiest)**

1. From the Vercel dashboard, click **"Add New" → "Project"**
2. Scroll down — there's an option to upload a folder directly, OR
3. Easier: drag this whole `oxytocin-site` folder onto the Vercel deploy page at https://vercel.com/new
4. Vercel will give you a free URL like `oxytocin-site-xxx.vercel.app` immediately

**Option B: Through GitHub (better for updates)**

1. Create a new GitHub repo called `oxytocin-website`
2. Upload these files to it
3. In Vercel, click **"Add New" → "Project"** → import the repo
4. Click **Deploy** — it goes live in ~30 seconds
5. Now any time you push changes to GitHub, Vercel re-deploys automatically

### Step 4 — Connect your domain (10 minutes)

1. In Vercel, go to your project → **Settings → Domains**
2. Add `oxytocinapp.com` (and `www.oxytocinapp.com` if you want both)
3. Vercel will tell you to add some DNS records at your domain registrar
4. Go to Cloudflare → DNS settings for oxytocinapp.com → add the records Vercel showed you
5. Wait 5–60 minutes for DNS to propagate
6. Done — your site is live at https://oxytocinapp.com

### Step 5 — Set up email forwarding (10 minutes)

You need `support@oxytocinapp.com` to actually receive email.

1. Go to **Cloudflare** (where you bought the domain) → click `oxytocinapp.com`
2. Click **Email** → **Email Routing** in the sidebar
3. Enable Email Routing (free)
4. Add a routing rule: `support@oxytocinapp.com` → forwards to your real personal email (Gmail, etc.)
5. Verify your personal email (Cloudflare sends a confirmation)
6. Done — emails to `support@oxytocinapp.com` will land in your inbox

If you bought elsewhere, **Forward Email** (https://forwardemail.net) is free and works the same way.

### Step 6 — Test everything (10 minutes)

- Visit https://oxytocinapp.com — landing page should load
- Click **Privacy** in the nav — should show Privacy Policy
- Click **Terms** in the nav — should show Terms of Service
- Click `support@oxytocinapp.com` — should open your mail app
- Send a test email to `support@oxytocinapp.com` from another address — should arrive in your inbox
- Try on your phone — site should look good on mobile too

---

## Things you'll want to do later

### Add real screenshots

The hero section currently shows a fake "Sarah, 28" mock card built with CSS. To replace it with a real iPhone screenshot of your app:

1. Take a clean screenshot on your iPhone (Cmd+Shift+3 on Mac to crop after AirDrop, or just AirDrop the screenshot)
2. Name it `app-preview.png` and put it in this folder
3. In `index.html`, find the `<div class="phone">` section
4. Replace its inner content with: `<img src="app-preview.png" alt="Oxytocin app preview" style="width: 100%; height: 100%; object-fit: cover; border-radius: 32px;">`

### Update the site as the app evolves

- **Add launch date** when you have one — update the "In Development" badge in `index.html` to "Launching [month/year]"
- **Add screenshots gallery** when the app is more polished — use a `<section>` with a grid of phone images
- **Add an email signup form** when you want to capture launch notifications — use a service like ConvertKit, Mailchimp, or Buttondown (free for first 1000 subscribers)

### Before App Store submission

Apple requires you to provide a Privacy Policy URL during App Store submission. Use:
```
https://oxytocinapp.com/privacy.html
```

Apple will check it loads and contains expected content. The draft I built covers the standard requirements but **strongly recommend a lawyer review before launch** — especially because:

- Dating apps are a high-scrutiny category
- You're processing sensitive personal data (location, sexual orientation, photos)
- GDPR enforcement in EU is strict
- One-person developers can absorb fines that big companies shrug off

Affordable options:
- **Termly** (https://termly.io) — €15/month, generates legally-vetted templates you can customize
- **iubenda** (https://iubenda.com) — €15-30/month, similar
- **LegalBuddy.se** — Sweden-based affordable legal services, ~3,000-5,000 kr for a review

---

## Common questions

### Can I change the colors?

Yes. Open any HTML file, find the `:root { ... }` section near the top of the `<style>` block. Change the CSS variables:
- `--coral` is the main pink
- `--cream` is the background
- `--ink` is the dark text

Save and refresh.

### Can I change the text?

Yes. Open the relevant HTML file in any text editor (VS Code, Notepad, anything). The text is plain English between the HTML tags. Edit, save, re-deploy (or if you're using GitHub + Vercel, just commit and push — auto-deploys).

### Why is the site so simple?

This is a coming-soon page, not a full marketing site. Once the app actually launches, you'll want more pages (Features, How it Works, FAQ, Press, Careers, etc.) — that comes later. Right now the goal is: **anyone who hears about the app and looks for it online finds something that confirms it's real and being built carefully.**

### Why no email signup form?

Forms need a backend (server or third-party service) to actually capture submissions. Adding it without that = broken form, looks bad. Add it later when you're ready to integrate ConvertKit/Mailchimp/Buttondown — those services give you a snippet you paste in.

### Can I use this site for both the website AND App Store privacy URL?

Yes — that's the point. Apple just wants `https://oxytocinapp.com/privacy.html` to load and show a privacy policy. Same domain, same files.

---

## Total monthly cost when live

- Domain (Cloudflare): ~$14/year = **$1.20/month**
- Vercel hosting (Hobby tier): **$0/month**
- Email forwarding (Cloudflare): **$0/month**

**Total: about $1.20/month** for a professional website with a real domain and working email. That's it.

---

## Questions or stuck?

Email me (Andreas) at the same address that's on the site, or come back to Claude with the exact step you're stuck on.

Last updated: May 6, 2026.
