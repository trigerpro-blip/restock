# Restock — setup

Four files. Put them on the web once, then it's an app on your phone and your computer.

Total cost: ₹0.

---

## 1. Put it online (10 minutes, once)

Free HTTPS hosting, which you need — the camera won't work over plain `file://` or `http://`.

1. Sign in at **github.com** (make an account if you don't have one).
2. Click **+ → New repository**. Name it `restock`. Set it **Public**. Create.
3. On the empty repo page click **uploading an existing file**, and drag in all five:
   `index.html`, `manifest.webmanifest`, `sw.js`, `icon-192.png`, `icon-512.png`.
   Click **Commit changes**.
4. Go to **Settings → Pages**. Under *Source* pick **Deploy from a branch**, branch `main`, folder `/ (root)`. Save.
5. Wait about a minute, then reload that page. It shows your address:
   `https://YOURNAME.github.io/restock/`

> The repo is public, so don't put anything private in it. Your grocery data never goes here — it lives in a **private** gist (step 3).

**Install it on your phone:** open that address in Chrome → menu → *Add to Home screen*. On iPhone use Safari → Share → *Add to Home Screen*. It then opens full-screen and works without signal.

---

## 2. Gemini key — for reading photos (5 minutes)

Barcodes and typing work without this. Only photos and screenshots need it.

1. Go to **aistudio.google.com/apikey** and sign in with any Google account.
2. **Create API key**. Copy it (starts with `AIza…`).
3. In Restock: tap the **gear** → paste into *Gemini API key* → **Test the key** → **Save settings**.

Free tier covers a generous number of images a day — ordinary grocery use won't come near it. If a photo ever fails with a limit message, wait a minute or scan the barcode instead. If the key rejects `gemini-2.5-flash`, put `gemini-2.0-flash` in the model box.

---

## 3. Sync between phone and computer (5 minutes)

Data is kept in one **private gist** on your GitHub account. No server, no cost.

1. Go to **github.com/settings/tokens** → *Tokens (classic)* → **Generate new token (classic)**.
2. Name it `restock`. Expiry: **No expiration** (or set a reminder to redo it).
3. Tick **only** the `gist` checkbox. Nothing else. Generate, and copy the token (`ghp_…`).
4. In Restock on your phone: **gear** → paste into *GitHub token* → tap **Create a gist**.
   It shows a **Gist ID**. Write it down.
5. **Save settings.** The dot in the header turns green and says *synced*.
6. Open the same site on your computer → gear → paste the **same token** and the **same Gist ID** → Save.

Both devices now read and write the same gist. It pulls when you open the app, when you switch back to it, and every 30 seconds while it's on screen. Changes merge item by item, so adding things on your phone while the laptop is open won't wipe either side.

Add something on your phone, then switch to the laptop tab — it appears within half a minute.

---

## How it works day to day

**Scan a barcode** — checks your own index first (instant), then Open Food Facts. Most Indian packaged brands are in there — Amul, Britannia, Parle, Tata, Maggi. If it's missing, you name it once and that code is yours forever.

**Take a photo** — of a product, a half-empty shelf, a handwritten list, a bill, or a WhatsApp screenshot. It comes back as a tick-list you confirm before anything is added.

**Tick something off** and it goes into your **Index** with the date. From the second purchase onward it learns your own gap — 9 days for dahi, 40 for atta — and the Index sorts by what's due, with a bar that fills as you get closer. That's the "what am I about to run out of" screen.

**Aisles** are set up for a kirana/supermarket run: vegetables & fruit, atta rice & dal, masala, oils & ghee, dairy, namkeen, cleaning, puja & sundries. Items are sorted into them automatically and you can change any of them.

---

## Where things are stored

| What | Where |
|---|---|
| List and index | This browser, plus your private gist |
| Gemini key, GitHub token | This browser only (localStorage), never uploaded |
| The app files | Your public GitHub repo |

The keys are stored on-device, so anyone who unlocks your phone can see them in the app. That's the trade-off for having no server. If a phone is lost: delete the token at github.com/settings/tokens and the key at aistudio.google.com — both take one click, and the app on your other device keeps working after you make new ones.

**Export a backup** at the bottom of the Index tab downloads everything as a JSON file. Worth doing occasionally.

---

## If something misbehaves

- **Camera won't open** — the site must be `https://`. Check the address bar, and allow camera access when the browser asks.
- **Live scanning doesn't start on iPhone** — Safari can't scan in-page; the app falls back automatically, and *Photograph it* works everywhere.
- **Dot says "sync error"** — the token expired or lost its `gist` scope. Make a new one and paste it in.
- **Changed the app files but nothing changed** — the service worker cached the old version. Close all tabs and reopen, or bump `CACHE = 'restock-v1'` to `v2` in `sw.js`.
