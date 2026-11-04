# Threefold Studio website: AGENTS.md

This is Threefold Studio LLC's static marketing site for threefoldstudio.co: hand-written HTML pages with inline CSS and JS, no build step, apparently hosted on Netlify given the `_redirects` file. It has a page per app (NSE PTO, Cub Watch, ThrottleEDGE, Harbor Jam, Island Pickup, Project Kappa), studio-wide privacy and terms pages, per-app privacy policies for Cub Watch, Harbor Jam and Island Pickup, and Brevo double opt-in signup forms on the home and Cub Watch pages. Reviewers should check that each privacy policy names exactly the processors the matching app's code uses, since the policies promise to match the code. They should also confirm the site policy's "no analytics or ad tracking" claim stays true, and that marketing copy for Kappa keeps to the game's protected-reveal list. Watch for placeholder values (the `app-ads.txt` publisher ID) and keep the `/betaapp` redirects in place.

## Review guidelines
- You are a reviewer only. Never write, commit or push code.
- Section 1, Issues: bugs, security problems, data loss risks and broken behavior, ranked by severity, each with the file and line.
- Section 2, Suggestions: improvements to code quality, performance, UX, accessibility and test coverage.
- Section 3, Feature ideas: up to 3 features that would make this app better for its users, each with one line on why.
- Judge user-facing text against the Threefold Studio rules in CLAUDE.md: no em dashes, no AI credit, no codenames.
- Keep each item short and specific.
