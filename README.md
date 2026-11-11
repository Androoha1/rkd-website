# Rīgas Kristus Draudze - website

The website of Riga Church of Christ (RKD, Rīgas Kristus Draudze).

It's one HTML page, one stylesheet and one translations file. There's no framework, no
`node_modules` and no build step: edit a file, refresh the browser, done. Please keep it that
simple unless there's a real reason not to.

## Run it

```bash
python -m http.server 8000      # → http://localhost:8000
```

Use a local server.

## Files

| File              | Contains                                                              |
|-------------------|-----------------------------------------------------------------------|
| `index.html`      | All markup, plus an inline script at the bottom (language switcher, scroll animations, smooth scrolling, donate toggle) |
| `styles.css`      | All styles. Colors, fonts and spacing are variables in `:root`       |
| `translations.js` | Every piece of visible text, in LV, EN and RU                         |
| `images/`         | Logo, favicon, hero photo                                             |

## Changing text

Nearly every text change is a `translations.js` change. Elements in `index.html` point to
keys:

```html
<h3 data-i18n="about.mission.title">Mission</h3>
```

```js
// translations.js: lv, en and ru each have the same keys
'about.mission.title': 'Mission',
```

Things you should know:

- **Update all three languages.** If a key is missing in one language, no error appears. The
  element just keeps the English text hardcoded in the HTML, and a Latvian visitor sees one
  English heading in the middle of the page. All three languages have complete keys right
  now; please don't be the one who breaks that.
- **The English text in `index.html` is the fallback.** It's what search engines and no-JS
  visitors see. Keep it in sync with `en`.
- **LV is the default language.** The visitor's choice is remembered in `localStorage`
  (`rkd_lang`). If you're "seeing the wrong language", that's probably why. Clear it.
- **Text is set with `textContent`**, so HTML inside translations shows up as literal text.
  This is intentional. Don't "fix" it with `innerHTML`.

## Changing styles

- Use the variables in `:root` (`--color-*`, `--font-*`, `--space-*`) instead of adding
  another shade of brown.
- Breakpoints are **768px** and **480px**.

## Caching (read this before you deploy)

Browsers cache aggressively. Everything will look right for you and stay broken for people
who visited last week.

- `styles.css` is loaded as `styles.css?v=3`. **Bump the number every time you change the
  CSS.**
- `translations.js` has **no** version parameter right now, so text changes can stay hidden
  behind a cached copy. Add `?v=` to it as well and bump it whenever translations change.

## Images

`images/photo.jpg` (the hero) is **4.3 MB**, which is a lot for a phone on mobile data just
to load the first screen. If you replace it, aim for a few hundred KB: resize it to roughly
2000px wide and compress it. Same goes for any image you add.

## Deploying

The site is hosted on a private web server.
