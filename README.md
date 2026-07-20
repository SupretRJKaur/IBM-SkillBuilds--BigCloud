````markdown
# ♻️ SortIt — AI-Powered Waste Classification Kiosk

> **SortIt** is an intelligent, cloud-native waste classification kiosk that uses **Google Gemini Vision AI** to identify waste materials and recommend the correct disposal bin in real time. Built on a **fully serverless architecture**, the system requires no backend hosting or local server management after deployment.

---

# 🌍 Overview

SortIt helps improve waste segregation by combining computer vision, cloud automation, and AI-powered classification. A user simply places an item in front of the kiosk camera, and the system analyzes it, detects individual components, and recommends the appropriate waste bin for each detected material.

The entire processing pipeline runs on cloud services, making the solution lightweight, scalable, and easy to deploy.

---

# ✨ Features

- 📷 Camera-based real-time waste scanning
- 🤖 Google Gemini 2.0 Flash Vision AI integration
- ☁️ Fully serverless cloud architecture
- 🔄 n8n cloud workflow orchestration
- 🌐 Vercel frontend deployment
- 🧩 Multi-component object analysis
- 🗂️ Material-wise waste segregation
- ⚡ Zero backend server maintenance
- 📱 Responsive kiosk interface
- 🌱 Designed for SDG 12 (Responsible Consumption and Production)

---

# 🏗️ System Architecture

```text
                     +---------------------------+
                     |   Camera / Browser UI     |
                     |     (Vercel Frontend)     |
                     +-------------+-------------+
                                   |
                                   | Capture Image
                                   | Convert to Base64
                                   v
                     +---------------------------+
                     |     n8n Cloud Webhook     |
                     |  Workflow Orchestration   |
                     +-------------+-------------+
                                   |
                                   | Prompt Routing
                                   v
                     +---------------------------+
                     | Google Gemini 2.0 Flash   |
                     |      Vision AI Model      |
                     +-------------+-------------+
                                   |
                                   | JSON Response
                                   v
                     +---------------------------+
                     |      Vercel Frontend      |
                     | Displays Component → Bin  |
                     +---------------------------+
```

---

# 🔄 Workflow

1. User places an object in front of the kiosk camera.
2. The frontend captures an image.
3. The image is converted into a Base64 payload.
4. The payload is sent to an n8n webhook.
5. n8n forwards the request to Google Gemini Vision.
6. Gemini identifies every visible material/component.
7. Gemini returns structured JSON.
8. The frontend displays the recommended waste bin for every detected component.

---

# 📁 Project Structure

```text
sortit/
│
├── frontend/
│   ├── index.html
│   └── vercel.json
│
├── n8n-workflow/
│   └── sortit-workflow.json
│
├── README.md
│
└── data/                 (Ignored via .gitignore)
```

### Folder Description

