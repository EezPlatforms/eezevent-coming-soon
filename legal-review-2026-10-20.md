# Launch policy review — October 20, 2026

Scope: Vendor Agreement and Privacy Policy HTML and Markdown on `feature/launch-party-2026-content`, with source checks against the current mobile and services `dev` branches. This is a product/source consistency review and proposed drafting update, not a determination that every jurisdictional or store obligation has been satisfied. No policy was published, no app/backend was changed, and no branch was merged.

## Findings and changes

1. **Markdown contradicted the current HTML.** The old vendor Markdown treated subscriptions as future functionality. The privacy Markdown omitted store purchase records and audit-vault retention, included an unqualified no-sale statement, and described different geographic availability. Both Markdown copies are now synchronized with the complete HTML articles, preserving the newer subscription, paid-discovery, contact-masking, event opt-out, and deletion disclosures.
2. **Reviews and vendor responses were missing.** Added service-specific reviews for eligible completed inquiries, owner responses, author editing where available, public display, reporting by email, and conduct rules against fabricated reviews, sentiment-conditioned incentives, retaliation, and suppression of honest negative reviews. Paid placement does not buy ratings or remove criticism.
3. **Review privacy was missing.** Added collected rating/comment/response data and account/inquiry/service links; public first-name/last-initial display, dates and aggregates; review notifications; and a warning against publishing confidential information. The backend changes profile identifiers on account deletion but does not delete review text or vendor responses, so the policy does not promise that it does.
4. **Location disclosures were too general.** Added entered/saved addresses and ZIPs, service radii, coordinates and approximate ZIP-derived locations. The inspected discovery flow does not require live device GPS access.
5. **Website-provider requests were not explained.** Added GitHub Pages, Google Fonts requests, and off-site Evite, maps and store links. This does not introduce analytics or new trackers.
6. **Change notices and privacy choices needed clarification.** Added material-change notice/required consent language and conditional statutory opt-out/appeal/agent request guidance through support. No unsupported response deadline or claim of universal legal applicability is added.
7. **Versioning and navigation were stale.** Proposed launch effective date is October 21, 2026; version `2026-10-21` appears in both formats. The two legal-page headers now link to launch details using the existing design.

## Implementation evidence

- `eezevent-services/app/reviews/service.py` and `schemas.py`: completed-inquiry eligibility, one review per inquiry, author editing, business-owner responses, first-name/last-initial author display, service aggregates, and vendor notifications.
- `eezevent-mobileapp/src/components/VendorReviews.js`: ratings, comments, author/date display, author edit action and owner response editor.
- `eezevent-services/app/auth/account_deletion_service.py`: replaced profile identifiers; encrypted original identity/business/service snapshots; retained review text; no review purge in the inspected deletion routine. An encrypted identity vault is not irreversible anonymization.
- `eezevent-services/docs/vendor-geographic-discovery.md`: saved/entered coordinates and ZIP centroids, service-level radii, distance matching and no external geocoding during ZIP search.
- Mobile `package.json` and `app.json`: current dependencies and permissions; no new analytics SDK identified in these files. These files alone are not a complete production data inventory.
- Existing policy HTML and September 28 review: subscription benefits, trials, downgrade restriction, purchase metadata, event opt-out decisions and known retention questions were preserved.
- Website source: GitHub Pages setup, Google-hosted font requests and external links.

## Items the document changes cannot resolve

- **Retention implementation remains unresolved.** The inspected audit-vault writes do not set an expiry. Confirm necessary fields, access restrictions, purpose-specific retention periods/review, and actual purge handling for originals, review content, files, logs and backups. No invented 30/90-day erasure promise was added. The existing retention-purpose statements are not proof that an operational schedule exists.
- **Paid event discovery still requires a state-law assessment.** The policy describes paid Pro discovery and event controls without reinstating an unverified no-sale assertion. Applicability, classification, any required opt-out mechanisms/signals, and request/appeal operations must be assessed against actual markets and data flows.
- **Draft adoption must be coordinated with app legal versions.** On release, serve matching policy text and version through the backend legal-document endpoints and preserve existing acceptance records. Deliver required change notices/acceptance prompts. Changing this website branch does not update the app's server-delivered policies, configure stores, or prove production review/opt-out behavior.
- **Existing dispute provisions need professional review.** Arbitration, liability limits and mandatory local rights remain as already drafted; they were not redesigned in this product-content update.
- **Store declarations need reconciliation.** Compare purchase history, publicly displayed reviews, location-derived data, and retained data with the actual App Store privacy and Google Data Safety submissions. Hosting source does not establish current production declarations.

## Primary references checked

- [FTC Consumer Reviews and Testimonials Rule — Questions and Answers](https://www.ftc.gov/business-guidance/resources/consumer-reviews-testimonials-rule-questions-answers): fake reviews, sentiment-conditioned incentives and suppression.
- [Apple App Review Guidelines](https://developer.apple.com/app-store/review/guidelines/): subscription information and privacy disclosures/retention/deletion.
- [Google Play User Data policy](https://support.google.com/googleplay/android-developer/answer/10144311?hl=en): accurate privacy disclosures, retention/deletion and third-party data handling.

## Verification

- Both HTML documents parse with balanced structure, one H1 and valid local links/assets.
- Markdown article text and links match the HTML versions; date/version match.
- Original subscription and audit-vault disclosures remain in both formats.
- `git diff --check` passes. Existing legal-page CSS and responsive layout are retained; visual browser review remains unavailable in this environment.
