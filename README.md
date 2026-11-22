# BetaNYC Pages template

A starting point for a one-page BetaNYC site on GitHub Pages: what a project is, why it exists, and a chart people can link to. It follows the look of BetaNYC's MCP sites ([mta-mcp](https://betanyc.github.io/mta-mcp/), [nyc-311-mcp](https://betanyc.github.io/nyc-311-mcp/)) and BetaNYC's brand colors.

There is no build step. The site is plain HTML, one stylesheet and one small script, served from `docs/`.

## Use it

**New repo:** click **Use this template** on GitHub.

**Existing repo:** copy the `docs/` folder into it.

Then:

1. In `docs/index.html`, change every line marked `REPLACE`. Search for the word; nothing should be left.
2. Edit the text in `docs/assets/social-card.html`, open it in a browser at exactly 1200 × 630, and save a screenshot as `docs/assets/og-image.png`. With Playwright:
   ```sh
   npx playwright screenshot --viewport-size=1200,630 docs/assets/social-card.html docs/assets/og-image.png
   ```
3. In the repo's **Settings → Pages**, publish from the `main` branch, `/docs` folder. The site appears at `https://betanyc.github.io/<repo>/`.
4. Put that address in the repo's **About** box (the "Website" field).

## What is in it

| File | What it is |
|---|---|
| `docs/index.html` | The page: top bar, opening section, number tiles, a shareable figure, an About section and the footer |
| `docs/assets/site.css` | Shared styles. Copy it as is, so it can be updated across sites; put page-specific styles in the page. |
| `docs/assets/nav.js` | The **Menu** button (burger) on the right of the top bar below 782px wide, as on BetaNYC's other sites. Copy it as is. |
| `docs/assets/share.js` | Keeps a chart's view (a precinct, a year) in the page address, and wires the **Copy link** buttons |
| `docs/assets/social-card.html` | The picture social sites show when the link is posted |
| `docs/assets/favicon.svg`, `betanyc-wordmark-*.svg` | BetaNYC logos, from the brand guide |
| `docs/.nojekyll` | Tells GitHub Pages to serve the files as they are |

## Shareable charts

Every view of a chart should have its own address, so someone can post exactly what they are looking at:

```
https://betanyc.github.io/<repo>/?precinct=034#coverage
```

`share.js` reads and writes those query parameters, and a **Copy link** button copies the current view with the figure's anchor. Social sites build their preview from the page's Open Graph tags, not from the query, so every view shares one preview card. Say which view it is in the post itself.

## Rules every site keeps

- **Name the data source** on the page: publisher, dataset and link, next to the chart and in the footer.
- **Say whether BetaNYC changed the data.** If it changed in any way, say so and say how. Link the official record.
- **Footer line:** "built by BetaNYC, a project of the Fund for the City of New York," with links to the source code and the issues page.
- **Accessible by default:** keep the skip link, alt text on every image, a text table or summary beside every chart, and the focus outline.
- **Works on a phone:** test at 375 px wide. Wide tables and charts scroll inside their own box, never the page.
- **Links to files, never to folders.** GitHub Pages serves `docs/guide.html`, not `docs/guide/`.

## Accessibility

The page aims for WCAG 2.2 AA. On 2026-11-22 it had no failures in [axe](https://github.com/dequelabs/axe-core) 4.10 at 390px and 1200px wide, with the menu open and closed. What is built in:

- A skip link, and page regions screen readers can jump between: the top bar is the `<header>`, the links are a `<nav>`, and everything from the opening section on is in `<main>`.
- The **Menu** button reports whether it is open (`aria-expanded`), closes on Escape, and works by keyboard. Every link and button shows an orange focus ring.
- Text colors pass 4.5:1 contrast. Tap targets in the phone menu are at least 44px tall.
- Smooth scrolling is turned off for people who set their device to reduce motion.
- A chart area that can be wider than the screen can take keyboard focus, so it can be scrolled with arrow keys.

What each site still has to do:

- Give every chart a text alternative: a summary in its caption and, where it helps, the numbers as a table.
- Replace the chart area's `aria-label` with the chart's title.
- Keep the shapes and colors that carry meaning in a chart at 3:1 contrast or better against the page, or say the same thing another way (a pattern, a label, the table).
- Run axe on the finished page before launch.

## License

MIT. See `LICENSE`. The BetaNYC logos are BetaNYC's marks and are not covered by the MIT license.
