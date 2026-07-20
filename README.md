```markdown
# ♻️ SortIt — AI-Powered Waste Kiosk

SortIt is an intelligent, cloud-native waste classification kiosk system designed to streamline recycling and eco-friendly disposal. Using a high-efficiency cloud orchestration pipeline and advanced Vision AI, SortIt captures items via a front-facing camera, analyzes their material composition, and visually maps each part to its corresponding designated waste bin in real time.

---

## 🏗️ System Architecture & Workflow

The application operates on a completely serverless, decoupled cloud-native architecture. Once deployed, it requires zero local terminal interaction or active server management:

```text
[Camera/Screen - Vercel Frontend]
         |  (Captures frame, converts to Base64 JSON payload)
         v
[n8n Webhook Engine - Always-On Cloud Workflow]
         |  (Payload forwarding & prompt routing)
         v
[Google Gemini 2.0 Flash AI]
         |  (Visual processing & multi-component JSON classification)
         v
[Vercel UI Render] ---> Displays: Component Part ➡️ Assigned Bin Color

```

---

## 📁 Repository Structure

The project separates the user interface layout from the backend orchestration layer:

```text
sortit/
├── n8n-workflow/
│   └── sortit-workflow.json     # Importable backend blueprint for n8n Cloud
├── frontend/
│   ├── index.html               # Responsive Kiosk User Interface & Camera Handler
│   └── vercel.json              # Vercel deployment routing configuration
└── README.md                    # Project documentation

```

> ⚠️ **Dataset Architecture Note:** The full local project footprint includes a structural dataset directory (`data/`) encompassing over 5,000+ high-density reference images across multiple waste classes. To comply with modern cloud engineering practices, bypass GitHub remote file-size limitations, and keep the production branch optimized, this training layer is safely excluded via `.gitignore`. Real-time classification is completely handled live on the cloud.

---

## 🧠 Core Classification Matrix

The classification engine maps visual components directly to four rigid bin colors based on the foundational categories established by the project framework:

| Dataset Category | Target Material Sub-classes | Designated Kiosk Bin Mapping |
| --- | --- | --- |
| **`hazardous/`** | Chemicals, batteries, electronic waste components | 🔴 **Red Bin** |
| **`medical/`** | Bio-hazards, clinical materials, medical packaging | 🟡 **Yellow Bin** |
| **`recyclable/`** | Cardboard, glass, metal, paper, plastic composites | 🔵 **Blue Bin** |
| **`biodegradable/`** | Organic items, degradable cardboard, pure paper products | 🟢 **Green Bin** |

---

## 🚀 Deployment Steps

### Step 1 — Get a Free Gemini API Key

1. Go to [Google AI Studio Key Generator](https://aistudio.google.com/apikey) and sign in with a Google account.
2. Click **Create API Key** and copy it safely. Gemini's free tier (15 requests/minute, 1,500 requests/day) handles standard kiosk traffic beautifully without credit card requirements.

### Step 2 — Set up the n8n Cloud Orchestration Brain

1. Sign up on [n8n Cloud](https://n8n.io).
2. Click **Import from File** on your dashboard and upload `n8n-workflow/sortit-workflow.json`.
3. Open the **Gemini Vision - Classify** node ➡️ under *Credentials*, add a new **Query Auth** item:
* **Name:** `key`
* **Value:** *[Your copied Gemini API Key]*


4. Toggle the workflow status switch in the top-right corner to **Active / Published**.
5. Open the **Webhook** node and copy the **Production URL** (e.g., `https://yourname.app.n8n.cloud/webhook/sortit-scan`).

### Step 3 — Deploy the Frontend to Vercel

1. Open `frontend/index.html` and update the global webhook connection string with your live production URL:
```javascript
const N8N_WEBHOOK_URL = "[https://yourname.app.n8n.cloud/webhook/sortit-scan](https://yourname.app.n8n.cloud/webhook/sortit-scan)";

```


2. Commit and push your clean changes to your remote GitHub repository branch.
3. Import the repository into your [Vercel Dashboard](https://vercel.com). Vercel reads your root `vercel.json` structure automatically. Click **Deploy** to get your secure public `https://...` application link.

### Step 4 — Set up the Physical Kiosk

1. Launch the public Vercel deployment link on your kiosk screen, mobile module, or micro-PC browser (e.g., Raspberry Pi).
2. Set the browser view mode to Fullscreen/Kiosk (`F11`).
3. Position your integrated web-camera terminal. Present any item to the scanner lens, hit **Scan Item**, and track the real-time sorting recommendations!

---

## 📑 Technical Highlights

* **Prompt-Bounded Rules vs. Custom Classification Servers:** Training a traditional image classifier requires heavy custom server infrastructure and always-on web hosting fees. Instead, SortIt feeds exact dataset categories directly into Gemini's LLM vision context as structural rules, offering lightning-fast, zero-cost classification out of the box.
* **CORS Safe Routing:** Built-in wildcard optimization options inside the cloud gateway prevent cross-origin tracking dropouts during server-to-client operations.

---

### 🏛️ Program & Project Identification

* **Project Name:** SortIt
* **Target Focus:** UN Sustainable Development Goal 12 (SDG 12: Responsible Consumption and Production)
* **Deployment System:** Cloud Native Sustainability & Waste Classification Automation

```

```