| Folder | Purpose |
|----------|----------|
| **frontend/** | User interface, camera capture, API communication |
| **n8n-workflow/** | Importable cloud workflow |
| **README.md** | Documentation |
| **data/** | Local reference dataset (excluded from GitHub) |

---

# 📂 Dataset Information

The development version of SortIt contains a local dataset consisting of **5,000+ reference images** covering multiple waste categories.

To keep the repository lightweight and comply with GitHub storage limitations, the dataset is excluded using `.gitignore`.

```text
data/
├── hazardous/
├── medical/
├── recyclable/
└── biodegradable/
```

The deployed application **does not require the dataset** because classification is performed live using **Google Gemini Vision AI**.

---

# 🧠 Waste Classification Matrix

| Dataset Category | Example Materials | Assigned Bin |
|-----------------|------------------|--------------|
| **hazardous/** | Batteries, chemicals, electronic waste | 🔴 Red Bin |
| **medical/** | Medical packaging, biohazard waste, clinical items | 🟡 Yellow Bin |
| **recyclable/** | Plastic, glass, cardboard, metal, paper | 🔵 Blue Bin |
| **biodegradable/** | Organic waste, biodegradable paper, food waste | 🟢 Green Bin |

---

# 🚀 Deployment Guide

## Step 1 — Generate a Gemini API Key

Visit:

https://aistudio.google.com/apikey

1. Sign in using a Google account.
2. Click **Create API Key**.
3. Copy and securely store the generated key.

The free tier provides:

- 15 requests per minute
- 1,500 requests per day

which is sufficient for typical kiosk usage.

---

## Step 2 — Configure n8n Cloud

1. Create an account at:

https://n8n.io

2. Import:

```text
n8n-workflow/sortit-workflow.json
```

3. Open the **Gemini Vision - Classify** node.

4. Create a new Query Authentication credential.

```
Name:
key

Value:
YOUR_GEMINI_API_KEY
```

5. Activate the workflow.

6. Copy the Production Webhook URL.

Example:

```
https://your-workspace.app.n8n.cloud/webhook/sortit-scan
```

---

## Step 3 — Configure the Frontend

Open:

```javascript
frontend/index.html
```

Replace:

```javascript
const N8N_WEBHOOK_URL = "YOUR_WEBHOOK_URL";
```

with your production webhook URL.

Example:

```javascript
const N8N_WEBHOOK_URL =
"https://your-workspace.app.n8n.cloud/webhook/sortit-scan";
```

---

## Step 4 — Deploy on Vercel

1. Push the project to GitHub.
2. Import the repository into Vercel.
3. Vercel automatically detects:

```text
vercel.json
```

4. Click **Deploy**.

After deployment you'll receive a public URL similar to:

```
https://sortit.vercel.app
```

---

## Step 5 — Physical Kiosk Setup

1. Open the Vercel deployment URL.
2. Switch the browser to Fullscreen (F11).
3. Connect a webcam.
4. Present an item.
5. Press **Scan Item**.
6. View the recommended waste bins.

---

# 💡 Technical Highlights

### Serverless Architecture

No backend hosting is required after deployment.

---

### AI Vision Classification

Google Gemini Vision performs:

- Material recognition
- Multi-object analysis
- Component-wise classification
- Structured JSON generation

---

### Cloud Workflow Automation

n8n acts as the orchestration layer:

- Receives image payload
- Routes prompts
- Sends requests to Gemini
- Returns structured responses

---

### Responsive Frontend

The frontend provides:

- Camera interface
- Live scanning
- JSON rendering
- Bin recommendations

---

### CORS-Safe Communication

The application is designed to support secure frontend-to-cloud communication while avoiding common cross-origin issues.

---

# 🛠️ Technologies Used

| Technology | Purpose |
|------------|----------|
| HTML5 | User Interface |
| CSS3 | Styling |
| JavaScript | Frontend Logic |
| Google Gemini 2.0 Flash | Vision AI |
| n8n Cloud | Workflow Automation |
| Vercel | Frontend Hosting |
| JSON | AI Response Format |

---

# 🌱 Sustainability Impact

SortIt promotes:

- Better waste segregation
- Increased recycling efficiency
- Reduced landfill contamination
- Smarter public recycling systems

The project aligns with:

## United Nations Sustainable Development Goal 12

**Responsible Consumption and Production**

---

# 📌 Project Information

| Property | Value |
|----------|-------|
| **Project Name** | SortIt |
| **Category** | AI-Powered Waste Classification |
| **Architecture** | Cloud Native |
| **Deployment** | Serverless |
| **Frontend** | Vercel |
| **Workflow Engine** | n8n Cloud |
| **Vision AI** | Google Gemini 2.0 Flash |
| **Primary Goal** | Smart Waste Segregation |

---

# 📜 License

This project is intended for educational, research, and sustainability-focused applications.

---

**SortIt** demonstrates how modern cloud-native technologies, workflow automation, and multimodal AI can be combined to build scalable, intelligent, and environmentally conscious waste management solutions.
````
