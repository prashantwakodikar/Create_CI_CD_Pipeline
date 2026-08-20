# 🚀 Create CI/CD Pipeline

This repository demonstrates a **modern Angular CI/CD workflow** using **GitHub Actions**.  
It automates build, test, and deployment steps, ensuring reliable delivery of production‑ready code.

---

## ⚡ Workflow Overview
The pipeline is defined in `.github/workflows/ci.yml` and runs on every push or pull request to `main` or `develop`.

### 🔑 Key Stages
1. **Checkout** → Pulls source code into the runner.  
2. **Setup Node.js** → Configures Node.js v24 with npm caching.  
3. **Install Dependencies** → Runs `npm ci` for reproducible installs.  
4. **Unit Tests** → Executes Angular tests in headless Chrome.  
5. **Build** → Compiles production‑ready static assets.  
6. **Upload Artifacts** → Stores build output for deployment.  
7. **Deploy** → Publishes to GitHub Pages using `angular-cli-ghpages`.  
8. **Verify Deployment** → Confirms site availability via `curl`.

---

## 🧩 Workflow File (`ci.yml`)
