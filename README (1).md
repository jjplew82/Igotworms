# I Got Worms — Setup Guide

## What you have
A single self-contained site: `index.html` (all CSS/JS inline, Google Fonts loaded via CDN). No build step — you can open it directly in a browser or upload it as-is to any static host.

## 1. Get approved for Amazon Associates
Amazon requires your site to be **live and public** before they'll review your application — you can't apply with a local file.
1. Host the site first (see §3).
2. Apply at [affiliate-program.amazon.com](https://affiliate-program.amazon.com).
3. Amazon typically requires 3 qualifying sales within 180 days to stay approved, so drive some real traffic before/while you wait.
4. Once approved, you'll get a **tracking ID** (looks like `igotworms0d-20`).

## 2. Wire in your real tag and products
Open `index.html` and find:
```js
const AFFILIATE_TAG = "PLACEHOLDER-TAG-20";
```
Replace with your real tag.

Every product card lives in the `PRODUCTS` object near the bottom of the file, e.g.:
```js
{tag:"Test kit", title:"...", desc:"...", price:"$24.99", icon:"kit", asin:"PLACEHOLDER-ASIN"},
```
Replace `asin` with the real 10-character ASIN from the Amazon product URL (`amazon.com/dp/ASIN_HERE/`). Update `title`, `desc`, and `price` to match the real listing — **don't leave marketing copy that doesn't match what's actually being sold**, that's an Amazon Associates policy violation as well as generally deceptive.

For real product **images**, either:
- Use Amazon's **SiteStripe** toolbar (shows up on product pages once you're logged into your Associates account) to grab a pre-approved image + link snippet, or
- Pull structured data via the **Product Advertising API (PA-API)**, which is the only way to legally display live prices/images/availability that auto-update. This requires your Associates account plus a qualifying sales history to get API access.

The placeholder line-icon cards are there so the site isn't legally exposed while you don't yet have real image rights — you can ship it looking like this indefinitely if you'd rather keep the illustrated style.

## 3. Hosting igotworms.com
Any static host works since there's no backend:
- **Cloudflare Pages / Netlify / Vercel** — free tier, drag-and-drop the folder, point your domain's DNS at them.
- **GitHub Pages** — free, works well if you want version control on the product data too.

Point your domain registrar's DNS to whichever host you pick (they'll give you the exact records).

## 4. Compliance checklist (don't skip these)
- ✅ **FTC/Amazon disclosure** — already on the site (top bar + footer). Required, not optional.
- ✅ **`rel="nofollow sponsored"`** on every outbound product link — already added, this is Google's required markup for paid/affiliate links.
- ⚠️ **Health claims** — copy in the "For People" aisle is deliberately general (testing, hygiene, herbal supplements framed as traditional-use) rather than treatment/dosing claims. Keep it that way. Amazon suspends Associates accounts for unsubstantiated medical claims, and the FTC separately regulates health advertising claims.
- ⚠️ **Prescription-only drugs** — true anthelmintic prescription drugs (e.g. albendazole for humans) generally aren't sold OTC on Amazon in the US. Stick to what's actually legally sold there: test kits, herbal/wellness supplements, hygiene products, and OTC veterinary/livestock dewormers (many livestock dewormers like ivermectin pour-ons ARE legitimately OTC for animal use).
- ⚠️ **Species-specific warnings** — worth keeping visible near the pet/livestock sections: some dewormers (e.g. ivermectin) are dangerous for certain dog breeds (collies and other herding breeds with the MDR1 gene mutation) and for certain species combos. A short warning here is good practice, not just legal cover.
- ⚠️ **Price/availability drift** — Amazon's terms require you not to display stale prices as if current. The footer disclaimer covers this; if you move to live PA-API data this becomes moot since prices pull in real time.

## 5. Optional next steps
- Add a `robots.txt` and `sitemap.xml` once hosted, for SEO.
- Consider a blog/content section ("how to tell if your dog has worms") — Amazon favors Associates sites with genuine editorial content over pure link farms, and it's also just better for organic traffic.
- Add Google Analytics or Cloudflare Web Analytics to track which aisle converts best.
