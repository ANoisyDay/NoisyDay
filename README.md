# NoisyDay
We started creating films together in our early college years and have learned narrative in any form is essential. On Noisy Day we strive to tell original stories, wether that’s documentary’s, commercial’s, or films. 
# Noisy Day — Webflow Build Plan

**Objective:** Build a Webflow site for **Noisy Day** — editorial-first, responsive, simple typography, a shop, social embeds, contact, and press/partner sections. The brand should feel bold, cultural, and media-driven.

---

## 1) High-level sitemap

* Home
* Field Day (Sub‑section / Brand Vertical)

  * Field Day Landing Page (CMS filtered view)
  * Field Day Article (CMS Template – shared with Articles but tagged "Field Day")
* Shows / Articles (Main CMS Collection Landing)

  * Article (CMS Template)
* About
* Shop (Ecommerce or Shopify embedded)

  * Product (Ecomm Template)
* Press / Partners (static or CMS)
* Contact
* Terms / Privacy / Shipping (static)

---

## 2) Page layouts & components

### Global

* **Header**: left-aligned site title/logo, right-aligned nav (`Home | Shop | About | Contact`). Sticky on scroll? optional. Minimal border-bottom.
* **Footer**: site copyright, small nav, social icons, newsletter signup.
* **Container system**: use 1200px max-width with 16–24px side padding; a fluid container for small screens.

### Home

* **Hero**: large title (site name), subheadline; optional featured article carousel or static hero card.
* **Latest / Grid**: 2–3 column responsive article grid showing cover image, title, excerpt. Use CMS Collection List bound to `Articles` collection.
* **Shop teaser**: 2–3 product cards with CTA to /shop.
* **Social strip**: small embedded videos or social icons.
* **Press logos**: horizontal Scroller or grid.

### Article page (CMS Template)

* Fields used: cover image, title, subtitle/excerpt, publish date, body (rich text), tags, related articles
* Layout: title + meta, cover image full-bleed or inset, article body (rich text block with embedded media), share buttons, show author and tags, related articles carousel.

### Shop

* If using Webflow Ecommerce: product grid with add-to-cart buttons, product detail template, cart UI (mini cart + checkout pages provided by Webflow).
* If embedding Shopify: use Buy Button or link to hosted Shopify checkout. Build product cards with external Checkout CTA (or custom modal with Storefront SDK if you want headless).

### About / Contact

* About: team / mission / press blurb.
* Contact: a form (Webflow form) that posts to Webflow or to Mailgun/Formspree. Add mailto fallback.

---

## 3) Webflow CMS collections

### Collection: Articles

> Field Day will live inside this collection as either:
>
> * A Boolean field: `is_field_day` (true/false), OR
> * A Category field: `vertical` with options: "Noisy Day" and "Field Day" (recommended for scalability).

On the Field Day landing page, filter the Collection List where `vertical = Field Day`.

* `title` — Plain text
* `slug` — Slug (auto)
* `excerpt` — Plain text
* `cover_image` — Image
* `body` — Rich Text
* `publish_date` — Date/Time
* `author` — Reference (to People collection) or plain text
* `tags` — Multi-reference or plain text list
* `featured` — Boolean
* `og_image` — Image (optional)

### Collection: Products` (only if using Webflow Ecommerce, otherwise skip)

* Built-in Webflow ecommerce product model — add `shopify_product_id` as external reference if syncing

### Collection: People (optional)

* `name`, `photo`, `bio`, `role`, social links

### Collection: Press / Partners (optional)

* `name`, `logo`, `url`, `excerpt`

---

## 4) Visual / Style guide

### Typography

* Headline: **Inter / Variable** or *Playfair Display* for a more editorial tone. Sizes:

  * H1 = 40–48px (mobile 28–34px)
  * H2 = 28–32px
  * Body = 16–18px
  * Small = 13–14px

### Colors

* Primary (text): `#111827` (very dark slate)
* Accent / Link: `#000000` (or a single accent color like `#E11D48` if you want subtle color)
* Muted gray: `#6B7280`
* Background: white

### Spacing

* Use consistent vertical rhythm: 16px base, 24px sections, 48px for major breaks.

### Image treatment

* Use large, edge-to-edge hero images for articles. Use `object-fit: cover` and serve optimized images (Webflow will auto-generate sizes).
* Use Webflow’s responsive images and lazy-loading options.

### Buttons & UI

* Minimal outlined buttons for secondary actions, solid for primary. 8px radius, subtle shadow removed for flatter look.

---

## 5) Interactions & microcopy

* Hover underline for article titles.
* Fade-in on scroll for article cards (use simple AOS / Webflow interactions: move up + fade in).
* Newsletter modal or tiny footer form; optional cookie-based frequency limiter.

---

## 6) SEO & Open Graph

