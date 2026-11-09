# Production web login handoff

## Approved destination

- Production webapp origin: https://web.eezevent.com (confirmed in `eezevent-webapp/.github/workflows/deploy-prod.yml`).
- Login route: `/login` (confirmed in `eezevent-webapp/src/app/login/page.jsx`).
- Intended marketing-site login destination: https://web.eezevent.com/login.

## Verification gate

Live DNS/HTTPS resolution for `web.eezevent.com` could not be confirmed from the execution environment on 2026-11-08. **Do not publish the Login navigation item until this gate passes.**

1. Confirm DNS resolves and TLS certificate is valid for `web.eezevent.com`.
2. Open `https://web.eezevent.com/login` in a browser and confirm a successful page load without a redirect loop.
3. Test Google and Apple sign-in for Host and Business accounts, including callback/redirect settings and backend CORS.
4. Confirm post-login navigation and logout; test on mobile and desktop.
5. Once verified, add a visible `Login` anchor to the `topbar-actions` navigation in `index.html` and `marketing.html` with `href="https://web.eezevent.com/login"`. Keep the marketing site separate from the webapp authentication implementation.

This feature branch intentionally contains approved marketing copy but **does not expose an unverified Login link**. No changes to main or production are included.
