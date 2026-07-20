# SortIt — Kiosk Deployment Guide (Free Version — Google Gemini)

Screen-in-front-of-bins setup. No terminal, no local machine needed after deployment.
This version uses **Google Gemini 2.0 Flash** instead of OpenAI — Gemini's free tier
(15 requests/minute, 1500 requests/day) is enough for a kiosk that isn't scanning
constantly.

Bin logic is grounded in your dataset's own folder structure, so the AI classifies
into the same 4 categories your data uses, then maps each to a bin:

| Dataset category | Bin   |
|---|---|
| `hazardous`      | 🔴 Red |
| `medical`         | 🟡 Yellow |
| `recyclable` (cardboard, glass, metal, paper, plastic) | 🔵 Blue |
| `biodegradable` (cardboard, paper) | 🟢 Green |

## STEP 1 — Get a free Gemini API key

1. Go to https://aistudio.google.com/apikey and sign in with a Google account.
2. Click **Create API Key** — copy it somewhere safe. This is free, no card needed.

## STEP 2 — Set up n8n (the "brain" — hosted, always-on)

1. Go to https://n8n.io and sign up for **n8n Cloud** (free tier available).
   (Or self-host on Railway/Render — same steps apply.)
2. Click **Import from File** and upload `sortit-workflow.json`.
3. Open the **"Gemini Vision - Classify"** node → under Credentials, add a new
   **Query Auth** credential:
   - Name: `key`
   - Value: *your Gemini API key from Step 1*
4. Click **Activate** (top-right toggle) to make the workflow live.
5. Open the **Webhook** node → copy the **Production URL**
   (looks like `https://yourname.app.n8n.cloud/webhook/sortit-scan`).

This URL is now your always-on backend — no local machine required, and no
per-use cost since Gemini's free tier covers it.

## STEP 3 — Deploy the Frontend to Vercel (public screen)

The frontend (`index.html`) doesn't need any changes for the free version — it
just calls the webhook and renders whatever JSON comes back, same shape as before.

1. Open `index.html` and paste your n8n webhook URL into:
   ```js
   const N8N_WEBHOOK_URL = "https://yourname.app.n8n.cloud/webhook/sortit-scan";
   ```
2. Push this folder to a GitHub repo (keep `index.html` and `vercel.json` at the
   same level, matching this project's existing structure).
3. Go to https://vercel.com → **New Project** → Import that GitHub repo.
4. Vercel auto-detects `vercel.json` — click **Deploy**.
5. You'll get a public URL like `https://sortit-yourname.vercel.app`.

## STEP 4 — Set up the physical kiosk

1. On the screen above the bins, open the Vercel URL in a browser.
2. Put the browser in **Kiosk/Fullscreen mode** (F11, or a kiosk browser app on
   a Raspberry Pi / mini PC / Android tablet).
3. Connect a USB or built-in camera facing the person.
4. Done — anyone walks up, holds the item to the camera, taps "Scan Item", and
   the screen shows which bin each component goes in.

## How it all connects

```
[Camera/Screen - Vercel hosted frontend]
        |  (captures photo, sends as base64)
        v
[n8n webhook - always-on cloud workflow, FREE]
        |  (sends photo to Gemini 2.0 Flash)
        v
[Gemini classifies into: hazardous / medical / recyclable / biodegradable]
        |  (returns JSON with per-component bins)
        v
[Frontend displays: Part -> Bin color]
```

No terminal is ever opened during actual use — n8n runs the AI logic 24/7 in
the cloud on Gemini's free tier, and the frontend is a static site on Vercel.

## Why this classification approach (not a trained model)

Your dataset (biodegradable/cardboard, biodegradable/paper, hazardous, medical,
recyclable/{cardboard,glass,metal,paper,plastic}) defines the categories, but
training a custom image classifier would need its own always-on hosting (not
free, and not something n8n does natively). Instead, Gemini's vision model is
prompted with your exact category definitions as classification rules — so it
reasons about *any* item using the same categories your dataset uses, without
needing a training step or a hosted model server. If you later want to validate
or improve accuracy against your actual images, that dataset is still useful for
manual testing — just run a batch of your labeled photos through the webhook and
compare Gemini's output to the folder each image came from.
