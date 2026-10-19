# UGO Project Domain Redirects

Redirect configuration for the `ugoproject.org` domain, served by Cloudflare Pages.

## What it does

`ugoproject.org` and `www.ugoproject.org` redirect (301) to the UGO page on euroteamoutreach.org: <https://euroteamoutreach.org/ugo/>.

Only the root path redirects. Deep paths (`ugoproject.org/anything`) return 404 by design; there is no wildcard (splat) rule.

The entire configuration is the one-line [`_redirects`](_redirects) file, in [Cloudflare Pages redirects syntax](https://developers.cloudflare.com/pages/configuration/redirects/).

## How it's deployed

- **Cloudflare Pages project:** `ugoproject-redirects`, connected to this repo via the Cloudflare GitHub integration.
- **Production branch:** `main`. No build command; Pages publishes the repo contents as-is.
- **Custom domains:** `ugoproject.org` and `www.ugoproject.org`, attached to the Pages project.

There is no manual deploy step. Every push to `main` deploys automatically in about 20 seconds.

In the Cloudflare dashboard: **Workers & Pages → ugoproject-redirects** (Deployments, Custom domains, Settings → Build).

## Changing the redirect target

1. Edit the URL in `_redirects`.
2. Commit and push to `main`.
3. Verify (below).

## Verifying a deploy

- The commit on GitHub gets a **Cloudflare Pages** check. "Deploy successful" means it's live, and the check's Details link opens the deployment in the dashboard.
- `curl -sI https://ugoproject.org | grep -i location` prints the current target.
- In a browser, test in a private/incognito window. Browsers save 301 redirects, so a normal window can keep showing the old target after a successful deploy.
