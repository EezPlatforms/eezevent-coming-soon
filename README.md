# EezEvent Website

Static home, product overview, and support site for GitHub Pages deployment with custom domain `eezevent.com`.

## Files

- `index.html` home page, launch party details, RSVP, and getting started
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


## October 21, 2026 launch update

The launch content is prepared on `feature/launch-party-2026-content`. Review and merge through your normal process; publishing is not part of this change. Neither `main` nor `dev` is updated by this feature branch.

- Party: Wednesday, October 21, 2026, 6:30–8:30 PM Eastern, 7000 Tea Olive Road, Marvin, NC 28173. RSVP uses the existing Evite invitation.
- Existing fonts, brand color tokens, logo, imagery, and card patterns are retained.
- Plan descriptions follow the current Vendor Agreement. Prices and trial eligibility are shown by the purchasing store rather than hardcoded into the website.
- Store buttons link to verified public EezEvent listings: Apple App Store ID `6774633058` and Google Play package `com.eezevent.app` (checked October 20, 2026).
- Review help describes the completed-inquiry flow present on the mobile app's `dev` branch and qualifies actions by availability. Confirm the reviews backend migrations and app release are deployed before advertising reviews more broadly.
- After the party, replace the dated invitation and RSVP calls to action with evergreen product content. The page intentionally uses the full date instead of a relative “tomorrow” label.

Before publishing, open all three pages at phone and desktop widths, follow navigation and fragment links, check the RSVP and directions, and verify store access on a phone. Hosting configuration is unchanged. Customer Terms, Vendor Agreement, and Privacy Policy updates are documented in [the October 20 review](./legal-review-2026-10-20.md).
