# EezEvent Website

Static home, product overview, and support site for GitHub Pages deployment with custom domain `eezevent.com`.

## Files

- `index.html` vendor-first home page, five pillars, plans, FAQs, and download/setup guidance
- `marketing.html` features, audiences, and Basic/Pro overview
- `help.html` onboarding, workflow help, subscriptions, and reviews
- `styles.css` brand styling (mobile app palette)
- `CNAME` custom domain config (`eezevent.com`)
- `.nojekyll` disables Jekyll processing

## Deploy To GitHub Pages

1. Create a new repository, for example `eezevent-coming-soon`.
2. Copy contents of this folder into the repository root.
3. Push to `main`.
4. In GitHub:
   - `Settings` -> `Pages`
   - `Source`: `Deploy from a branch`
   - `Branch`: `main` and `/ (root)`
5. Wait for Pages to publish.

## Connect `eezevent.com` (GoDaddy DNS)

Use these records on your domain:

- `A` record: host `@` -> `185.199.108.153`
- `A` record: host `@` -> `185.199.109.153`
- `A` record: host `@` -> `185.199.110.153`
- `A` record: host `@` -> `185.199.111.153`
- `CNAME` record: host `www` -> `<your-github-username>.github.io`

Then in GitHub Pages settings:

1. Set custom domain to `eezevent.com`.
2. Enable `Enforce HTTPS` after DNS resolves.

## Local Preview

Open `index.html` directly, or run:

```bash
cd coming-soon-site
python3 -m http.server 8080
```


## Post-launch website — October 22, 2026

Prepared on `feature/post-launch-website`, based on the merged launch update. No deployment or merge is included.

- Vendor-first homepage: business challenges, five launch-deck pillars, inquiry-to-booking walkthrough, Basic/Pro, client/host secondary section, FAQs, downloads and setup.
- Pillar names: Discover & Connect; Capture & Convert; Plan & Organize; Communicate & Collaborate; Track, Analyze & Grow. Document storage is emphasized under Plan & Organize. Growth copy describes current dashboard/status visibility, not future analytics or guaranteed outcomes.
- Product overview provides deeper feature details and working setup-guide links for each pillar.
- Existing blue/indigo tokens, typography, logo and card layouts remain. The existing dashboard asset is labeled as an illustrative preview with sample data; no performance statistics are presented as customer results.
- All public navigation uses download/setup calls to action instead of the completed launch party. Legal article text, policy versions, and effective dates are unchanged by this update; only their header navigation changes.
- Store links: Apple App Store ID `6774633058`; Google Play package `com.eezevent.app`. Both SVG QR codes encode these exact HTTPS links with a four-module quiet zone. QR generation requires no client-side code or third-party QR service.
- Plan descriptions follow the current Vendor Agreement. The purchasing store remains authoritative for localized pricing, trial eligibility, and renewal terms.
- No new analytics, forms, trackers, JavaScript framework or runtime dependency. FAQs use native HTML disclosure controls.

## Review before publishing

Open home, features and help at phone and desktop widths. Check store/QR links, FAQ disclosure controls, section navigation and policy-header download links. Scan the codes with a physical phone. Hosting configuration is unchanged.

The policy review remains in [legal-review-2026-10-20.md](./legal-review-2026-10-20.md); this website content update does not resolve backend retention, release or policy-acceptance operations.
