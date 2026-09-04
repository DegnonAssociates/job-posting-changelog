# Changelog

All notable features, updates, fixes, security hardening, infrastructure work, tests, and documentation changes to this app are tracked here in reverse chronological order.

Dates are based on the repository git history. Entries are grouped by development milestone so the progress of the job posting platform can be followed from the current state back to the initial build.

## 2026-09-04

### Added

- Added Canadian provinces and territories to the company location selector, grouped separately from U.S. states.

## 2026-09-03

### Added

- Grant the local `ADMIN` role during MemberClicks login when the issued OAuth token contains the exact `ROLE_ADMIN` authority, while preserving existing roles and preventing duplicates.

### Security

- Moved MemberClicks profile synchronization into the server-side OAuth callback and disabled the legacy public token-bearing synchronization route.

### Tests

- Added regression coverage for MemberClicks authority parsing, role merging, new and existing users, concurrent synchronization, profile failures, callback sessions, and the disabled legacy route.

## 2026-08-25

### Updated

- Updated Next.js from `16.2.11` to `16.3.3` and refreshed its locked image-processing dependencies.

## 2026-08-21

### Added

- Added a tenant-aware Neon CRM SSO flow with signed, expiring OAuth transactions, safe post-login redirects, Neon profile synchronization, and signed application sessions.

### Security

- Restricted Neon CRM login initiation to same-origin requests and validated callback state, tenant, origin, and transaction expiry before authenticating users.

### Tests

- Added coverage for Neon OAuth response parsing, transaction signing, authentication exchange, account synchronization, and route behavior.

## 2026-08-14

### Fixed

- Fixed the first MemberClicks SSO login attempt redirecting to the internal `localhost:8080` address by building the SSO state redirect from the proxy-aware public request origin.
- Preserved safe post-login destinations while rejecting external redirect targets during SSO state initialization.

### Tests

- Added regression coverage for public-origin redirects behind a reverse proxy and unsafe external `next` destinations.

## 2026-08-13

### Added

- Added this changelog to document the app's development history from the initial commit through the current codebase.
- Structured the log in reverse chronological order with dated sections and categorized notes for features, updates, bugfixes, security, tests, docs, and infrastructure.

## 2026-07

### Updated

- Updated Next.js to `16.2.11`, keeping the application framework current with later security and compatibility releases.
- Refined email copy across the job posting and payment workflows.
- Added a payment button to the My Content area so users can continue or complete payment from their own content dashboard.
- Updated email form handling to use `useActionState`, aligning the email-related UI with the app's current React action patterns.
- Resized logos in job and company views to improve consistency and prevent awkward image presentation.

### Added

- Added an admin resend email button so administrators can resend job-related emails from the admin workflow.
- Added stricter email validation checks around resend behavior to reduce invalid or unsafe resend attempts.

## 2026-06

### Added

- Added backend edit logging for job changes so administrative edits can be audited.
- Added a removal date picker to the job editing workflow, giving admins more direct control over expiration timing.
- Added payment attempt records when payment verification runs, improving traceability for attempted payments.
- Reimplemented the payment verification flow after earlier simplification, restoring explicit verification while keeping direct payment publishing behavior where appropriate.
- Added payment verification notifications and supporting application logic.
- Added maintenance/service offline handling through a dedicated service offline gate.

### Updated

- Refined edit tracking and removal date behavior after the first edit-log implementation.
- Updated Prisma schema and migrations to support edit tracking, posted date display, payment verification, payment attempts, and related database changes.
- Restored direct payment publishing after the first payment verification removal, then brought verification back with a revised implementation.
- Set `original_id` to `0` for new job submissions to clarify the difference between new postings and renewal-derived postings.
- Updated job posting form wording.
- Improved tenant-aware dashboard links and authentication redirects.
- Removed noisy runtime logging after production troubleshooting.
- Removed the old Coolify deployment workflow after deployment strategy changes.
- Updated and locked build dependencies, including Next.js security updates and `esbuild` compatibility for Railway builds.

### Fixed

- Fixed high-risk security findings identified in the security review.
- Fixed tenant-aware auth redirects and dashboard links.
- Fixed optimized image failures for company logos by avoiding Next.js optimization paths that could break remote or tenant-specific logo assets.
- Fixed dynamic route behavior by awaiting route params before querying.
- Fixed TypeScript and build issues related to dependency and framework updates.

