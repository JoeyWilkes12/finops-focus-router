# FinOps FOCUS — QR Code Router

A stable public address for **FOCUS Explorer**, Joey Wilkes's FinOps FOCUS application. Visitors follow a portfolio link or scan a QR code, open this router, and continue to the application's current website.

The router lets you **print, laminate, and distribute a QR code, then maintain its destination in one place.** If FOCUS Explorer moves to a different URL or hosting provider, update the router while keeping existing links and the address encoded in the QR code unchanged.

## Why use a router?

Portfolio links and printed materials can outlast an application's hosting arrangement. A stable entry point helps keep them useful:

- **Preserve shared materials.** QR codes that encode the router address can continue to work after a destination change without reprinting or redistribution.
- **Centralize updates.** One destination setting updates every portfolio link and QR code that points to the router.
- **Support future moves.** FOCUS Explorer can be maintained and hosted independently of its public entry point.

These benefits depend on preserving the router URL and keeping its GitHub Pages publication available.

## Routing

```mermaid
flowchart LR
    Entry[Portfolio link or QR code] --> Router[Stable FinOps FOCUS router URL]
    Router --> App[Current FOCUS Explorer website]
```

| Address | URL |
| --- | --- |
| **Share or encode in the QR code** | [https://joeywilkes12.github.io/finops-focus-router/](https://joeywilkes12.github.io/finops-focus-router/) |
| Current application destination | [https://finops-focus-jwilkes.vercel.app/](https://finops-focus-jwilkes.vercel.app/) |

The included [PNG](finops-focus-router-qr.png) and [SVG](finops-focus-router-qr.svg) QR assets encode the stable router address. Keep the white border around the code when printing or placing it in a design. Regenerate these assets only if the router address itself changes.

## Implementation

This repository contains a small static HTML router. GitHub Pages processes its Jekyll/Liquid templates so one `redirect_url` setting in [index.html](index.html) supplies the navigation and metadata URLs.

- **JavaScript** uses `window.location.replace(...)` to navigate without adding the router page to browser history.
- An **HTML meta refresh** forwards visitors when JavaScript is disabled.
- A **manual link** provides a way to continue if automatic navigation does not occur.
- The canonical link and structured metadata use the same destination setting.

The router is served as an HTTP 200 page; navigation happens in the browser rather than through an HTTP 301/302 response. It has no application backend or database. FOCUS Explorer is hosted separately.

## Deployment

GitHub Pages publishes this repository with the following configuration:

| Setting | Value |
| --- | --- |
| Publishing branch | `main` |
| Publishing folder | `/` (repository root) |
| Rendering | GitHub Pages with Jekyll/Liquid |
| Router source | [index.html](index.html) |

Changes merged into `main` are published by GitHub Pages. Keep `.nojekyll` absent so the URL substitutions run. Opening the source HTML directly does not process the templates; use a rendered preview for validation.

## Changing the destination

1. Confirm the replacement application URL is published and accessible.
2. Create a feature branch from `main` and update only the `redirect_url` value at the top of `index.html`. Use an absolute HTTPS URL in double quotes:

   ```yaml
   redirect_url: "https://finops-focus-jwilkes.vercel.app/"
   ```

3. Update the current destination in this README and run the checks described in [MAINTENANCE.md](MAINTENANCE.md).
4. Open a pull request against `main` for review. Obtain the repository owner's approval before merging.
5. After GitHub Pages finishes deploying, verify the public router and scan a QR code to confirm both reach the new destination.

Keep the repository name, Pages address, and QR assets unchanged when moving the application. The [maintenance guide](MAINTENANCE.md) covers local previews, link and browser checks, publication verification, and rollback.
