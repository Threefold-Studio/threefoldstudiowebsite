# Threefold Studio website: CLAUDE.md

## App

### What it is
The public marketing website for Threefold Studio LLC ("Everyday apps for everyday people."), served at threefoldstudio.co. It lists the studio's published and upcoming apps with a page per app, hosts per-app privacy policies, collects email signups for launch news, and links the studio's social accounts. Audience is prospective app users and anyone looking for the studio's contact or legal pages.

### Stack
- Plain static HTML with inline CSS and small inline scripts (countdown timers). No build step, no package.json, no framework.
- Fonts from Google Fonts (fonts.googleapis.com / fonts.gstatic.com).
- Brevo (sibforms.com) embedded signup forms with `https://sibforms.com/forms/end-form/build/main.js`.
- Images in `assets/`; `favicon.ico`, `favicon-32.png`, `apple-touch-icon.png`, `social-share.png`.

### Repo
- Folder on this clone: `/home/user/threefoldstudiowebsite`.
- Local folder on Seth's computer: CONFIRM: not stated in repo.
- GitHub remote: https://github.com/Threefold-Studio/threefoldstudiowebsite (HTTPS, public repo per brief).
- Default branch: `main` (origin/HEAD -> origin/main).

### Bundle IDs
- Not applicable (website). Domain: `threefoldstudio.co` (canonical and og:image URLs in the HTML; policies say "the website threefoldstudio.co").
- App IDs referenced on the site: NSE PTO App Store `id6816827500`, Google Play `co.threefoldstudio.nsepto`.

### Backend
- None. No Supabase. Email list handled by Brevo.
- Hosting: `_redirects` file in Netlify syntax (`/betaapp /cubwatch 301`, `/betaapp/* /cubwatch/:splat 301`) suggests Netlify. CONFIRM: host is Netlify (no netlify.toml or other host config in repo), and how deploys are triggered (likely push to `main`).

### Monetization
- None on the site itself. Privacy policy: "We do not currently use analytics or advertising tracking tools". No ads on the site.
- `app-ads.txt` exists for the apps' AdMob inventory but contains a placeholder publisher ID: `google.com, pub-XXXXXXXXXXXXXXXX, DIRECT, f08c47fec0942fa0`. CONFIRM: real AdMob publisher ID.

### Third-party services
- Brevo (Sendinblue SAS): mailing list signup forms on `/` and `/cubwatch` (account form host `63321165.sibforms.com`), double opt-in with `thank-you.html` / `confirmed.html` and `cubwatch/thank-you.html` / `cubwatch/confirmed.html`. Named as processor in the site privacy policy.
- Google Fonts: web fonts.
- Hosting provider: unnamed in policy ("standard website hosting infrastructure"); see Backend.
- Social links: X, Instagram, TikTok, Reddit `@threefoldapps` (`/links`); ThrottleEDGE has its own X, Reddit, Instagram.
- No analytics, no forms other than Brevo signup. Contact is a `mailto:hello@threefoldstudio.co` link.

