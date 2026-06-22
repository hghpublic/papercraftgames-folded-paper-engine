# Codex Plan: Add Prominent FPE Support CTAs to Website

## Goal

Update the Folded Paper Engine website so support options are clear, visible, and tasteful.

Primary support path:

```text
Ko-fi
```

Secondary support path:

```text
GitHub Sponsors
```

Support message:

```text
Fund ongoing FPE maintenance, docs, tutorials, sample projects, and the first official showcase game.
```

Do not implement products/shop content yet. This is only for support/donation visibility.

---

## Known Inputs

Ko-fi URL:

```text
https://ko-fi.com/papercraftgames
```

Ko-fi handle:

```text
papercraftgames
```

Ko-fi floating widget code provided by owner:

```html
<script src='https://storage.ko-fi.com/cdn/scripts/overlay-widget.js'></script>
<script>
  kofiWidgetOverlay.draw('papercraftgames', {
    'type': 'floating-chat',
    'floating-chat.donateButton.text': 'Support Us',
    'floating-chat.donateButton.background-color': '#fcbf47',
    'floating-chat.donateButton.text-color': '#323842'
  });
</script>
```

GitHub Sponsors URL to verify before final commit:

```text
https://github.com/sponsors/papercraftgames
```

Existing repo URL:

```text
https://github.com/papercraftgames/folded-paper-engine
```

---

## CTA Copy

Primary CTA label:

```text
Support FPE
```

Secondary CTA label:

```text
Sponsor on GitHub
```

Support section headline:

```text
Help Keep FPE Free
```

Support section body:

```text
Folded Paper Engine stays free, open-source, and MIT licensed. Support helps fund ongoing maintenance, docs, tutorials, sample projects, and the first official showcase game.
```

Small support prompt for docs/footer:

```text
Using FPE? Support ongoing development, documentation, and showcase projects.
```

---

## Placement Plan

### 1. Header: Add Support FPE button

Files likely affected:

```text
website/index.html
website/blender-panel-docs.html
website/godot-feature-docs.html
website/youtube-tutorials.html
website/docs/*.html
```

Current header has:

```html
Download
```

Add a second button near Download:

```text
Support FPE
```

Behavior:

* Link to Ko-fi.
* Open in new tab.
* Use `target="_blank"` and `rel="noopener noreferrer"`.
* Make it visually distinct, likely orange/gold.
* Keep Download visible. Do not replace Download.

Suggested href:

```text
https://ko-fi.com/papercraftgames?utm_source=fpe_site&utm_medium=header&utm_campaign=fpe_support
```

---

### 2. Home page: Add prominent support section near top

File:

```text
website/index.html
```

Add a new support section after the splash/demo section and before the docs section.

Section should include:

* Headline: `Help Keep FPE Free`
* Body copy from above
* Primary button: `Support FPE` → Ko-fi
* Secondary button: `Sponsor on GitHub` → GitHub Sponsors
* Optional small note:

```text
Ko-fi is the easiest way to support FPE. GitHub Sponsors is available for open-source/dev-focused support.
```

Use existing visual style:

* `.section`
* playful title styling
* large buttons
* existing icons where possible

Suggested icons:

* Ko-fi/Support button can reuse `mug-icon.png`
* GitHub Sponsors button can reuse `github-logo.png`

---

### 3. Download section: Add support reminder

File:

```text
website/index.html
```

Inside or below `#download`, after download buttons, add a small support card:

```text
FPE is free. Support keeps it maintained.
```

Buttons:

* `Support FPE`
* `Sponsor on GitHub`

This catches users at the point of value: when they download.

Keep it smaller than the top support section.

---

### 4. Footer: Make support links visible

Files:

```text
website/index.html
website/blender-panel-docs.html
website/godot-feature-docs.html
website/youtube-tutorials.html
website/docs/*.html
```

Current footer social icons are too subtle for funding.

Add a footer support row above or near the social links:

```text
Support Folded Paper Engine
```

Buttons/links:

```text
Ko-fi
GitHub Sponsors
GitHub Repo
```

Ko-fi should be first.

Do not remove existing GitHub/YouTube/Bluesky icons.

---

### 5. Docs pages: Add subtle support banner

Files:

```text
website/docs/*.html
```

Add a small support banner near the bottom before footer:

```text
Using FPE? Support ongoing development, documentation, and showcase projects.
```

Buttons:

* `Support FPE`
* `Sponsor on GitHub`

Keep it modest. Docs should still feel like docs, not a sales page.

---

## Ko-fi Floating Widget

Add the Ko-fi floating widget, but centralize it.

Preferred implementation:

Create:

```text
website/support-widget.js
```

Implementation idea:

```js
const loadKoFiWidget = () => {
  const script = document.createElement('script');

  script.src = 'https://storage.ko-fi.com/cdn/scripts/overlay-widget.js';
  script.async = true;

  script.addEventListener('load', () => {
    if (window.kofiWidgetOverlay) {
      window.kofiWidgetOverlay.draw('papercraftgames', {
        type: 'floating-chat',
        'floating-chat.donateButton.text': 'Support FPE',
        'floating-chat.donateButton.background-color': '#fcbf47',
        'floating-chat.donateButton.text-color': '#323842'
      });
    }
  });

  document.body.appendChild(script);
};

loadKoFiWidget();
```

