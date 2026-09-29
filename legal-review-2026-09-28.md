# EezEvent subscription and privacy review

Review date: September 28, 2026. Draft for business and qualified counsel review; not a legal opinion or store-compliance certification.

## Scope and conclusion

Reviewed the local Markdown agreements, their public-facing HTML counterparts, website links, mobile subscription screen and legal URLs, backend subscription models and plan definitions, subscription documentation, and lead-response fields. The agreements dated August 5, 2026 do not adequately describe the current subscription implementation. Revise before releasing the updated paid offering. No published documents were changed by this review.

This was a source review, not a test of deployed behavior or an inspection of App Store Connect/Play Console. Actual prices, offer eligibility, production configuration, privacy labels, retention operations, distribution countries, and applicable statutory thresholds remain unverified.

## Confirmed product baseline

| Item | Current source behavior |
|---|---|
| Basic | Monthly; one owned business, multiple services, profiles/catalog, incoming inquiries, messaging, calendar/availability |
| Pro | Monthly; up to three owned businesses, Basic features, delegated business/service teams, search priority, local event leads/outreach |
| Subscriber | Vendor owner; not a separate subscription per business or team member |
| Customers and teams | Customers do not need a vendor subscription; delegated members depend on the owner's Pro entitlement |
| Trial | Documentation and UI advertise six months; store configuration and individual eligibility need verification |
| Downgrade | Scheduled Pro benefits persist until the effective change; team/outreach access then becomes restricted; retained records are not automatically deleted |
| Search | Pro boost follows exact-name matching and eligibility filters; not a guaranteed first position or quality endorsement |

Evidence: `eezevent-services/app/subscriptions/plans.py`, `app/subscriptions/models.py`, `docs/vendor-subscriptions.md`, and `eezevent-mobileapp/src/screens/VendorSubscriptionScreen.js`.

## Findings and required revisions

### 1. High: vendor subscription contract is missing

Vendor Agreement §6 and its HTML equivalent describe paid subscriptions as a future possibility. Replace that paragraph with current terms covering plan benefits/limits, monthly renewal, store billing, eligible trial conversion, cancellation, refunds, changes of plan, expiration, restoration, pricing changes and notice. Separate EezEvent subscription charges from payments between vendors and customers; the latter remain outside the platform according to the reviewed materials.

Do not promise another trial on upgrade, a particular proration method across both stores, a permanent free tier, automatic deletion of excess businesses, or guaranteed lead volume. Explain consequences for owners with more than one business when moving to Basic. The documentation identifies a transition decision for existing over-limit accounts; resolve it before drafting a definitive promise.

