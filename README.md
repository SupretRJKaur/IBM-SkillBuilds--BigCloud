# ♻️ SortIt — AI-Powered Waste Segregation Kiosk

> **SortIt** is an intelligent waste segregation system that leverages **Google Gemini 1.5 Flash Vision** and **n8n workflow automation** to accurately classify waste. Unlike traditional classifiers that label an object as a single item, SortIt identifies **individual physical components** of an object and recommends the correct disposal bin for each component, enabling smarter and more sustainable waste management.

---

## 🌍 The Problem

Improper waste segregation is one of the biggest challenges in recycling. Many everyday objects are made from multiple materials, yet they are often discarded as a single piece of waste.

For example, a juice carton contains paper, plastic, and sometimes aluminum layers. Similarly, a coffee cup may contain paper, plastic, and leftover liquid. Disposing of the entire object in one bin reduces recycling efficiency and increases landfill waste.

SortIt addresses this challenge by using AI-powered visual understanding to identify each component individually and assign it to the appropriate waste stream.

---

# ✨ Features

- 📷 Live camera-based waste scanning
- 🤖 AI-powered image understanding using Google Gemini 1.5 Flash Vision
- 🧩 Component-level waste decomposition
- 🎨 Automatic color-coded waste bin assignment
- ⚡ Real-time waste classification
- 🔄 Automated backend powered by n8n workflows
- 📦 Structured JSON responses for seamless frontend integration
- 🌐 Lightweight static frontend
- 🚀 Easy deployment on Vercel or any static hosting platform

---

# 🗑️ Waste Bin Classification

SortIt categorizes detected waste into four standardized disposal bins.

| Bin | Category | Examples |
|------|----------|----------|
| 🔴 Red | Hazardous / E-Waste | Batteries, electronics, aerosol cans, chemicals, sharp objects |
| 🟡 Yellow | Medical Waste | Syringes, gloves, masks, bandages, medicine blister packs |
| 🔵 Blue | Recyclables | Plastic bottles, paper, cardboard, glass, metals, cans |
| 🟢 Green | Biodegradable | Food waste, organic matter, food-soiled paper |

---

# 🧩 Example Waste Segregation

Unlike conventional systems, SortIt analyzes every visible component of an object separately.

## 🥤 Tetra Pak Juice Box

| Component | Material | Bin |
|-----------|----------|-----|
| Carton Body | Cardboard | 🟢 Green |
| Plastic Straw | Plastic | 🔵 Blue |
| Straw Wrapper | Plastic | 🔵 Blue |

**Explanation**

Although commonly treated as a single item, a Tetra Pak consists of different materials. SortIt separates the cardboard body from the plastic straw and wrapper, ensuring each component is directed to the correct disposal bin.

---

## 🧴 Plastic Water Bottle

| Component | Material | Bin |
|-----------|----------|-----|
| Bottle | PET Plastic | 🔵 Blue |
| Cap | HDPE Plastic | 🔵 Blue |
| Label | Plastic Film | 🔵 Blue |

---

## ☕ Disposable Coffee Cup

| Component | Material | Bin |
|-----------|----------|-----|
| Paper Cup | Paper | 🟢 Green |
| Plastic Lid | Plastic | 🔵 Blue |
| Leftover Coffee | Organic Waste | 🟢 Green |

---

## 🔋 TV Remote

| Component | Material | Bin |
|-----------|----------|-----|
| Battery | Hazardous Chemical | 🔴 Red |
| Plastic Body | ABS Plastic | 🔵 Blue |

---

## 💊 Medicine Blister Pack

| Component | Material | Bin |
|-----------|----------|-----|
| Blister Pack | Medical Waste | 🟡 Yellow |
| Foil Layer | Medical Waste | 🟡 Yellow |

---

# 🏗️ System Architecture

```
                    User
                      │
                      ▼
             Capture Waste Image
                      │
                      ▼
          Frontend (index.html)
                      │
          POST Base64 Image
                      │
                      ▼
              n8n Webhook Trigger
                      │
                      ▼
        Prepare Gemini Vision Request
                      │
                      ▼
       Google Gemini 1.5 Flash Vision
                      │
                      ▼
      Component & Material Detection
                      │
                      ▼
        Parse & Validate JSON Output
                      │
                      ▼
       Return Structured JSON Response
                      │
                      ▼
     Render Color-Coded Waste Components
```

---

# 🔄 Workflow

### 1. Capture

The user captures an image using the device camera.

---

### 2. Upload

The frontend converts the captured image into Base64 format and sends it to the configured **n8n Production Webhook**.

---

### 3. AI Request Preparation

The workflow prepares the Gemini Vision request by embedding:

- Waste segregation instructions
- Material classification rules
- JSON formatting constraints

---

### 4. Gemini Vision Analysis

Google Gemini analyzes the image to determine:

- Item name
- Individual components
- Material type
- Appropriate disposal bin

---

### 5. Response Parsing

The raw AI response is sanitized and validated to guarantee a consistent JSON structure before being returned to the frontend.

---

### 6. Frontend Visualization

Each detected component is displayed as a separate card with its assigned waste bin, allowing users to easily understand how each part should be disposed of.

---

# 📂 Project Structure

```text
SortIt/
│
├── index.html          # Single-page application with live camera functionality
├── vercel.json         # Deployment configuration
└── README.md           # Project documentation
```

---

# 🛠️ Technology Stack

| Technology | Purpose |
|------------|---------|
| HTML5 | Frontend |
| CSS3 | Styling |
| JavaScript | Camera & API Integration |
| Google Gemini 2.0 Flash | Multimodal Vision AI |
| n8n | Workflow Automation |
| Vercel | Deployment |

---

# 🚀 Quick Setup

## 1. Configure n8n Workflow

- Import the workflow into your n8n instance.
- Add your Google Gemini API key.
- Activate the workflow.
- Copy the Production Webhook URL.

---

## 2. Connect the Frontend

Open **index.html** and update:

```javascript
const N8N_WEBHOOK_URL = "YOUR_PRODUCTION_WEBHOOK_URL";
```

---

## 3. Run the Project

Simply open:

```
index.html
```

or deploy it on any static hosting platform.

---

# 🚀 Deployment

### Deploy using Vercel

```bash
git clone https://github.com/your-username/SortIt.git

cd SortIt

vercel
```

or

1. Push the repository to GitHub.
2. Import it into Vercel.
3. Deploy.

No dedicated backend server is required because all AI processing is handled through **n8n**.

---

# 💡 Future Improvements

- 🌍 Multi-language support
- 🎤 Voice-assisted waste guidance
- 📊 Recycling analytics dashboard
- 📈 Confidence scores for AI predictions
- 🤖 IoT-enabled smart recycling kiosks
- 📦 Barcode and QR code recognition
- ☁️ Cloud storage for scan history

---

Built using **Google Gemini 2.0 Flash Vision**, **n8n**, and modern web technologies to make waste segregation smarter, more accurate, and environmentally responsible.