* Add meta title/description fields in CMS; populate on article template using CMS fields.
* Create an `og_image` field and use it for `og:image` meta. Webflow automatically builds Open Graph tags in the Page Settings when using CMS fields.
* Create `robots.txt` and `sitemap.xml` (Webflow generates sitemap automatically on paid plans).
* Add structured data (JSON-LD) in the head for Article schema on article pages.

---

## 7) Analytics & Privacy

* Add Google Analytics 4 or use Plausible / Fathom if privacy-first.
* Add cookie consent banner if using GA or tracking; store consent in localStorage.

---

## 8) Social / Embeds

* Embed YouTube/TikTok/Instagram with their embed codes. Use `Embed` component and set `allowfullscreen`.
* To keep pages fast, use lazy-load wrappers for embeds (render placeholder image and only load embed on click).

---

## 9) E-commerce options (choose one)

### Option A — Webflow Ecommerce (Simple & integrated)

* Pros: Native cart, checkout pages, Webflow handles taxes/shipping. Good for low volume stores.
* Cons: Transaction fees if you don’t use Shopify or external gateways; built-in UI is opinionated.
* Steps: enable Ecommerce, add products, style Product Template, configure Payments (Stripe), setup shipping/taxes.

### Option B — Shopify (recommended if you need robust store)

* Pros: Best for inventory, fulfillment, real payments. Use Shopify admin; connect via Buy Button or Storefront API for headless.
* Steps: keep product/catalog in Shopify. For simple approach, copy Buy Button code into Webflow Product Cards or link to Shopify product pages. For headless, use Storefront SDK + custom checkout (advanced).

### Option C — Snipcart + Stripe

* Pros: Lightweight JS cart that works with static sites. Easy to add to buttons.
* Steps: add Snipcart script, set data-item attributes on Add buttons, configure Stripe keys.

---

## 10) Forms & Email

* Use Webflow Forms for contact; send notifications to the team email and also forward to Mailchimp or ConvertKit for newsletter signups.
* Add double-opt-in to mailing list to stay compliant.

---

## 11) CMS editorial workflow

* Use Webflow’s Editor feature for non-dev editing.
* Create a simple CMS guide for editors: title, excerpt, add cover image (set focal point), body paste via rich text, set tags, publish date.
* Use Collections + Reference fields for author attribution.

---

## 12) Accessibility checklist

* Proper semantic HTML (Headings in order), alt attributes for images, keyboard-focus styles, color contrast >= 4.5:1 for text.
* Make sure interactive elements are reachable and forms have labels.

---

## 13) Performance checklist

* Use Webflow image optimization and choose appropriate image sizes.
* Lazy-load non-critical embeds; avoid auto-playing video/audio.
* Use minimal custom JS; prefer native Webflow interactions.

---

## 14) Deployment & hosting

* Host on Webflow (production domain attached). For Shopify headless that needs server functions, use Vercel for any serverless pieces (webhooks) and connect via API keys.
* Use Webflow site settings to add custom domain and configure SSL (automatic) and set favicons/meta.

---

## 15) Estimated time & cost (ballpark)

* Design + Webflow build (static pages + CMS collections + styling): **1–4 days** depending on polish.
* E-commerce setup (Webflow native): **1–2 days**.
* Shopify integration (Buy Button simple): **0.5–1 day**. Headless Shopify: **3–7 days**.
* Typical cost: if hiring a freelancer, **$800–$4,000** depending on scope and design complexity. If in-house or DIY, platform costs: Webflow hosting $18–$200/month depending on plan + transaction fees.

---

## 16) Deliverables I can produce for you right now

* A step-by-step Webflow Editor build checklist (ready to copy/paste into a project task list).
* Exact CMS schema JSON you can paste into a Webflow import template (I can format the fields for manual creation).
* A simple design mockup (responsive frame-level spec) you can hand to a Webflow developer.
* Example embed code snippets (YouTube lazy-load, Shopify Buy Button, Snipcart Add button).

---

## 17) Implementation checklist (copy into a task manager)

1. Create Webflow project and set global styles (fonts, colors, container).
2. Create Collections: Articles, People, Partners.
3. Build global header & footer symbols.
4. Build index page (Hero, Collection List grid, Shop teaser).
5. Build Article Template (bind fields, add share buttons, related items).
6. Connect forms to email / Zapier / Mailchimp.
7. Add SEO / OG field mappings and test share cards.
8. Add shop (choose option), add products & product template.
9. Test payment flow & shipping/taxes.
10. QA: mobile responsiveness, accessibility, performance.
11. Launch: connect domain, set up analytics, privacy/cookie banner.

---

## 18) Notes & trade-offs

* Webflow is fastest for editorial and small-shop workflows. For high-traffic editorial with complex personalization or scale, consider Next.js + headless CMS and CDN.
* Shopify is best for complex products, inventory, and fulfillment; Webflow Ecommerce is fine for small catalogs.

---

If you want any of the **deliverables** from section 16, tell me which one(s) and I’ll produce them now — I can generate the **Webflow CMS field list**, **task checklist formatted as JSON**, **embed snippets**, or a **responsive mockup spec**.
