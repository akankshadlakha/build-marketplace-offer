# Napster Microsoft Marketplace Offer — Landing Page

A self-contained HTML mockup of the landing page introducing Napster's Microsoft Marketplace credit offer. Designed to live at `napster.com/marketplace-offer` (or similar) and capture registrations into HubSpot.

## Files

| File | What it is |
|------|------------|
| `napster-marketplace-offer.html` | The landing page. Single self-contained HTML file with all CSS inlined and the registration form ready to be wired to HubSpot. |
| `README.md` | This file. |

## Preview

Open `napster-marketplace-offer.html` in any browser. No build step, no dependencies — fonts (Avantt → Poppins fallback) and icons load from CDNs.

To host as a quick preview link via GitHub Pages, rename `napster-marketplace-offer.html` → `index.html`, push to a public repo, enable Pages in repo settings, and it'll live at `https://<username>.github.io/<repo>/`.

## Design notes

- **Typography**: Avantt is the primary face per the Napster brand guide. The page declares it first in the font stack; Poppins (the brand-approved Google Fonts alternative) is loaded as the fallback so the mockup renders correctly out of the box. When the production page is built on `napster.com`, drop in the licensed Avantt `@font-face` rules and the page will use them automatically.
- **Color palette**: Jet Black (#000000), Napster Mulberry (#1A0918), Napster Pink (#BE369D), Napster Neon gradient (#FFA1F3 → #EA2DD2). All sourced from the Napster brand guide.
- **Nav**: Rendered as an inline SVG so its layout is pixel-locked across browsers. Only the Napster logo region is clickable (links to napster.com). Replace with the live napster.com Webflow nav at integration time if preferred.
- **Footer**: A standalone footer modeled after napster.com. Remove this at integration time so the Webflow site shell provides the real footer.

## Wiring the form to HubSpot

The form section uses an embed target. Replace the static fallback markup with HubSpot's embed code:

1. In HubSpot, go to **Marketing → Lead Capture → Forms** and create a new form.
2. Add fields matching the static form in the HTML:
   - First Name *
   - Last Name *
   - Email * (helper text: "Use your Azure account email")
   - Company Name *
   - Country * (single-line text or dropdown)
   - Marketplace Subscription ID * (create this as a custom contact property first, in **Settings → Properties**, type Single-line text)
3. Set submission behavior to **show an inline thank-you message** (so the page doesn't navigate away from the offer context).
4. Publish the form, click **Share → Embed code**, and copy the three values: `region` (e.g. `na1`), `portalId`, and `formId`.
5. In `napster-marketplace-offer.html`, find the block that starts with `<!-- HUBSPOT FORM EMBED -->`.
6. **Delete** the `<form class="np-form-fallback">…</form>` inside `#hubspotForm`.
7. **Uncomment** the `<script>` block right below it and paste the three values into the `hbspt.forms.create({...})` call.
8. Save. The embedded HubSpot form will render into `#hubspotForm`, and the CSS already targets HubSpot's generated classes (`.hs-form-field`, `.hs-form-required`, `.hs_submit input[type=submit]`) so it inherits the Napster look — dark inputs, pink focus rings, gradient submit button.

### Recommended HubSpot setup

- **Workflow**: Trigger on form submission to assign the contact to a "Microsoft Marketplace Offer" list and notify whoever validates eligibility. They'll cross-reference the Marketplace Subscription ID against Microsoft Partner Center reports before credits are issued.
- **Hidden fields**: Add hidden UTM source/medium/campaign fields to attribute traffic. HubSpot auto-populates these from URL parameters when marked as hidden.
- **reCAPTCHA**: Turn on the form's spam filter — the offer ID + email combination is a high-value target.
- **GDPR**: Enable explicit consent checkboxes in HubSpot's GDPR settings if targeting EU traffic.

## Page sections

1. **Hero** — Pink-gradient "$300 in credits" highlight, two CTAs (Subscribe on Marketplace / Register your offer).
2. **How it works + Form** — Combined two-column section: four numbered steps on the left, registration form on the right.
3. **What you get** — Three benefit cards with custom inline SVG icons.
4. **Who's eligible** — Three gradient-backdrop cards with line-icon, number label, and criterion. A "Read full terms & conditions" link opens the terms in a lightbox.
5. **Footer** — Mirrors napster.com structure.

## Terms & conditions lightbox

The full T&C copy lives inside a hidden modal (`#np-terms-modal`) that opens when "Read full terms & conditions" is clicked. Close with the × button, click outside, or press Escape. **Run the legal copy through Napster Legal before launch** — it's currently paraphrased.

## What's not in the mockup

- Avantt webfont files (licensed; drop into `@font-face` at integration time).
- Live HubSpot portal/form IDs (placeholder script is commented out).
- Real T&C wording cleared by Napster Legal.
- Production Webflow nav and footer (mockup includes its own approximations).
