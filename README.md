# mythnyc — Character Quote Bubble section

This repo was empty, so this adds a single, self-contained Shopify section
rather than editing an existing theme file: `sections/character-quote-bubble.liquid`.

## What it does

Renders your character PNG with a speech bubble next to it. On every page
load (i.e. every refresh) it picks a random line from a quotes list you
manage in the theme customizer and shows it in the bubble.

## Install into your live theme

1. Shopify admin → **Online Store → Themes → Edit code** (on the theme you
   want to update).
2. Under **Sections**, click **Add a new section**, name it
   `character-quote-bubble`, and paste in the contents of
   `sections/character-quote-bubble.liquid`.
   - If you use Shopify's GitHub integration to connect this repo directly to
     a theme, just merge/copy this file into your theme repo's `sections/`
     folder instead.
3. Go to **Online Store → Themes → Customize**, open the **Home page**.
4. Click **Add section**, choose **Character Quote Bubble**.
5. In the section settings:
   - Upload your **Character image** (your PNG). Use **Character position on
     page** (left/center/right) to place it within the section, and the
     **Character horizontal/vertical nudge** sliders to fine-tune its exact
     position — the speech bubble stays anchored to the character and moves
     with it.
   - Optionally upload a **Speech bubble image**. If you leave it blank, a
     simple rounded bubble is drawn with CSS using the color settings below
     it (with a little tail pointing at the character). Use **Bubble width**
     and **Bubble height** to resize it — an uploaded bubble image scales to
     fit inside that box without distorting; the drawn bubble treats height
     as a minimum and grows for longer quotes.
   - Set **Bubble position** (top-left/top-right of the character) and
     nudge it into place with the offset sliders.
   - Under **Text**, pick a **Quote font** from your theme's font library,
     set **Quote font size**, **Text alignment**, and nudge the quote's
     exact position inside the bubble with the horizontal/vertical offset
     sliders (useful for centering it just right on an uploaded bubble
     image).
   - Edit the **Quotes** field — one quote per line. Add as many as you
     like; a random one is chosen each time the page loads.
6. Save.

## How the randomization works

The quotes are rendered into a small inline JSON `<script>` tag, and a tiny
inline script picks `quotes[Math.floor(Math.random() * quotes.length)]` and
writes it into the bubble's text element on page load. No external JS file,
no app, no extra network request — it reruns on every full page load, which
covers a manual refresh and normal Shopify navigation (Shopify's default
Online Store theme does full page loads on navigation).

## Notes / limitations

- This picks a new quote per page load, not truly "per session" — navigating
  to another page and back will show a (possibly different) random quote
  again, same as a refresh. If you'd rather it stay the same across an
  entire visit, that needs `sessionStorage` instead of picking fresh every
  load — say the word and this can be swapped in.
- Everything is scoped to the section's own generated id, so you can safely
  add more than one instance of the section to a page without style/JS
  collisions.
- If your theme uses a click-to-navigate "instant page"/prefetch feature
  that swaps content without a full reload, the script re-runs whenever this
  section's markup is (re)inserted into the DOM — for the stock Shopify
  Online Store theme this isn't a concern.
