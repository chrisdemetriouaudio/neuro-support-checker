# Neuro Support Checker

A free UK directory of about 900 support organisations for autism, ADHD, dyslexia, learning disability, Down syndrome, brain injury and related conditions. It re-checks every listing by itself, every 1 to 3 days.

**Live:** https://neurosupport.labs.chrisdemetriou.com

## The problem

Support directories go out of date. A family is pointed at a group that closed a year ago, and nobody finds out until the phone number is dead.

## What I built

- **A directory that checks itself.** A scheduled job visits each organisation's website and suggests a status.
- **A live check for anyone.** Paste a website on the home page and get an answer in seconds.
- **A person decides every closure.** The job only raises a flag. An admin closes a listing.
- **Finds new groups.** It reads the UK charity registers for all four nations and checks each group is still registered.
- **Display settings.** Text size, a dyslexia-friendly font, spacing, high contrast, a reading mask and dark mode.

## What it spots

- The web address no longer exists.
- The site is down 3 times in a week.
- "We have closed" wording on the page.
- Parked or for-sale domains.
- A move to a new domain.

Every listing carries one status: Looks active, Needs a check, Likely closed (hidden from the directory), Closed (only by a person) or Confirmed (by the organisation).

## How it works

| Where | What runs there |
|---|---|
| **In the browser** | The directory, the live check and the display settings |
| **Cloudflare Worker** | Serves the directory, runs live checks and postcode look-ups, and holds the passkey admin |
| **Cloudflare D1** | Approved admins and the audit log |
| **GitHub Actions** | The daily job: visits sites, rebuilds the directory, posts new flags to a review issue |

The checker is polite. It makes one visit a day per site, names itself in its user agent, and follows `robots.txt`.

## Run it

Needs Node 22.18 or newer.

```bash
npm ci
npm run check    # typecheck and tests
npm run checks   # visit every site and rewrite the outputs
```

## Where things are

| Folder | What |
|---|---|
| `src/` | The checker, the register look-ups and the page builder |
| `worker/` | The Cloudflare Worker and the passkey admin |
| `test/` | The tests (`npm test`) |
| `data/` | The organisations and each check's result |
| `.github/workflows/` | CI, the daily check and the search for new groups |
| `NeuroSupport-PMO/` | Project notes: plan, decisions and changelog (an Obsidian vault) |

## How this was built

I design the solution and direct AI coding tools to build it. I test it, and nothing ships until I sign it off.
