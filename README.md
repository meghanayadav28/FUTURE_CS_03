# API Security Risk Analysis & Boundary Audit (Task 3)

## 📌 Project Overview
This repository contains a professional, presentation-grade API Security Risk Analysis evaluating the authentication layers, transmission schema footprints, and transaction rate-limiting thresholds of a target production-grade SaaS platform gateway. 

The audit methodology and risk classifications are modeled directly after the industry-standard **OWASP API Security Top 10** project framework.

---

## 🛠️ Testing Methodology & Tooling
* **Interaction Engine:** Postman Web Dashboard Workspace Client
* **Audit Mode:** External, Passive Black-Box Boundary Inspection
* **Scope Parameters:** Read-Only Analysis of User Directory Microservices (`/api/users`)
* **Reference Framework:** OWASP API Security Core Threat Matrix

---

## 📊 Summary of Core Audit Findings

| Vulnerability Vector | Threat Mapping | Status / Posture | Remediation Priority |
| :--- | :--- | :--- | :--- |
| **01. Gateway Authentication** | OWASP API2:2023 - Broken Authentication | 🟩 **Secure** (Access Blocked) | Pass (Maintained) |
| **02. Payload Data Minimization** | OWASP API3:2023 - Excessive Data Exposure | 🟩 **Secure** (Filtered Schema) | Pass (Maintained) |
| **03. Transaction Rate Throttling** | OWASP API4:2023 - Unrestricted Resource Consumption | 🟥 **Vulnerable** (No Limits) | **Immediate Horizon** |

### 🔍 Technical Deep-Dive Summary:
1. **Broken Authentication Enforcement:** Verified. Base guest requests submitted without a signature token are actively intercepted at the boundary tier, returning a strict `missing_api_key` block and an HTTP 401 Unauthorized status code.
2. **Excessive Data Exposure:** Compliant. Individual resource lookup payloads limit transit data attributes strictly to necessary public presentation definitions (`id`, `email`, `first_name`, `last_name`, `avatar`). No backend configuration strings or operational meta-flags are leaked.
3. **Unrestricted Resource Consumption:** **Vulnerable.** The endpoint completely lacks traffic-throttling circuit breakers. High-velocity automated injection loops (15 actions within 5 seconds) processed consecutively at a flat `~378ms` response speed with a 100% success code, exposing the backend database layer to potential infrastructure denial attacks.

---

## 📁 Repository Architecture & Verification Signatures
To maintain clean, enterprise-ready repository hygiene, files are organized under the following directory map:

```text
future_cs_03/
├── Evidence/
│   ├── Evidence_CS-01.jpg   <- Perimeter token challenge and HTTP 401 verification capture
│   ├── Evidence_CS-02.jpg   <- JSON data schema minimization validation capture
│   └── Evidence_CS-03.jpg   <- Transaction flooding test and rate limit omission capture
├── API_Security_Risk_Analysis_Task-3.pdf  <- Full 12-slide landscape presentation report
└── README.md
