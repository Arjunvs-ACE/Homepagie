# Nook

Design your own browser homepage, preview it live, and get a link to paste into your browser. No account, no server, no hosting steps.

## How it works

Nook is one static page (`homepagei.html`).

- **Builder:** open the site normally. Pick a theme, wallpaper, font, widget style, widgets and quick links while a live preview updates.
- **Homepage:** "Create my link" packs your choices into the link (`…/#c=…`). Opening that link shows your homepage.

Your settings live inside the link, so nothing is stored on a server.

## Features

- 6 themes (aesthetic, paper, ink, midnight, sunset, forest)
- Wallpaper from an image link or an upload (with darken and blur)
- 5 fonts, 4 widget styles, adjustable roundness
- Widgets: greeting, clock and date, search bar, quick links, notes, daily quote
- Choice of search engine (Brave, Google, DuckDuckGo, Bing)
- Mobile-friendly builder and homepage

## Put it online (free, about 2 minutes)

1. Create a GitHub repo and upload `homepagei.html` and this README.
2. Repo **Settings → Pages → Deploy from a branch → `main` / root → Save**.
3. Your site appears at `https://<your-username>.github.io/<repo>/`.

## Use it as your homepage in Web browser (Android)

1. Open your Nook site, design your page, tap **Create my link**, then **Copy link**.
2. Brave → **Settings → Homepage** → turn on, choose a custom address, paste.

## Security notes

- A Content Security Policy in `<head>` blocks scripts from other sites, outside connections and form posts.
- Everything from the link is validated before use (theme, font and widget names are whitelisted; numbers are clamped), and all text is HTML-escaped. Only `http` and `https` links are allowed, so `javascript:` links are blocked.
- A homepage opened from someone else’s link shows a notice and the real domain under each shortcut. A wallpaper from another site isn’t loaded until you tap “Looks good”, so a crafted link can’t quietly reveal your IP address.
- Links open with no referrer (`noopener noreferrer`).
- Uploaded wallpapers stay in the browser (IndexedDB) and are never uploaded anywhere. Use an image link if you want the wallpaper on every device.
- Notes are saved unencrypted in the browser. Don’t keep passwords in them.
- Fonts load from Google Fonts. To remove that, delete the font `<link>` tags and the two `fonts.g…` entries in the CSP.

## Editing the script

The CSP only allows the exact `<script>` block it was generated for. **If you change the script, update the hash in the CSP tag or the page will stay blank.** Print the new hash with:

```
node -e "const s=require('fs').readFileSync('homepagei.html','utf8').match(/<script>([\\s\\S]*)<\\/script>/)[1];console.log('sha256-'+require('crypto').createHash('sha256').update(s).digest('base64'))"
```

## Ideas for contributors

New widgets (weather, to-do, pomodoro), more themes, drag-to-arrange layout, import/export of settings.
