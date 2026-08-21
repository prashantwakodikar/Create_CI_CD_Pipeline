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

SAST & DAST Security Tools

🔐 What are SAST and DAST?

SAST (Static Application Security Testing) and DAST (Dynamic Application Security Testing) are application security testing techniques used to identify vulnerabilities during the software development lifecycle.

Type	Full Form	How it works	When it runs
SAST	Static Application Security Testing	Analyzes source code, bytecode, or binaries without executing the application	During development / CI
DAST	Dynamic Application Security Testing	Tests a running application from the outside	QA / Staging / CI/CD
IAST	Interactive Application Security Testing	Combines runtime information with code analysis	During application execution
SCA	Software Composition Analysis	Finds vulnerabilities in third-party/open-source dependencies	Development / CI

⸻

🛡️ SAST Tools

SAST tools analyze application source code and identify security vulnerabilities such as:

* SQL Injection
* XSS
* Hardcoded secrets
* Insecure authentication
* Command injection
* Path traversal
* Insecure coding patterns
* Vulnerable APIs

Popular SAST Tools

Tool	Languages / Technology	Open Source	CI/CD Support
SonarQube	Java, JavaScript, TypeScript, C#, Python, etc.	Community Edition	✅
SonarCloud	Multiple languages	❌	✅
Semgrep	JavaScript, TypeScript, Java, Python, Go, etc.	✅	✅
GitHub CodeQL	JavaScript, TypeScript, Java, C/C++, Python, C#, Go, Ruby	✅	✅
Checkmarx	Multiple languages	❌	✅
Fortify SCA	Multiple languages	❌	✅
Veracode	Multiple languages	❌	✅
Snyk Code	Multiple languages	Partial	✅
Bandit	Python	✅	✅
ESLint Security Plugins	JavaScript / TypeScript	✅	✅

⸻

⭐ Recommended SAST Tools

1. SonarQube

SonarQube provides:

* Static code analysis
* Security vulnerability detection
* Code smells
* Bugs
* Security hotspots
* Code coverage integration
* Quality gates

Example CI flow:

Developer
   ↓
Git Push
   ↓
GitHub
   ↓
GitHub Actions
   ↓
Build & Test
   ↓
SonarQube Analysis
   ↓
Quality Gate
   ↓
Deploy

⸻

2. GitHub CodeQL

CodeQL analyzes your source code using semantic queries to identify security vulnerabilities.

Typical workflow:

GitHub Repository
       ↓
GitHub Actions
       ↓
CodeQL Analysis
       ↓
Security Findings
       ↓
GitHub Security Tab

It is especially useful if your project is already hosted on GitHub.

⸻

3. Semgrep

Semgrep performs fast static analysis using security rules.

Example:

semgrep --config=auto

It is useful for:

* JavaScript
* TypeScript
* Angular
* React
* Node.js
* Python
* Java
* Go

⸻

🌐 DAST Tools

DAST tools test the running application rather than analyzing source code.

They simulate attacks against the application and identify vulnerabilities such as:

* XSS
* SQL Injection
* Authentication issues
* Authorization problems
* Security headers
* Session problems
* Misconfigured APIs
* Server-side vulnerabilities

Popular DAST Tools

Tool	Type	Open Source	CI/CD
OWASP ZAP	DAST	✅	✅
Burp Suite	DAST / Web Security	Community + Commercial	✅
Invicti	DAST	❌	✅
Acunetix	DAST	❌	✅
Veracode DAST	DAST	❌	✅
StackHawk	DAST / API Security	❌	✅
Nuclei	Vulnerability Scanner	✅	✅
Nikto	Web Server Scanner	✅	✅

⸻

⭐ Recommended DAST Tools

1. OWASP ZAP

OWASP ZAP (Zed Attack Proxy) is one of the most popular open-source DAST tools.

It can scan:

* Web applications
* REST APIs
* Authentication flows
* HTTP endpoints
* Security headers
* Common web vulnerabilities

