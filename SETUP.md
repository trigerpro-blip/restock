# Restock — setup

Six files, hosted once, then it's an app on your phone and your computer. Cost: ₹0.

**Updating?** Upload all six over the old ones — `icon-512-maskable.png` is new, so make sure it goes up too. Your data survives and is converted automatically — anything that was in your old index becomes part of *Things I've bought*, and anything that had an expiry date set becomes part of *Things I have*. Nothing is lost.

---

## The three stages

Your sketch, working:

```
   Things to buy  ──tick──▶  Things I have  ──used up──▶  gone
                        └──────── recorded in ────────▶  Things I've bought
```

**Things I have** is the home screen. It's what's physically in the house right now, sorted by use-by date, numbered, showing quantity and where it lives — Fridge, Freezer, Pantry. Filter chips at the top switch between them.

**Things to buy** is the shopping list, grouped by aisle. Tick something and it moves into *Things I have* and gets logged in *Things I've bought* at the same moment. If it's perishable and has no date yet, the toast offers a **Use by** button right there.

**Cook** looks at what's in the house, leans hardest on whatever expires first, and suggests four dishes. Three settings: *Only what I have* (the default — staples like salt and oil assumed), *A few extras ok* (at most two cheap additions per dish), *Anything goes*. Tap **Recipe** for the full method; **Add the extras** puts whatever's missing on the buy list. If the strict suggestions are dull, there's a one-tap "let it use a few extra ingredients" underneath.

**Medicines** is a separate scratch list for the chemist — type "Dolo 650, 1 strip" and it splits the name from the strength. Anything you mark as a **regular refill** disappears when you get it and comes back as a countdown under *Regulars*. It's a reminder list only; there's no advice of any kind in it, by design.

**Things I've bought** is the permanent record, newest first, exactly as you drew it. Each row has a small picture, when you last bought it, how many times, and its rhythm ("~9d"). Items currently in the house show **in stock** instead of a due tag, so you don't buy them twice. **+** puts anything back on the buy list.

On a computer all three appear side by side, in the order you drew them. On a phone they're three tabs, opening on *Things I have*.

---

## 1. Put it online (10 minutes, once)

Free HTTPS hosting — needed, because the camera refuses to work over `file://` or `http://`.

1. Sign in at **github.com**.
2. **+ → New repository**, name it `restock`, **Public**, Create.
3. **uploading an existing file** → drag in all six: `index.html`, `manifest.webmanifest`, `sw.js`, `icon-192.png`, `icon-512.png`, `icon-512-maskable.png`. Commit.
4. **Settings → Pages** → *Deploy from a branch*, `main`, `/ (root)`. Save.
5. A minute later: `https://YOURNAME.github.io/restock/`

**Install:** Chrome → menu → *Add to Home screen*. iPhone: Safari → Share → *Add to Home Screen*.

## 2. Gemini key — reads photos (5 minutes)

**aistudio.google.com/apikey** → Create API key → copy → in Restock, **gear** → paste → **Test the key** → Save. If it rejects `gemini-2.5-flash`, use `gemini-2.0-flash`.

## 3. Sync — pick one (5 minutes)

Two ways to store your data on GitHub. **Use the private repo** unless you have a reason not to.

### A. Private repo + fine-grained token  ← recommended

1. **github.com/new** → name it `restock-data` → tick **Private** → tick *Add a README* → Create.
2. **github.com/settings/personal-access-tokens/new** (Fine-grained tokens)
   - Expiration: pick a date you'll remember, or *No expiration*
   - **Repository access → Only select repositories → `restock-data`**
   - **Permissions → Repository permissions → Contents → Read and write**. Nothing else.
   - Generate, copy (`github_pat_…`).
3. In Restock: **gear → Sync → Private repo**, paste the token, put your username in *Owner* and `restock-data` in *Repo*. Leave file and branch as they are. **Test sync**, then **Save settings**.
4. Same three values on your other device.

### B. Secret gist + classic token

1. **github.com/settings/tokens** → *Tokens (classic)* → Generate → tick **only** `gist`.
2. In Restock: **gear → Sync → Secret gist**, paste the token, tap **Create a gist**, note the Gist ID, Save.
3. Same token and ID on the other device.

### Which is actually better

| | Private repo | Secret gist |
|---|---|---|
| Who can read your data | Only someone signed in with access | **Anyone who gets the URL** — "secret" means unlisted, not private |
| What the token can touch | That one repo, nothing else | **Every gist on your account**, read and write |
| Token expiry | Enforced, your choice | Classic tokens can live forever |
| If the token leaks | One repo of groceries | All your gists |
| History | Every save is a commit — you can recover an older version | Gists keep revisions too |

The repo wins on both counts that matter: your data actually requires authentication to read, and the token is scoped so narrowly that a leak costs you almost nothing. Fine-grained tokens simply cannot access gists, which is why option B needs the older, broader classic token.

The gist route survives only because it's two fields instead of four, and the app can create the gist for itself. Both are free, both handle conflicts the same way, and you can switch between them any time — export a backup first, switch, then restore.

**One caveat for the repo:** each save is a commit, so a busy day makes a few dozen commits. Harmless, and it means you can dig an old version out of the repo history if you ever wreck something.

---

## Day to day

**Adding.** The **+ Add** button in the header holds all five routes: photo of a whole list, photo of one item, gallery/screenshot, typing, barcode. You can also copy a screenshot anywhere and paste it straight into the page.

Everything that comes in — photo or typed — ends with three buttons instead of one: **To buy · I have it · Record only.** There is no default and no plain "Add", so nothing can quietly land in the wrong place. A photo of your fridge shelf → *I have it*. A photo of your written list → *To buy*. A recipe for next month → *Record only*.

**After a shop.** Photograph the bill, hit **I have it**, and it walks you straight through the perishables one at a time — pick a number of days, *Save & next*, repeat, *Skip* anything you don't care about. **Remember this shelf life** is ticked by default, so each item only ever needs dating once; from the next purchase on, its countdown starts by itself.

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
- **New files don't show up** — close all tabs and reopen, or bump `CACHE = 'restock-v6'` in `sw.js`.
- **Home-screen icon still the old one** — icons are cached hard. Remove the app from your home screen and add it again after the new files are live.