### Security

- Secured auth cookies.
- Added stronger admin tenant checks so admin actions remain scoped to the correct organization instance.
- Applied framework and dependency security updates.

## 2026-05

### Added

- Added a configurable admin dashboard and updated the app to use instance-level configuration.
- Added a posted date display toggle so tenants can control whether posted dates appear.
- Added instance-specific rich text instructions with proper HTML rendering.
- Added enhanced admin approval flow capabilities, including edit and preview behavior during review.
- Added a service offline maintenance gate.
- Added newest jobs stabilization work and an expiration cron endpoint.
- Added debugging for newest job logo rendering while diagnosing asset issues.

### Updated

- Applied the first round of SDBP-specific app edits.
- Updated text on company pages for SDBP requirements.
- Made company descriptions optional.
- Updated approval flow behavior and merged approval-related improvements.
- Updated rich text instruction handling.
- Updated application configuration patterns for tenant-specific display and admin settings.

### Fixed

- Fixed the MemberClicks SSO login flow.
- Fixed newest job logo rendering by bypassing image optimization where needed.
- Stabilized newest jobs ordering and display.

## 2026-04

### Added

- Added scheduled renewal reminder emails.
- Added visibility into sent renewal reminder emails so renewal communication can be reviewed.
- Added a conditional Create Account button.
- Added auto-deploy support for Coolify before later deployment changes removed the workflow.

### Updated

- Documented cron setup for renewal reminder and job expiration tasks in the README.

## 2026-03

### Added

- Added an instructions dashboard page.
- Added a default login redirect.
- Added expiration date display to My Content so users can see when their postings expire.
- Added company editing to both content and admin dashboards.
- Added expanded unit test coverage for payment flows and server actions.
- Added a payment porting guide for abstracting payment behavior.

### Updated

- Updated removal date handling and included active records that do not have an associated account.
- Ordered newest jobs by removal date.
- Removed posted date display from job listing and detail views before the later configurable toggle was introduced.

### Fixed

- Fixed admin company pagination.
- Fixed instance scoping in admin company views.

## 2026-02

### Added

- Added rich text editing in phases, including editor extensions, extension cleanup, and rollout of the richer editing experience.
- Added lazy loading for job cards and related loading skeleton updates.
- Added stacked card layouts and hover state enhancements for the landing page job display.
- Added filtering-based job discovery to replace the earlier posting search behavior.

### Updated

- Tweaked HTML rendering in job postings.
- Updated job card layouts for fixed height and long-title ellipsis handling.
- Updated logo sizing on the entry page and aligned entry page logo behavior with the sidebar logo.
- Simplified the dark mode switcher.
- Moved login/logout to the last menu position regardless of which navigation options are visible.
- Updated login/logout wording.
- Made jobs viewable without requiring login.
- Made both featured sections conditional so they only display when content exists.
- Updated Contact Us section visibility.

### Fixed

- Fixed a Load More bug in job filtering.
- Fixed job card rounded corner clipping.
- Fixed skeleton presentation for differing job card states.

## 2026-01

### Added

- Added pricing rules for job postings and renewals.
- Added pending and awaiting payment status filters to the admin table.
- Added additional admin table filtering and created-date filtering.
- Added transaction ID handling in payment status logging and payment routes.
- Added login redirects back to the payment page for users who start payment while logged out.

### Updated

- Updated pricing rule logic and fixed TypeScript errors in pricing rules.
- Touched up admin, posting, company, and job card views.
- Updated job card ordering.
- Added an instance-level choice for company logo fallback behavior.
- Made `created_ts` optional to support backfill and legacy data handling.
- Updated posting and renewal routes to use `{TRANSACTION_ID}`.

### Fixed

- Fixed transaction ID return behavior.
- Improved long job title handling while keeping card heights consistent.

## 2025-12

### Added

- Added instance-based favicons and dynamic favicon handling.
- Added the instance logo as a placeholder on additional pages.
- Added on-the-fly company logo image sizing.
- Added instance logo fallback behavior for job images.

### Updated

- Removed unused badge features and all badge references from forms, emails, and related UI.
- Removed resume UI surfacing from My Content.
- Updated job card sliders to fill the viewport rather than showing only three cards at a time.
- Improved favicon production behavior after logging and diagnosis.

## 2025-11

### Added