Apple requires clear subscription information; Google specifically addresses price, trial conversion and cancellation disclosures. These must appear in the purchase experience, not only in a linked agreement. Sources: [Apple review guidelines, §3.1.2](https://developer.apple.com/app-store/review/guidelines/), [Google subscriptions policy](https://support.google.com/googleplay/android-developer/answer/9900533?hl=en).

### 2. High: privacy policy omits subscription processing

Privacy Policy §§1.5 and 3, including HTML, say the app does not offer/process payments. This is misleading for paid app subscriptions even though Apple/Google handle payment credentials. Replace with a distinction between store-billed subscriptions and external vendor/customer payments.

Add the data actually processed: account association, plan/product/provider, transaction/order identifiers, original transaction identifiers, Google purchase tokens, trial/billing dates, renewal status, pending plan changes, store environment and verification responses. The model also stores `raw_provider_payload`; inventory and minimize its contents rather than assume it contains identifiers only. Explain verification, entitlement management, restoration, support, security and recordkeeping purposes; Apple/Google exchanges; and retention criteria.

Reconcile the revised policy with App Store privacy disclosures and Google Data Safety, particularly purchase history and account linkage. Do not infer that store billing eliminates purchase-data collection. [Google User Data policy](https://support.google.com/googleplay/android-developer/answer/10144311?hl=en).

### 3. High: paid lead discovery exposes client contact data before engagement

`eezevent-services/app/outreach/router_outreach.py:140` onward returns event description, location ZIP, dates, guest count and budget, plus client name, email and phone. The response permits no existing outreach record. Privacy Policy §4.1 describes sharing largely in connection with an inquiry, outreach response or interaction; this is insufficiently explicit about discovery before that interaction.

Describe which eligible vendors/team members can discover each data category, when visibility starts, its purpose and actual user controls. Consider withholding direct contact details until the client accepts engagement and using in-app outreach first. A policy edit alone does not resolve unexpected or excessive disclosure.

Because Pro is paid access to identifiable leads, counsel must assess whether this arrangement falls within a statutory sale/sharing definition wherever applicable. Do not automatically label it a sale, but do not reaffirm the categorical no-sale statement without examining applicable laws, thresholds, exceptions and the actual exchange. Subscription revenue alone does not settle that analysis.

### 4. High: unconditional trial copy and inadequate purchase links

The subscription screen always displays “6 months free,” including a fallback without a numerical renewal price. Show the actual eligible offer and localized recurring price; provide an ordinary paid-subscription presentation for ineligible users. Apple's introductory offer is generally available once per subscription group. [Apple introductory-offer guidance](https://developer.apple.com/help/app-store-connect/manage-subscriptions/set-up-introductory-offers-for-auto-renewable-subscriptions).

The iOS text says payment is charged at confirmation, which needs qualification when a free trial applies. The Terms of Use link is hardcoded to Apple's standard EULA on both operating systems. Add EezEvent's applicable Vendor Agreement/subscription terms on both platforms; retain the Apple EULA where appropriate for iOS licensing. Apple's EULA is not a replacement for EezEvent's commercial terms.

No direct store subscription-management link was found in the inspected purchase/profile screens. Add an easily accessible management/cancellation action and verify the complete app flow. Google expressly requires an easy online cancellation route in the app. [Google subscriptions policy](https://support.google.com/googleplay/android-developer/answer/9900533?hl=en).

### 5. High: distinguish deletion, cancellation and retention

Privacy §5 and Vendor Agreement §12 do not explain that deleting the app/account does not itself cancel store billing. Add a warning and store-management link in the deletion flow. Do not force users to wait for subscription expiry to delete an account. Verify deletion for every account role, not only clients/vendor owners.

Replace broad retention permissions with defined categories, purposes and periods or meaningful criteria. Retaining team records after downgrade is different from retaining personal data after account deletion. Verify foreign-key handling and necessary subscription records before promising erasure or restoration. Sources: [Apple account deletion guidance](https://developer.apple.com/support/offering-account-deletion-in-your-app/), [Google account deletion requirements](https://support.google.com/googleplay/android-developer/answer/13327111?hl=en). Google's external deletion pathway and submitted URL also need verification; a generic help page should not be assumed sufficient.

### 6. Medium: customer-facing commercial disclosures

Customer Terms §4.1 should explain that a paid Pro plan can affect search position and that “Promoted” is not verification or endorsement. Vendor §7 can disclaim guaranteed position while still acknowledging the purchased boost. Customer §5 should distinguish current vendor subscriptions from any future customer charges, rather than suggest all subscriptions are future functionality.

### 7. Medium: agreement structure, assent and general clauses

`agreements/terms&conditions.md` is a short drafting placeholder, not completed terms. The website actually links Customer Terms and Vendor Agreement. Choose that role-specific structure or adopt unified terms; define precedence and avoid conflicting entire-agreement clauses. Keep HTML, Markdown and backend-delivered legal versions synchronized; the mobile app also has remote legal-document loading.

Vendor §14 and Customer §15 measure the liability cap using sums paid “directly” to EezEvent. Clarify whether amounts paid through app stores count. Counsel should review the cap, exclusions and mandatory-rights carve-outs.

The arbitration clauses lack procedural detail. Review applicable AAA rules, fees, small-claims access, venue, consumer rights, severability and assent. An opt-out is a potential drafting choice, not a universal requirement. Continued use alone should not be assumed sufficient to bind users to material new charges or dispute terms. Preserve versioned affirmative acceptance and give appropriate advance notice of changes.

For applicable consumer contracts, [North Carolina §75-41](https://www3.ncleg.gov/EnactedLegislation/Statutes/HTML/BySection/Chapter_75/GS_75-41.html) addresses conspicuous renewal/cancellation disclosure and changed terms. Its notice provision for renewals exceeding 60 days should not automatically be applied to a monthly renewal merely because the introductory trial lasts six months. Review other jurisdictions based on launch markets; North Carolina governing law does not settle all mandatory local rights.

Privacy §13's broad no-reliance disclaimer belongs in commercial terms, not as a qualification of privacy commitments. Narrow Vendor §8's marketing license so private messages/contracts are not treated like public promotional content. Confirm the no-tracking claims, permission descriptions, international-transfer disclosures and rights procedures against real practices and markets.

## Proposed drafting language

These are working clauses, not a complete replacement agreement. Confirm the implementation and business decisions above before adoption.

**Vendor subscriptions:** “EezEvent offers Basic and Pro monthly subscriptions to vendor account owners. Basic supports one owned business. Pro supports up to three owned businesses and includes business and service team access, priority placement in relevant searches, and eligible local event leads and outreach. Team members do not need a separate subscription to work for an eligible Pro business. Pro placement does not guarantee a particular position, lead, booking or revenue and is not an endorsement of service quality.”

**Billing and trial:** “The applicable store displays the price, currency, billing period and any introductory offer before you confirm your purchase. Trial offers are available only to eligible subscribers under the displayed offer and store rules. Unless canceled by the applicable deadline, a trial converts to a paid monthly subscription and the subscription renews automatically at the disclosed price. Manage or cancel through the Apple or Google account used to purchase. Plan-change timing, charges, credits and any trial effect are governed by the applicable store's disclosed terms. Price changes are subject to required notice and consent.”

**Refunds and deletion:** “Cancellation ordinarily stops future renewal; it does not itself refund charges already incurred. Refund eligibility is subject to the applicable store process and mandatory legal rights. Deleting EezEvent or your EezEvent account does not itself cancel a store subscription. Cancel separately through your purchasing store account to stop future billing. Account deletion remains available independently of subscription expiration.”

**Subscription privacy:** “Apple or Google processes payment for subscriptions purchased through its store. EezEvent receives and stores subscription information linked to your EezEvent account, including the purchased plan and product, transaction identifiers or purchase tokens, trial and billing dates, renewal status, plan changes, and store verification information. We use this information to verify purchases, provide and restore subscription access, manage plan limits, respond to support requests, prevent misuse, and maintain necessary records. We exchange subscription verification information with the relevant store. EezEvent does not receive your full payment-card number through these store subscription flows.”

The last sentence describes the inspected subscription integration only; confirm other payment/support collection paths before publishing. Draft lead-sharing language only after deciding which contact fields should remain visible and confirming client controls.

## Completion checklist

1. Confirm live Basic/Pro prices, six-month offer setup, eligible users, markets, cancellation and refund operations.
2. Decide over-limit downgrade behavior and notice to existing Basic team users; source documentation says team restrictions take effect on deployment.
3. Resolve lead visibility and the no-sale representation with counsel.
4. Revise Vendor Agreement, Privacy Policy and targeted Customer Terms sections; synchronize HTML and backend legal versions, date and acceptance records.
5. Fix trial display, EezEvent terms links and cancellation/deletion flows; reconcile store privacy declarations.
6. Validate actual store purchases, trial ineligibility, plan changes and deletion with active subscriptions before release.

Additional configuration discrepancy: subscription documentation lists Basic `eezevent.vendor.basic.monthly`, but current mobile/backend constants use `eezevent.vendor.basic.monthly.new`. Confirm store setup and legacy subscription handling; do not treat documentation as evidence of the live offer.

## Confirmed outreach decision after review

The owner confirmed that client details must be withheld until the client responds to vendor outreach, and that clients have no separate outreach opt-out setting. The three HTML drafts now describe that intended behavior while preserving mandatory privacy rights. The previously inspected backend response exposes contact fields without requiring a response; implementation must be reconciled before publishing this promise. Confirm whether a decline/not-interested action qualifies as a response before implementing the release condition. Paid discovery of event information still requires the previously identified privacy-law assessment; this decision alone does not resolve the no-sale representation.

## Confirmed downgrade decision after review

On an effective Pro-to-Basic downgrade, the vendor must select one business to keep active and make all other businesses inactive. All inquiry access is blocked until only one active business remains, including inquiries for the business to be retained. The Vendor Agreement HTML now states this rule. Verify that backend eligibility counts active businesses and that vendors retain access to business-deactivation controls while inquiry access is blocked. This decision supersedes the earlier open question about excess-business treatment; no application code was changed by this document update.

## Deletion implementation and planned event opt-out

The owner reports immediate anonymization. Inspection of `eezevent-services/app/auth/account_deletion_service.py` confirms immediate replacement of profile identifiers, but also encrypted retention of original identity fields in `DeletedAccountAuditVault`, plus an email hash and linked user reference. Vendor deletion additionally retains business/service snapshots. The model has an optional `retained_until`; the inspected creation paths do not populate it. Full irreversible anonymization must not be claimed on this evidence. The privacy HTML draft now describes the distinction. Confirm the vault's necessity, specific lawful purposes, access limits and enforced expiry, and separately inventory messages, attachments, events, logs and backups.

The owner is willing to add an event-creation outreach opt-out. This is a planned control, not verified functionality. Recommended behavior: opting out excludes the event from vendor lead discovery and prevents new unsolicited outreach; provide the same control on existing events. Determine treatment of existing conversations and previously disclosed data. Update the current no-opt-out text in both HTML agreements when the design is confirmed and before releasing the feature. A creation-only control must not be assumed to satisfy all applicable statutory opt-out rights. The no-sale representation still requires assessment; neither contact masking nor a toggle alone establishes compliance.

## Confirmed event opt-out and retention purposes

The owner confirmed event opt-out on creation and editing: hide opted-out events from Pro discovery and prevent new unsolicited outreach. The three HTML drafts now reflect that behavior, superseding the previous no-opt-out wording. Verify backend enforcement before publication; existing conversations and the response-versus-decline contact-release rule still need clarification.

The owner identified referential integrity, disputes and fraud investigation as retention purposes. Privacy draft distinguishes records with replaced identifiers from recoverable encrypted originals. Referential integrity alone does not establish a need to preserve original contact details. No retention duration, purge job or access policy has been verified. Unqualified no-sale statements were removed pending applicable state-law assessment; removing those statements and providing an event toggle do not themselves complete that assessment or all required rights mechanisms. Confirmed six-month eligible trials and USA availability are now reflected in the HTML.
