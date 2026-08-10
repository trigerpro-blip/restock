# Restock — setup

Five files. Put them online once, then it's an app on your phone and your computer. Cost: ₹0.

**Updating from the earlier version?** Upload all five again, replacing what's there. Your list, index and settings survive — they're in the browser and the gist, not in these files. The service worker version was bumped, so the new code lands on its own; if a device looks stale, close every tab and reopen.

---

## 1. Put it online (10 minutes, once)

Free HTTPS hosting, which you need — the camera refuses to work over plain `file://` or `http://`.

1. Sign in at **github.com**.
2. **+ → New repository**, name it `restock`, **Public**, Create.
3. Click **uploading an existing file** and drag in all five: `index.html`, `manifest.webmanifest`, `sw.js`, `icon-192.png`, `icon-512.png`. Commit.
4. **Settings → Pages** → Source: *Deploy from a branch*, branch `main`, folder `/ (root)`. Save.
5. A minute later, reload — it shows `https://YOURNAME.github.io/restock/`

The repo is public but holds only the app code. Your groceries live in a **private** gist (step 3).

**Install it:** Chrome → menu → *Add to Home screen*. iPhone: Safari → Share → *Add to Home Screen*.

---

## 2. Gemini key — for reading photos (5 minutes)

1. **aistudio.google.com/apikey** → sign in → **Create API key** → copy (`AIza…`).
2. In Restock: **gear** → paste into *Gemini API key* → **Test the key** → **Save settings**.

If the key rejects `gemini-2.5-flash`, put `gemini-2.0-flash` in the model box.

---

## 3. Sync between phone and computer (5 minutes)

1. **github.com/settings/tokens** → *Tokens (classic)* → **Generate new token (classic)**.
2. Name it `restock`, expiry **No expiration**, tick **only** `gist`. Generate, copy (`ghp_…`).
3. In Restock: **gear** → paste into *GitHub token* → **Create a gist** → note the **Gist ID** → **Save settings**.
4. On your computer: same site → gear → same token, same Gist ID → Save.

Header dot turns green. It pulls on open, on focus, and every 30 seconds. Merges item by item, so both devices can be open at once.

---

## How it works now

### The index is the home screen

It opens on your index — everything you've ever bought, each with a picture, how many times you've bought it, and how due it is. The **+** on any row sends it to *To buy*. Nothing lands there on its own.

Filter chips across the top: **All**, **Due**, **Expiring**, **On my list**.

### Pictures

Tap any thumbnail to set one. Five ways in, because barcodes are unreliable on loose goods:

- Take a photo
- Choose a file
- **Search the web** — opens Google Images for that item name; long-press a result → *Copy image* → come back → paste
- **Paste from clipboard** button, or just Ctrl/⌘ V anywhere on the page
- Drop an image, or paste an image link

Stored as a 112px square JPEG, about 3 KB. A hundred items with pictures is roughly 300 KB — comfortably inside what a gist holds. Items without a picture show a coloured initial instead; nothing is ever fetched or invented for you.

When you photograph a single item, the confirm sheet offers to keep that photo as its thumbnail, ticked by default.

### Expiry countdowns

Any recently bought perishable shows a dashed **+ expiry** chip. Tap it, pick a number of days or a date, and the row carries a countdown that recolours as it runs down: green, amber under 5 days, red under 2 or past. Sort the index by **Expiring first** to see what needs using.

Tick **Remember this shelf life** and it becomes automatic — every future time you mark that item bought, the countdown restarts by itself.

### Quantities

A plain number means pieces:

| You type | You get |
|---|---|
| `banana 6` | Banana — 6 pcs |
| `potatoes 4` | Potatoes — 4 pcs |
| `6 bananas` | Bananas — 6 pcs |
| `toor dal 1 kg` | Toor dal — 1 kg |
| `bhindi 500 g` | Bhindi — 500 g |
| `tomatoes 1/2 kg` | Tomatoes — 1/2 kg |
| `dahi` | Dahi |

Works in the quick-add box, in the bulk typing sheet, and on anything read out of a photo.

### Whole list in one shot

*Add → Photo of your whole list*, or copy a screenshot and paste it anywhere in the app. It reads everything, shows one confirm sheet with everything ticked, and then two choices:

- **Add to list** — onto *To buy*, and recorded in the index
- **Index only** — remembered for later, nothing on the shopping list

**Untick all** at the top flips the selection if you only want a couple.

---

## Where things are stored

| What | Where |
|---|---|
| List, index, pictures | This browser, plus your private gist |
| Gemini key, GitHub token | This browser only, never uploaded |
| App files | Your public GitHub repo |

Settings shows your total size and how many items have pictures. If the gist starts complaining, remove a few thumbnails.

**On iPhone especially, set up the gist sync early.** Safari clears local storage under pressure, and an installed web app isn't fully exempt — the gist is the copy that survives. *Export a backup* in the Index tab is worth doing occasionally too.

If a phone is lost: revoke the token at github.com/settings/tokens and the key at aistudio.google.com. One click each.

---

## If something misbehaves

- **Camera won't open** — the address must be `https://`, and the browser needs camera permission.
- **Live barcode scanning won't start on iPhone** — Safari can't do it in-page; *Photograph it* works everywhere.
- **A web image won't save** — some sites block other pages from reading their pictures. The link is kept instead, so it still shows, but it needs signal. Screenshot it and paste the screenshot to get a proper offline copy.
- **Dot says "sync error"** — token expired or lost its `gist` scope. Make a new one.
- **Changes to these files don't show up** — close all tabs and reopen, or bump `CACHE = 'restock-v2'` in `sw.js`.
