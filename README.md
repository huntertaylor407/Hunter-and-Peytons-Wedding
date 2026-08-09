Hunter & Peyton — Garden Party Disco Wedding Website
A two-page wedding website: a single scrolling homepage (`index.html`) and a
separate day-of schedule (`schedule.html`). Plain HTML, CSS and vanilla
JS — no build step, no frameworks. Open `index.html` in a browser to preview,
or host the whole folder anywhere static (GitHub Pages, Netlify, Vercel,
plain S3, etc).
```
wedding/
├── index.html          ← homepage (all sections)
├── schedule.html        ← day-of timeline
├── css/style.css        ← all styling + color palette (CSS variables)
├── js/main.js            ← nav, animations, countdown, gallery, forms, music
├── images/               ← put your photos here (see below)
├── audio/                ← optional ambient background track
└── README.md              ← this file
```
Quick start
Open `index.html` in your browser to see the placeholder site.
Do a find-and-replace across `index.html` and `schedule.html` for every
`{{PLACEHOLDER}}` token — your code editor's "Find in Files" / "Find All"
works well for this. Each token is named for what goes there, e.g.
`{{PARTNER\_ONE}}`, `{{VENUE\_NAME}}`, `{{WEDDING\_DATE\_LONG}}`.
Add your photos to `/images` (filenames and sizes below) and uncomment
the matching `<img>` tags.
Set your real countdown date (see below).
Connect your RSVP form (see below).
Optional: add a background music track (see below).
Publish the folder to your host of choice.
Where everything lives
What	Where
Names, date, venue, all page copy	`{{PLACEHOLDER}}` tokens in `index.html` and `schedule.html`
Countdown target date/time	`data-countdown="..."` attribute on the countdown `<div>` in `index.html` (search for it)
Colors	CSS variables at the top of `css/style.css` (`:root`)
Fonts	`<link>` tag in the `<head>` of both HTML files (Google Fonts)
Photos	`/images` folder — see filenames below
Registry links	`{{REGISTRY\_URL\_1/2/3}}` in the Registry section of `index.html`
Schedule / timeline	`schedule.html`, one `.timeline-item` block per event
RSVP form	`.rsvp-form` in `index.html`, plus notes below
Background music	`<audio id="ambient-audio">` near the end of `index.html`, plus `/audio` folder
Social links	Footer of `index.html` (`.footer-social`)
Adding your photos
Every photo slot on the site currently shows a soft color placeholder with a
label telling you exactly what file to add and its recommended size, e.g.:
```html
<div class="story-photo">
  <!-- <img src="images/story-photo-1.jpg" alt="Describe this photo"> -->
  <div class="photo-frame-label">Add story-photo-1.jpg here (1000×1250px)</div>
</div>
```
To add a real photo:
Save your image into `/images` using the suggested filename (or your own —
just update the `src`).
Uncomment the `<img>` line and fill in a real, descriptive `alt` attribute
for screen reader accessibility.
Delete or comment out the `<div class="photo-frame-label">` line below it.
Recommended sizes:
Hero background — optional; the hero uses a CSS gradient by default.
To swap in a photo, add a full-bleed image (2400×1600px, `images/hero-photo.jpg`)
and see the comment inside the `.hero` section of `index.html`.
Our Story photos — 1000×1250px (4:5 ratio), JPG, under 400KB
Wedding Party photos — 600×600px (square), JPG, under 250KB
Gallery photos — 1200px on the long edge, JPG, under 500KB each
Social share image (`images/social-share.jpg`, used in link previews) — 1200×630px
Keep total image weight reasonable (a few MB across the whole gallery) so the
site stays fast on mobile data.
Setting the countdown date
In `index.html`, find:
```html
<div class="countdown reveal-scale" data-countdown="2027-06-12T16:00:00" ...>
```
Change `2027-06-12T16:00:00` to your real wedding date and start time, in the
format `YYYY-MM-DDTHH:MM:SS` using a 24-hour clock in your local timezone.
Connecting your RSVP form
The form ships as a working demo: submitting it shows a thank-you message but
doesn't send the data anywhere yet. Pick one option (see the comment directly
above `<form class="rsvp-form">` in `index.html` for the same instructions):
Google Forms (easiest): build a form at forms.google.com, use
Send → Embed HTML, and replace the `<form>...</form>` block with the
`<iframe>` snippet it gives you.
Tally, Typeform, or similar: same approach — swap in their embed code,
or simply replace the form with a button linking to your form's URL.
Your own backend / Formspree / Netlify Forms: set the form's `action`
and `method` attributes to your endpoint, and in `js/main.js` (section 8,
"RSVP FORM"), remove the `e.preventDefault()` call so the browser submits
normally.
Adding background music
The music toggle button is muted/paused by default, as required — a guest
must tap it to opt in. To use it:
Add a short, loop-friendly ambient track (garden ambience with a light
disco undertone works well) to `/audio/ambient-garden-disco.mp3`.
Make sure you have the rights to use the track on a public website.
That's it — the existing `<audio id="ambient-audio">` element and
`.music-toggle` button in `index.html` already wire it up.
If you'd rather not include music at all, delete the `<audio>` element and
the `<button class="music-toggle">` from `index.html`, and section 9 of
`js/main.js` will simply do nothing.
Editing colors
All colors are CSS custom properties at the top of `css/style.css`:
```css
:root {
  --blush-pink:    #e9b7bb;
  --blood-orange:  #cc4b24;
  --dusty-coral:   #d98871;
  --sage-green:    #8a9a6b;
  --mauve:         #a2748c;
  --berry:         #8e3b5d;
  --wine:          #4d1930;
  --burnt-orange:  #bf5b30;
  --olive:         #6e6b35;
  --slate-blue:    #5c6b8a;
  --cream:         #fbf5ea;
}
```
Change a hex value here and it updates everywhere that color is used.
Editing the schedule
`schedule.html` contains one `.timeline-item` block per event (arrival,
ceremony, cocktail hour, dinner, toasts, dancing, send-off). A copy-paste
template with instructions is included as an HTML comment right above the
first entry. Each item has a `timeline-marker` with a category class
(`prelude`, `ceremony`, `cocktail`, `dinner`, `toasts`, `dancing`,
`sendoff`) that controls its color — reuse these or add new categories in
`css/style.css`.
Accessibility & performance notes
Semantic HTML landmarks (`header`, `main`, `footer`, `nav`) throughout.
All interactive elements are keyboard-operable (nav menu, FAQ accordion,
gallery lightbox with arrow-key navigation and Escape to close).
Color choices maintain readable contrast against their section backgrounds.
Animations respect `prefers-reduced-motion` and are disabled for users who
have that setting turned on.
No build step, no heavy JS frameworks — the whole site is a handful of
lightweight files, so it loads fast even on mobile data.
Hosting on GitHub Pages
Push this folder to a GitHub repository (root of the repo, or a `/docs`
folder — either works).
In the repo, go to Settings → Pages, choose the branch and folder
you pushed to, and save.
Your site will publish at `https://your-username.github.io/repo-name/`.
Update the `{{YOUR\_DOMAIN}}` placeholder in the Open Graph tags in
`index.html` to match your final URL (or your custom domain, if you add one).
Enjoy the party. 🪩
