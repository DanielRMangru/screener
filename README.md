# ATS Algorithmic Bias Screener & Plaintext Normalizer

> Pre-flight resume audit engine designed to screen for ageism, demographic proxies, tenure velocity penalties, and algorithmic knockouts before submitting to modern ATS (Workday, Taleo, Greenhouse, Ashby) or AI ingestion layers (Eightfold.ai, Phenom, SeekOut).

Powered by **Gemini 3.8 Flash** with **Zero Data Retention** and an integrated **Document Poisoning & Prompt Injection Shield**.

---

## 🚀 Key Features

- **🗓️ 10-Year Rolling Window (Ageism Defense):** Automatically identifies pre-2016 employment dates and reframes senior tenure claims (e.g., "20+ years") to prevent algorithmic overqualification knockouts and salary-cap filters.
- **🎓 Graduation Date Cleansing:** Strips degree completion years (used as algorithmic proxies for applicant age).
- **🛡️ EEOC Demographic & Protected Class Shield:** Removes direct demographic cues (DOB, marital status, nationality, headshots) and modernizes legacy ISP email domains (`@aol.com`, `@yahoo.com`, `@comcast.net`).
- **⚡ Tenure Velocity & "Job-Hopper" Scoring:** Protects candidates with short stints (<24 months) by appending `(Contract)` tags and eliminating staffing agency misclassification strings (`via Agency X`).
- **📍 Commute Radius Knockout Defense:** Normalizes 5-digit ZIP codes and full street addresses down strictly to `City, ST` to bypass rigid algorithmic geo-fencing.
- **💰 Salary & Cliché Filter:** Strips unsolicited salary history (`$XXk/yr`) and deletes outdated clichés (_"References available upon request"_, generic _"Objective"_).
- **🎯 Active STAR Language Normalization:** Reframes passive duty phrasing (_"Responsible for..."_, _"Duties included..."_) into quantifiable, high-impact achievement statements.
- **🔤 Universal ASCII Delimiters:** Replaces parser-breaking Unicode bullets (`•`), middle dots (`·`), and en-dashes (`–`) with standard keyboard ASCII pipes (`|`) and asterisks (`*`).
- **📄 Client-Side File Extraction:** Upload or drag-and-drop `.pdf` (via PDF.js), `.docx` (via Mammoth), and `.txt`/`.md` files. All parsing occurs locally inside the browser.
- **⚡ Live Heuristic Telemetry:** 10 real-time regex chips provide instant feedback as you type.

---

## 🔒 Privacy Policy & Zero Data Retention

- **Zero-Retention Guarantee:** Resumes, contact information, and audit results are handled **strictly in volatile RAM** and immediately discarded upon response generation. Nothing is logged, cached, or written to disk or any database.
- **Local Document Extraction:** Binary PDF and Word documents are parsed directly in your browser using WebAssembly/JavaScript; files never touch server storage.
- **No AI Training:** Submissions are processed through zero-retention enterprise API endpoints and are never used to train or fine-tune models.
- **Prompt & Document Poisoning Shield:** Enforces strict boundary isolation (`<UNTRUSTED_CANDIDATE_DOCUMENT>`) and control-character stripping to neutralize prompt injection attacks.

---

## 🛠️ Quick Start

### 1. Clone & Install Dependencies

```bash
git clone https://github.com/DanielRMangru/screener.git
cd screener
npm install
```

### 2. Configure Environment

Copy the example environment file:

```bash
cp .env.example .env
```

Edit `.env` and provide your Google Gemini API key:

```env
PORT=3045
GEMINI_API_KEY=your_gemini_api_key_here
```

### 3. Run Locally

```bash
# Start server
npm start

# Or with live reload
npm run dev
```

Open your browser to:

- Direct access: `http://localhost:3045`
- Reverse-proxy path: `http://localhost:3045/screener`

---

## 🌐 Production Deployment (Nginx Reverse Proxy)

To host under a subpath such as `https://yourdomain.com/screener`:

```nginx
location /screener {
    rewrite ^/screener/?(.*)$ /$1 break;
    proxy_pass http://127.0.0.1:3045;
    proxy_http_version 1.1;
    proxy_set_header Upgrade $http_upgrade;
    proxy_set_header Connection 'upgrade';
    proxy_set_header Host $host;
    proxy_set_header X-Real-IP $remote_addr;
    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    proxy_set_header X-Forwarded-Proto $scheme;
    proxy_cache_bypass $http_upgrade;
    client_max_body_size 10M;
}
```

---

## 📖 DIY Manual Checklist

For applicants auditing their resumes manually, refer to the included [ATS Algorithmic Bias Audit.md](ATS%20Algorithmic%20Bias%20Audit.md) guide for a 10-step DIY inspection framework.

---

## 📄 License

ISC License. Built by [Daniel R. Mangru](https://danielmangru.com).
