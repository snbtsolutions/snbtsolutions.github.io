# SNBT Solutions Website — Setup, Deploy & Go-Live Guide

This folder is a complete, ready-to-host website. No build tools, no database, no monthly server.

```
snbt-site/
├── index.html      ← the whole website (all sections, styles, scripts)
├── 404.html        ← "page not found" page
├── favicon.svg     ← browser tab icon / logo mark
├── robots.txt      ← tells Google it may index the site
├── sitemap.xml     ← list of pages for search engines
└── DEPLOY-GUIDE.md ← this file
```

Total cost to go live: **about $10–20 per year** (only the domain name). Hosting is free.

---

## Step 1 — Personalize the content (15 minutes)

Open `index.html` in any text editor (VS Code is free: https://code.visualstudio.com) and use **Find & Replace**:

| Find | Replace with |
|---|---|
| `snbtsolutions.com` | your real domain (if different) — also replace in `robots.txt` and `sitemap.xml` |
| `info@snbtsolutions.com` | your real business email |
| `+1 (000) 000-0000` | your real phone number |
| `https://www.linkedin.com/` | your company LinkedIn page URL |

Also review:
- The **services list** (search `SVC-01` … `SVC-10`) — delete or edit any you don't offer, and adjust the technology tags.
- The **industries** and **support response times table** (P1–P4) — change times to what you actually commit to.
- Add your office address in the Contact section if you want it shown.

To preview: double-click `index.html` and it opens in your browser.

---

## Step 2 — Buy your domain (10 minutes)

1. Check availability of `snbtsolutions.com` (or `.io`, `.tech`, `.co` if taken) at one of:
   - **Cloudflare Registrar** — https://www.cloudflare.com/products/registrar/ (at-cost pricing, recommended)
   - Namecheap — https://www.namecheap.com
   - Porkbun — https://porkbun.com
   - GoDaddy — https://www.godaddy.com
2. Buy it for 1–3 years and turn on **auto-renew** and **WHOIS privacy** (free at most registrars).

> Avoid paid add-ons (hosting bundles, "SEO packages", premium DNS). You don't need them.

---

## Step 3 — Host the site for free (choose ONE option)

### Option A: Netlify (easiest — drag and drop)
1. Create a free account at https://app.netlify.com/signup.
2. Go to **Sites → Add new site → Deploy manually**.
3. Drag the whole `snbt-site` folder onto the upload box.
4. In about 10 seconds you get a live URL like `random-name-123.netlify.app`. Open it and check the site.
5. **Site configuration → Change site name** → `snbtsolutions` (gives `snbtsolutions.netlify.app`).
6. To update later: **Deploys** tab → drag the folder in again.

### Option B: Cloudflare Pages (best if your domain is on Cloudflare)
1. Log in at https://dash.cloudflare.com → **Workers & Pages → Create → Pages → Upload assets**.
2. Name the project `snbtsolutions`, upload the folder, click **Deploy**.
3. You get `snbtsolutions.pages.dev`.

### Option C: GitHub Pages (good if you want version history)
1. Create a free account at https://github.com, then **New repository** → name it `snbt-website`, Public.
2. **Add file → Upload files** → drag in all files from the folder → **Commit changes**.
3. **Settings → Pages → Source: Deploy from a branch → Branch: main / (root) → Save**.
4. After 1–2 minutes the site is at `https://<your-username>.github.io/snbt-website/`.

All three give you free HTTPS (the padlock) automatically.

---

## Step 4 — Connect your domain (15 min + up to 24 hrs to spread)

### If using Netlify
1. **Domain management → Add a domain** → enter `snbtsolutions.com` → Verify → Add.
2. Easiest route: choose **Set up Netlify DNS**, then copy the 4 nameservers Netlify shows (e.g. `dns1.p01.nsone.net`).
3. At your registrar, open the domain → **Nameservers → Custom** → paste the 4 nameservers → Save.
4. Back in Netlify, under **HTTPS**, click **Verify DNS configuration** → **Provision certificate** (often automatic).

*Alternative (keep DNS at your registrar):* add these records at the registrar:

| Type | Name / Host | Value |
|---|---|---|
| A | `@` | `75.2.60.5` |
| CNAME | `www` | `snbtsolutions.netlify.app` |

### If using Cloudflare Pages
1. Project → **Custom domains → Set up a custom domain** → enter `www.snbtsolutions.com`, then repeat for `snbtsolutions.com`.
2. If the domain is on Cloudflare, records are created for you. Done.

### If using GitHub Pages
1. Repo **Settings → Pages → Custom domain** → `www.snbtsolutions.com` → Save, then tick **Enforce HTTPS** once available.
2. At your registrar add:

| Type | Name | Value |
|---|---|---|
| A | `@` | `185.199.108.153` |
| A | `@` | `185.199.109.153` |
| A | `@` | `185.199.110.153` |
| A | `@` | `185.199.111.153` |
| CNAME | `www` | `<your-username>.github.io` |

> Always confirm these IP values against your host's current documentation, since providers occasionally change them.

**Check it worked:** visit https://dnschecker.org, enter your domain, and wait until most locations show the new records. Then open `https://www.snbtsolutions.com` and confirm the padlock appears.

---

## Step 5 — Set up a business email (optional but recommended)

Use an address on your own domain (`info@snbtsolutions.com`) — it looks far more credible than Gmail.
- **Google Workspace** (~$7/user/month): https://workspace.google.com
- **Microsoft 365 Business Basic** (~$6/user/month): https://www.microsoft.com/microsoft-365/business
- **Zoho Mail** (free plan available): https://www.zoho.com/mail/
- **Cloudflare Email Routing** (free forwarding to your Gmail): Cloudflare dashboard → Email → Email Routing

Each provider gives you MX and TXT records to add in your DNS settings. Add them exactly as shown. They do not affect the website.

---

## Step 6 — Make the contact form deliver to your inbox (5 minutes)

The form is ready for **Formspree** (free plan: 50 messages/month).
1. Sign up at https://formspree.io with your business email.
2. **+ New Form** → name it "SNBT website" → copy the form endpoint, e.g. `https://formspree.io/f/xyzabcd`.
3. In `index.html` find `https://formspree.io/f/YOUR_FORM_ID` and replace it with your endpoint.
4. Re-upload the site (Step 3), submit a test message, and confirm it in your inbox (the first one asks you to verify).

*Using Netlify?* Alternatively use Netlify Forms: change the form tag to `<form id="contact-form" name="contact" method="POST" data-netlify="true" action="/">`, add `<input type="hidden" name="form-name" value="contact">` inside it, and in the script replace the fetch URL with `"/"`. Submissions then appear under **Forms** in Netlify.

---

## Step 7 — Get found on Google (the key go-live step)

A new site does **not** appear in Google automatically right away. Do these:

### 7a. Google Search Console (free)
1. Go to https://search.google.com/search-console → **Add property → Domain** → enter `snbtsolutions.com`.
2. Google shows a TXT record like `google-site-verification=abc123…`. Add it as a **TXT** record (Name `@`) at your DNS provider → click **Verify** (may take a few minutes to an hour).
3. Left menu **Sitemaps** → enter `sitemap.xml` → **Submit**.
4. **URL Inspection** → paste `https://www.snbtsolutions.com/` → **Request indexing**.
5. Typically your site appears for the search **"SNBT Solutions"** within a few days to 2 weeks.

### 7b. Bing Webmaster Tools (also feeds DuckDuckGo & Yahoo)
1. https://www.bing.com/webmasters → sign in → **Import from Google Search Console** (one click).

### 7c. Google Business Profile (shows your company in Maps and the side panel)
1. https://www.google.com/business → **Manage now** → enter "SNBT Solutions", category **Software company** or **IT services**.
2. Add website, phone, hours, logo and service areas. Complete Google's verification (postcard, phone, or video).

### 7d. Build credibility signals (these help ranking)
- Create a **LinkedIn company page**, and put your website URL on it. Put the LinkedIn link in the site footer.
- List the company on **Clutch.co**, **GoodFirms**, **Crunchbase**, and local business directories with the exact same name, phone, and website.
- Ask early clients to leave Google reviews.
- In `index.html`, add your social profile URLs inside the `"sameAs": []` list in the structured-data block near the top, e.g. `"sameAs": ["https://www.linkedin.com/company/snbt-solutions"]`.

---

## Step 8 — Go-live checklist

- [ ] Placeholder email / phone / LinkedIn replaced
- [ ] Domain in `index.html`, `robots.txt`, `sitemap.xml` matches your real domain
- [ ] Site loads at both `snbtsolutions.com` and `www.snbtsolutions.com` with the padlock (HTTPS)
- [ ] Contact form test message received
- [ ] Looks right on a phone (open it on your mobile)
- [ ] Speed check at https://pagespeed.web.dev (should score 90+)
- [ ] Search Console verified, sitemap submitted, indexing requested
- [ ] Bing Webmaster Tools imported
- [ ] Google Business Profile created
- [ ] LinkedIn company page links to the website

---

## Updating the site later

1. Edit `index.html` locally and preview it in your browser.
2. Re-upload: Netlify → drag folder into **Deploys**; Cloudflare Pages → **Create new deployment**; GitHub → upload changed files and commit.
3. Changes are live within a minute.

## Growing later (optional)

- **Analytics:** Cloudflare Web Analytics (free, no cookies) or Google Analytics 4.
- **More pages:** copy `index.html` to e.g. `careers.html`, keep the header/footer, change the content, and add each new page to `sitemap.xml`.
- **Blog / case studies:** publishing helpful articles monthly ("How to migrate to Azure", client case studies) is the most effective way to rank for searches beyond your company name.