Pages and the apps they cover:
- `/` home: About, app cards, "Also built" websites (The Design Ward, links to https://thedesignward.co), signup, countdowns.
- `/nsepto`: NSE PTO, "Out now on iOS and Android" for North Smyrna Elementary parents; privacy and terms hosted at nsepto.com/privacy and nsepto.com/terms; support at nsepto.com/support.
- `/cubwatch` (+ `/cubwatch/privacy`, thank-you, confirmed): Cub Watch, "launches December 1" (2026); one-time Pro purchase, 7 day trial.
- `/throttleedge`: ThrottleEDGE(TM), "Launching January 1, 2027", links throttleedge.com; "Safety features are always free", optional subscription.
- `/harborjam` (+ `/harborjam/privacy`): Harbor Jam, in development.
- `/islandpickup` (+ `/islandpickup/privacy`): Island Pickup, in development.
- `/kappa`: Project Kappa, in development, "Working title".
- `/privacy`, `/terms`: site-only policies (effective August 6, 2026; Terms governed by Delaware law).
- `/links`: link-in-bio page.

Processors named in privacy policies:
- Site (`/privacy`): Brevo; unnamed web host.
- Cub Watch (`/cubwatch/privacy`, updated October 9, 2026): Apple iCloud (CloudKit) for optional Household sharing; Apple App Store (StoreKit) and Google Play Billing for Pro; states no analytics, ads, crash reporting or servers.
- Harbor Jam (`/harborjam/privacy`, November 1, 2026): Supabase, Sign in with Apple / Google Sign-In, Google AdMob (with Google UMP consent), RevenueCat, Google Firebase Cloud Messaging, Google Fonts.
- Island Pickup (`/islandpickup/privacy`, November 1, 2026): Supabase, Google AdMob (with UMP), RevenueCat, Sign in with Apple / Google Sign-In, Google Fonts (no FCM listed).

### Commands
- No build, test or lint commands in repo. Local preview (inferred): `python3 -m http.server` from the repo root.
- Deploy: CONFIRM: presumably push to `main` with Netlify auto-deploy (inferred from `_redirects`).

### Current version
- Not versioned. Latest commit: "Harbor Jam and Island Pickup privacy policies: ads through AdMob, in-app purchases through RevenueCat; updated 2026-11-01".

### Locked decisions and rules
- Keep the `/betaapp` redirects "until the Brevo double opt-in redirect URLs are updated, and ideally leave them in place permanently for any old links already shared" (`_redirects`).
- Site policy "covers the Threefold Studio website only"; each app has its own separate privacy policy linked from that app's page (`privacy/index.html`).
- "We do not sell your personal information." and no analytics or ad tracking on the Site; "If this changes, we will update this policy." (`privacy/index.html`).
- App policies state they are "written to match what the app's code actually does. Nothing here describes a feature the app does not have." and that anything new will be described "before the version that adds it ships" (cubwatch, harborjam, islandpickup privacy pages).
- Kappa page: "Kappa is a placeholder ... this page will change when it does. Nothing is lost in the meantime, old links will keep working." (`kappa/index.html`).
- ThrottleEDGE: "Safety features are always free." Cub Watch Pro: "one time purchase, never a subscription" (app pages).
- No other rules files (no README, no CLAUDE.md) in repo.

## Threefold Studio rules (apply to every repo)

### Git and review
- Never push to main. Work on a branch, open a pull request, and never merge without Seth's explicit approval, except under the standing approval below.
- Standing approval (Seth, 7 Nov 2026): when ChatGPT Codex finishes reviewing a PR's latest commit with no findings, and the repo's own checks pass, Claude may merge that PR without waiting for Seth, then start the Codemagic TestFlight build (when set up) (and the Play internal build once Android is set up). Still wait for Seth when: the PR needs SQL that has not been run yet (a website merge deploys at once); Codex left any finding, until it is fixed and a fresh Codex review is clean; or the step is an App Store or Google Play production submission. Say in chat what was merged and built.
- Commits are authored Seth A. Ward Sr. <admin@threefoldstudio.co>. Never add a Co-Authored-By line for Claude, and never add any Claude or AI trailer to commits or PR descriptions.
- SQL and Edge Functions (Seth, 7 Nov 2026): when a Supabase access token is saved on this environment (when set up), Claude runs migrations and deploys Edge Functions itself. Do not paste the SQL in chat first; say in one or two lines what is being changed, then run it, then report the result. Anything that deletes data (DELETE, TRUNCATE, DROP TABLE or DROP COLUMN on a table with rows, removing storage objects) waits for Seth: say in plain words what would be deleted and run it only after he says okay. Dropping a constraint, index, trigger or function deletes no data. Without a token, give Seth the SQL to paste in full.
- Stage files by path. Do not use git add -A.
- One commit per change, with a clear message.
- Pull the branch's latest before working on it. Retry pulls and pushes only for network errors.
- Never force-push or rewrite history on a shared branch; bring changes in with a merge.
- Remotes are HTTPS, never SSH.
- Never commit secrets: .env files, .p8, .jks, .keystore, key.properties, service-role keys. Publishable keys are fine.
- Before every commit run this repo's own checks (analyze, tests, lint, typecheck, build, whichever exist). Work is not done while any of them fails.

### Handling ChatGPT Codex reviews
- Codex reviews every pull request and may post bugs, suggestions and feature ideas. You make the final call on each.
- Bugs and security issues: verify each one, fix the real ones, and reply on the PR with the reason for any you decline. A fresh clean review is needed before merging under the standing approval.
- Suggestions: apply the ones that clearly improve the app within the PR's scope. Decline the rest with a one-line reason.
- Feature ideas: decide which are worth doing, but never build them in the same PR. Add the ones you would keep to docs/IDEAS.md with Codex's reason and your verdict. Build only after Seth approves.

### Shipped output
- Never credit Claude or any AI anywhere that ships. The byline is "Built by Threefold Studio".
- Never put Seth's real name in shipped output.
- No em dashes in any user-facing text. Marketing and website copy uses no dashes as punctuation at all. Code comments are fine.
- Greek-letter codenames are internal only and never appear in user-facing text. App names are not published until Seth clears each one.
- Every app ships on iOS and Android.
- Privacy policies name processors specifically (Supabase, Twilio, Firebase, Brevo, Netlify, Apple, Google). When a live policy is rewritten, keep the original effective date and change only the last updated date.

### Versioning
- MAJOR.MINOR.PATCH+BUILD. Every new build raises the build number.
- The version stays the same across test builds (TestFlight, Play testing tracks (when set up)) until that version is released to the public. The first build after a release raises the version.
- Build numbers never reset, are never reused, and are never date stamps. An uploaded build that was never released is still spent. iOS and Android share one build counter.

### Images
- Images are made in ChatGPT and attached to the session. Put them in the assets folder and register them in pubspec.yaml when needed.
- For anything posted publicly, strip ChatGPT's C2PA metadata by rebuilding the PNG with only the IHDR, IDAT and IEND chunks.

### How to respond to Seth
- Order every reply: bottom line up front, open questions he must answer, the detail he needs, then numbered steps in true execution order with prerequisites placed where they happen.
- One terminal command per code block, in run order. Send a cd once, then relative paths.
- Anything he must copy and paste goes in the chat in full, in its own block. Never point him at a file.
- Prefer tables for comparisons. Keep it direct.
- Seth is on US Eastern time. Run TZ=America/New_York date before saying today, tomorrow or any elapsed time.