Example:

zap-baseline.py \
  -t https://example.com \
  -r zap-report.html

Typical CI/CD flow:

Build
 ↓
Deploy to Test Environment
 ↓
Start Application
 ↓
OWASP ZAP Scan
 ↓
Generate Security Report
 ↓
Pass / Fail Pipeline

⸻

🔎 SAST vs DAST

                 APPLICATION SECURITY
                         │
             ┌───────────┴───────────┐
             │                       │
            SAST                    DAST
             │                       │
       Source Code              Running App
             │                       │
             ↓                       ↓
     Find Coding Issues       Find Runtime Issues
             │                       │
             ↓                       ↓
       Before Deploy           After Deploy

Example

Suppose your Angular/Node.js application contains:

const query = `SELECT * FROM users WHERE id = ${userId}`;

A SAST tool may detect the potential SQL injection by analyzing the source code.

A DAST tool may detect the vulnerability by sending malicious input to the running API.

⸻

🧩 SCA Tools

SCA is different from SAST and DAST.

SCA = Software Composition Analysis

It checks third-party dependencies for known vulnerabilities.

Popular SCA tools:

Tool	Purpose
Snyk Open Source	Dependency vulnerabilities
Dependabot	GitHub dependency updates
OWASP Dependency-Check	Known vulnerable dependencies
Mend	Open-source dependency security
Trivy	Dependencies, containers, IaC
npm audit	npm dependency vulnerabilities

For a Node.js / Angular project:

npm audit

⸻

🏗️ Complete DevSecOps Pipeline

A modern CI/CD pipeline can combine all of these security checks:

                 Developer
                     │
                     ↓
                  Git Push
                     │
                     ↓
              ┌──────────────┐
              │   CI Pipeline │
              └──────┬───────┘
                     │
          ┌──────────┼──────────┐
          ↓          ↓          ↓
        SAST        SCA       Secrets
          │          │          │
      CodeQL      Snyk       Secret Scan
      Semgrep     npm audit
      SonarQube
          │          │          │
          └──────────┼──────────┘
                     ↓
                   Build
                     ↓
                   Test
                     ↓
             Deploy to Staging
                     │
                     ↓
                   DAST
                     │
                OWASP ZAP
                     │
                     ↓
              Security Gate
                     │
              ┌──────┴──────┐
              ↓             ↓
            PASS           FAIL
              │             │
              ↓             ↓
         Production       Fix Issue
           Deploy

🏆 Recommended Stack for Angular + Node.js

For an Angular / TypeScript / Node.js application, a practical security stack is:

┌─────────────────────────────────────────┐
│              GitHub Actions             │
├─────────────────────────────────────────┤
│                                         │
│  SAST                                   │
│  ├── CodeQL                             │
│  ├── Semgrep                            │
│  └── SonarQube                           │
│                                         │
│  SCA                                    │
│  ├── npm audit                          │
│  ├── Snyk                               │
│  └── Dependabot                         │
│                                         │
│  Secrets                                │
│  └── GitHub Secret Scanning              │
│                                         │
│  DAST                                   │
│  └── OWASP ZAP                          │
│                                         │
└─────────────────────────────────────────┘

Quick Recommendation

Requirement	Recommended Tool
Code Quality + SAST	SonarQube
GitHub-native SAST	CodeQL
Fast custom SAST rules	Semgrep
Dependency Security	Snyk / Dependabot
Open-source DAST	OWASP ZAP
Web/API Security Testing	Burp Suite
Container Security	Trivy
Secret Detection	GitHub Secret Scanning

Best Combination

For a typical enterprise Angular + Node.js project:

CodeQL
   +
SonarQube
   +
Snyk / Dependabot
   +
OWASP ZAP
   +
GitHub Secret Scanning

This provides a strong DevSecOps security layer across source code, dependencies, secrets, and the running application.


