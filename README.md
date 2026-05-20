# Napster Microsoft Marketplace Offer — Landing Page

A self-contained HTML landing page introducing Napster's Microsoft Marketplace credit offer. Designed to live at `napster.com/marketplace-offer` (or similar) and drive subscriptions to the Napster Omniagent API on Microsoft Marketplace.

## Files

| File | What it is |
|------|------------|
| `index.html` | The landing page. Single self-contained HTML file with all CSS inlined. |
| `README.md` | This file. |

## Preview

Open `index.html` in any browser. No build step, no dependencies — fonts (Avantt → Poppins fallback) and the Napster logo load from CDNs.

To host as a preview link via GitHub Pages, push to a public repo, enable Pages in repo settings (Source: `main`, Folder: `/ (root)`), and it'll live at `https://<username>.github.io/<repo>/`.

## Page sections

1. **Hero** — Pink-gradient "$300 in credits" highlight, single CTA "Subscribe on Marketplace."
2. **How it works** — Tabbed module with three steps (subscribe → credits activate → use over 3 months); clicking each tab swaps the active panel showing a large heading, description, and supporting visual.
3. **What you get** — Three benefit cards with custom inline SVG icons.
4. **Who's eligible** — Three gradient-backdrop cards with line-icon, number label, and criterion. A "Read full terms & conditions" link opens the terms in a lightbox.
5. **Footer** — Mirrors napster.com structure.

The user journey is entirely outbound: the page sends users to Microsoft Marketplace via the Subscribe CTA. Credits are applied automatically once the subscription is verified on the back end — no registration form, no form fields, no HubSpot integration required.

## Design notes

- **Typography**: Avantt is the primary face per the Napster brand guide. The page declares it first in the font stack; Poppins (the brand-approved Google Fonts alternative) loads as the fallback so the mockup renders correctly out of the box. On the live napster.com page, drop in the licensed Avantt `@font-face` rules and the page will use them automatically.
- **Color palette**: Jet Black (#000000), Napster Mulberry (#1A0918), Napster Pink (#BE369D), Napster Neon gradient (#FFA1F3 → #EA2DD2). All sourced from the Napster brand guide.
- **Nav**: Rendered as an inline SVG so the layout is pixel-locked across browsers. Only the Napster logo region is clickable (links to napster.com). Replace with the live napster.com Webflow nav at integration time if preferred.
- **Footer**: A standalone footer modeled after napster.com. Remove at integration time so the Webflow site shell provides the real footer.

## Terms & conditions lightbox

The full T&C copy lives inside a hidden modal (`#np-terms-modal`) that opens when "Read full terms & conditions" is clicked. Close with the × button, click outside, or press Escape. **Run the legal copy through Napster Legal before launch** — it's currently paraphrased.

## What's not in the mockup

- Avantt webfont files (licensed; drop into `@font-face` at integration time).
- Real T&C wording cleared by Napster Legal.
- Production Webflow nav and footer (the mockup includes its own approximations).
- Tracking — add Google Analytics, Microsoft Clarity, or whatever Napster uses, plus UTM-aware outbound link tracking on the "Subscribe on Marketplace" CTA so the team can attribute conversions.