Then include it before `</body>`.

Top-level pages:

```html
<script src="./support-widget.js"></script>
```

Docs pages inside `/docs`:

```html
<script src="../support-widget.js"></script>
```

Notes:

* Use `Support FPE`, not `Support Us`.
* The widget is secondary to native site CTAs.
* Site must still work if the external Ko-fi script fails or is blocked.

---

## CSS Plan

File:

```text
website/index.css
```

Add a gold/yellow support button variant:

```css
.gold {
    --button-top-color: #fcbf47;
    --button-bottom-color: #e28903;
    --button-glow-color: #ffda70;
}
```

Add support section/card styles:

```css
.support-section {
    background: linear-gradient(to bottom, #ffc100 0%, #ffe380 100%);
}

.support-card {
    max-width: 900px;
    margin: 0 auto;
    padding: 2em;
    background: rgba(255, 255, 255, 0.25);
    border: 0.125em solid #fff;
    border-radius: 1em;
    box-shadow: var(--basic-shadow);
    text-align: center;
}

.support-card-title {
    font-size: 3em;
    color: #fff;
    text-shadow: var(--title-text-shadow);
    margin-bottom: 0.25em;
}

.support-card-body {
    font-size: 1.5em;
    color: #323842;
    max-width: 780px;
    margin: 0 auto 1.5em auto;
}

.support-actions {
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: center;
    gap: 1em;
    flex-wrap: wrap;
}

.footer-support {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    gap: 1em;
    text-align: center;
}

.footer-support-title {
    color: #fff;
    font-size: 2em;
    text-shadow: var(--title-text-shadow);
}
```

Adjust exact sizing after visual check.

Mobile requirement:

* Support buttons must wrap cleanly.
* Widget must not cover primary content or download buttons.
* Header must not become too crowded.

---

## Tracking / UTM URLs

Use UTM parameters so support clicks can be separated in analytics.

Ko-fi header:

```text
https://ko-fi.com/papercraftgames?utm_source=fpe_site&utm_medium=header&utm_campaign=fpe_support
```

Ko-fi home section:

```text
https://ko-fi.com/papercraftgames?utm_source=fpe_site&utm_medium=home_support_section&utm_campaign=fpe_support
```

Ko-fi download section:

```text
https://ko-fi.com/papercraftgames?utm_source=fpe_site&utm_medium=download_section&utm_campaign=fpe_support
```

Ko-fi footer/docs:

```text
https://ko-fi.com/papercraftgames?utm_source=fpe_site&utm_medium=footer&utm_campaign=fpe_support
```

GitHub Sponsors equivalents:

```text
https://github.com/sponsors/papercraftgames?utm_source=fpe_site&utm_medium=header&utm_campaign=fpe_support
https://github.com/sponsors/papercraftgames?utm_source=fpe_site&utm_medium=home_support_section&utm_campaign=fpe_support
https://github.com/sponsors/papercraftgames?utm_source=fpe_site&utm_medium=download_section&utm_campaign=fpe_support
https://github.com/sponsors/papercraftgames?utm_source=fpe_site&utm_medium=footer&utm_campaign=fpe_support
```

If GitHub rejects or strips UTM params, plain URL is acceptable.

---

## SEO / Trust Notes

Add support language without making the site feel needy.

Avoid:

```text
Please donate
We need money
Help us survive
```

Use:

```text
Support ongoing FPE development
Help keep FPE free and maintained
Fund docs, tutorials, sample projects, and showcase games
```

Keep the MIT/FOSS promise visible:

```text
FPE stays free, open-source, and MIT licensed.
```

---

## Acceptance Criteria

* [x] Ko-fi is clearly the primary support path.
* [x] GitHub Sponsors is much more visible than the current footer-only icon.
* [x] Homepage has a prominent support section near the top.
* [x] Download area includes a support reminder.
* [x] Footer includes clear support links.
* [x] Docs pages include a subtle support banner.
* [x] Ko-fi floating widget appears and says `Support FPE`.
* [x] Site still works if Ko-fi script fails.
* [x] Existing demo, download buttons, docs links, and social links still work.
* [x] All external links use `target="_blank"` and `rel="noopener noreferrer"`.
* [x] Mobile layout remains clean.
* [x] No private Stripe, tax, phone, address, or payment details are added anywhere.

## Progress

Current phase:

* [x] Add shared header `Support FPE` Ko-fi CTA.
* [x] Add prominent homepage support section.
* [x] Add download-area support reminder.
* [x] Add shared footer support links.
* [x] Add docs-only support banner through `GuideLayout`.
* [x] Add centralized Ko-fi floating widget loader.
* [x] Build and inspect generated output.
* [x] Run visual/mobile sanity check.
* [x] Mark acceptance criteria complete after verification.

Verification:

* [x] `yarn build:web` completed successfully and canonical validation passed.
* [x] Rendered homepage and docs HTML contain support CTAs, docs banner, footer links, and `/support-widget.js`.
* [x] Headless Chrome mobile screenshots checked for homepage and docs wrapping.
* [x] GitHub Sponsors URL returned `200`.
* [x] Ko-fi URL accepted as owner-confirmed; the implemented URL and widget handle match the provided inputs.
