# Opt-In Funnel — The 27-Point Marketing Checklist

A complete, deployable 2-page opt-in funnel. Static HTML, no build step, no dependencies.

Built from the `optin-funnel` skill's templates in this repo, with the placeholders
filled in and a working form handler added.

## Pages

| Path | File | Purpose |
|---|---|---|
| `/` | `index.html` | Squeeze page — headline, benefits, email capture |
| `/thank-you` | `thank-you.html` | Confirmation + delivers the lead magnet |
| `/checklist` | `checklist.html` | The lead magnet itself (printable to PDF) |
| `/privacy` | `privacy.html` | Placeholder privacy policy |

Flow: `/` → submit email → `/thank-you` → `/checklist`

## Deploying to Vercel

This funnel lives in a subdirectory, so Vercel needs to be pointed at it:

1. Import the repo in Vercel.
2. Set **Root Directory** to `funnel-optin`.
3. Framework Preset: **Other**. Leave build and output settings empty.
4. Deploy.

`vercel.json` sets `cleanUrls`, which is what makes `/thank-you` work without the
`.html` extension. Keep it.

## Collecting emails for real

Out of the box the form runs in **demo mode**: it validates the address and
redirects to the thank-you page, but stores nothing. A warning is logged to the
console so this is never silently mistaken for a working list.

To start collecting, open `index.html`, find this line near the bottom, and set it:

```js
var ENDPOINT = "";
```

Any endpoint accepting a JSON `POST` of `{ "email": "..." }` works:

- **Formspree** — `https://formspree.io/f/xxxxxxxx`
- **ConvertKit** — `https://app.convertkit.com/forms/xxxxxxx/subscriptions`

On a non-2xx response the form re-enables and shows an error rather than
dropping the address silently.

## Before running paid traffic

- Replace `privacy.html` with a real policy. The current one is a generic
  starter and explicitly says so.
- The "Join 2,400+ subscribers" social proof is carried over from the template.
  **Make it true or remove it.**
- Add analytics — no tracking is installed.
