# Restock — setup

Five files, hosted once, then it's an app on your phone and your computer. Cost: ₹0.

**Updating?** Upload all five again over the old ones. Your data survives and is converted automatically — anything that was in your old index becomes part of *Things I've bought*, and anything that had an expiry date set becomes part of *Things I have*. Nothing is lost.

---

## The three stages

Your sketch, working:

```
   Things to buy  ──tick──▶  Things I have  ──used up──▶  gone
                        └──────── recorded in ────────▶  Things I've bought
```

**Things I have** is the home screen. It's what's physically in the house right now, sorted by use-by date, numbered, showing quantity and where it lives — Fridge, Freezer, Pantry. Filter chips at the top switch between them.

**Things to buy** is the shopping list, grouped by aisle. Tick something and it moves into *Things I have* and gets logged in *Things I've bought* at the same moment. If it's perishable and has no date yet, the toast offers a **Use by** button right there.

**Things I've bought** is the permanent record, newest first, exactly as you drew it. Each row has a small picture, when you last bought it, how many times, and its rhythm ("~9d"). Items currently in the house show **in stock** instead of a due tag, so you don't buy them twice. **+** puts anything back on the buy list.

On a computer all three appear side by side, in the order you drew them. On a phone they're three tabs, opening on *Things I have*.

---

## 1. Put it online (10 minutes, once)

Free HTTPS hosting — needed, because the camera refuses to work over `file://` or `http://`.

1. Sign in at **github.com**.
2. **+ → New repository**, name it `restock`, **Public**, Create.
3. **uploading an existing file** → drag in `index.html`, `manifest.webmanifest`, `sw.js`, `icon-192.png`, `icon-512.png`. Commit.
4. **Settings → Pages** → *Deploy from a branch*, `main`, `/ (root)`. Save.
5. A minute later: `https://YOURNAME.github.io/restock/`

**Install:** Chrome → menu → *Add to Home screen*. iPhone: Safari → Share → *Add to Home Screen*.

## 2. Gemini key — reads photos (5 minutes)

**aistudio.google.com/apikey** → Create API key → copy → in Restock, **gear** → paste → **Test the key** → Save. If it rejects `gemini-2.5-flash`, use `gemini-2.0-flash`.

## 3. Sync (5 minutes)

**github.com/settings/tokens** → *Tokens (classic)* → Generate → tick **only** `gist` → copy. In Restock: **gear** → paste the token → **Create a gist** → note the Gist ID → Save. On your computer, same token and same Gist ID.

---

## Day to day

**Adding.** The **+ Add** button in the header holds all five routes: photo of a whole list, photo of one item, gallery/screenshot, typing, barcode. You can also copy a screenshot anywhere and paste it straight into the page.

Everything that comes in — photo or typed — asks one question first: **To buy / I have it / Record only.** So a photo of your fridge shelf goes to *I have*, a photo of your written list goes to *To buy*, and a recipe you might cook next month goes to *Record only*.

**Use-by dates.** Any item in the house without one shows a dashed **+ use by** chip. Tap it, pick a number of days or a date. The row then carries a countdown bar that recolours as it drains — green, amber under 5 days, red under 2 or past. Tick **Remember this shelf life** and every future purchase of that item starts its own countdown automatically.

**Used up.** The ✓ on a *Things I have* row. It vanishes — the purchase stays in the record, which is where the history belongs.

**Pictures.** Tap any thumbnail. Take a photo, choose a file, **search the web** (opens Google Images for that name — long-press → Copy image → come back → paste), paste from clipboard, drag one in, or give a link. 112px squares, about 3 KB each. No picture means a coloured initial; nothing is fetched unless you ask.

**Quantities.** A plain number means pieces.

| You type | You get |
|---|---|
| `banana 6` | Banana — 6 pcs |
| `eggs +30` | Eggs — 30 pcs |
| `toor dal 1 kg` | Toor dal — 1 kg |
| `bhindi 500 g` | Bhindi — 500 g |
| `tomatoes 1/2 kg` | Tomatoes — 1/2 kg |
| `cheese slice x1` | Cheese slice — 1 pcs |
| `dahi` | Dahi |

---

## Storage and safety

| What | Where |
|---|---|
| Have, buy, bought, pictures | This browser, plus your private gist |
| Gemini key, GitHub token | This browser only, never uploaded |
| App files | Your public GitHub repo |

**Set up the gist sync early, especially on iPhone** — Safari clears local storage under pressure and installed web apps aren't fully exempt. The gist is the copy that survives. *Export backup* lives in Settings.

Lost phone: revoke the token at github.com/settings/tokens and the key at aistudio.google.com. One click each.

## If something misbehaves

- **Camera won't open** — the address must be `https://`, and the browser needs permission.
- **Live barcode scanning won't start on iPhone** — Safari can't do it in-page; *Photograph it* works everywhere.
- **A web image won't save** — some sites block other pages from reading their pictures, so the link is kept instead and needs signal. Screenshot it and paste the screenshot for a proper offline copy.
- **"sync error"** — token expired or lost its `gist` scope. Make a new one.
- **New files don't show up** — close all tabs and reopen, or bump `CACHE = 'restock-v3'` in `sw.js`.