- Added a resume upload switcher.

### Updated

- Updated navigation links.

## 2025-10

### Added

- Added an improved job posting flow that supports admin approval before payment.
- Added renewal and initial posting length configuration.
- Added a login text variable for tenant-specific login page messaging.
- Added dashboard empty states for sections without content.
- Added a state dropdown to job/company flows.
- Added sanitization for HTML tags in legacy job descriptions.
- Added renewal route support and data import work.
- Added sender configuration so both email flows can use `instance.email_address`.
- Added a reusable `sendMail.tsx` framework for email work.

### Updated

- Abstracted the public checkout key.
- Updated the renewal flow and renewal public checkout behavior.
- Updated resume actions to use the current logged-in user.
- Removed the image from the login page.
- Fixed logo and login text display.
- Improved no-logo display handling.
- Refined login behavior when using `original_id`.
- Continued `original_id` handling updates for initial versus renewal posting relationships.

## 2025-09

### Added

- Added renewal route support and data import work.
- Added sanitization for legacy HTML job descriptions.

## 2025-08

### Added

- Added a transaction table to the Prisma schema.
- Added documentation comparing initial posting and renewal behavior.

### Fixed

- Fixed renewal form population for fields that were not carrying over correctly.

## 2025-07

### Added

- Added job renewal options.
- Added a developer walkthrough document.
- Added tenant/instance configuration support.
- Added initial Payscape payment setup and later expanded the flow with amount and SKU payload details.
- Added production logging while diagnosing domain, host, and instance lookup issues.

### Updated

- Updated Payscape SKU handling, payment flow behavior, and processing URL configuration.
- Updated middleware for tenant detection and instance handling.
- Moved deployment toward `inetpub`.
- Cleaned up the tenant flow after initial implementation.
- Updated SKU data type.

### Fixed

- Fixed TypeScript build errors.
- Fixed build issues after payment and instance configuration changes.
- Removed Prisma from middleware edge functions to avoid edge runtime incompatibility.
- Fixed bugs discovered during tenant and payment rollout.

## 2025-06

### Added

- Added MemberClicks authentication completion work.
- Added initial Payscape setup.
- Added instance configuration groundwork.

### Updated

- Updated authentication implementation.
- Updated package configuration and deployment setup for Coolify.

### Fixed

- Fixed build issues during authentication and payment rollout.

## 2025-05

### Added

- Added a non-SSO login flow.

### Updated

- Removed the Neon login flow.

## 2025-04

### Added

- Added a seed script for database setup.

### Security

- Locked down the dashboard so only logged-in users can access protected areas.

## 2025-03

### Added

- Added initial emails to job posters and admins.
- Added an approval button to the job posting admin section.

## 2025-02

### Added

- Added an admin page.
- Added dark mode.
- Added admin role authentication.
- Added payment flow work and completed credit card form implementation.
- Added type definitions and updated the content component.

### Updated

- Updated radio group styles.
- Removed the Neon API version from fetch headers.
- Resolved pnpm and build issues during payment implementation.

### Fixed

- Fixed multiple build issues during the payment rollout.

## 2024-11

### Added

- Added S3 uploads for resumes and company logos.
- Added a My Content section backed by real user data.
- Added search functionality.
- Added file upload support.

### Updated

- Restructured actions.
- Updated content and search components.

## 2024-10

### Added

- Added job cards for each main page display type.
- Added dummy images for early UI development.
- Added company information routes.
- Added different card components and job routes.
- Added the renamed submit job route.
- Added server-side validation for resume upload.
- Added skeleton loading states.
- Added company form, validation, skeleton, and actions.
- Added a job type badge field to the job submission form.
- Added company pages that display jobs belonging to the company.

### Updated

- Moved date formatting helpers into the helpers directory.
- Updated the MemberClicks helper function.
- Removed the export from the Neon route.
- Updated form state handling from `useFormState` to `useActionState` to address React version compatibility.
- Updated job form submission to pull validation errors from the Zod schema.

### Fixed

- Fixed a TypeScript error on the jobs page.
- Fixed TypeScript warnings in action routes.

## 2024-09

### Added

- Created the initial Next.js job posting application.
- Added the first hooks folder.
- Added initial database-backed card display.

### Updated

- Cleaned up the `components/ui` folder.

### Fixed

- Fixed early hook issues, including user role hook behavior.
