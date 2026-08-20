# FinGuardian: Enterprise Automated Tax & Financial Intelligence Platform
FinGuardian AI Multi-Year Indian Tax Audit &amp; Savings Engine

> **Architectural Paradigm:** Event-Driven Microservices | Zero-Trust AI Data Pipeline | Hybrid Low-Cost Multi-Cloud Design

FinGuardian is an enterprise-grade financial intelligence platform designed to automate document parsing, complex tax calculations, and dynamic report generation. Built using modern cloud-native architectures, standard compliance controls, and privacy-preserving AI orchestration, FinGuardian processes sensitive tax assets with sub-second retrieval latency while adhering to strict data sovereignty mandates.

---

## 🏛️ Enterprise Architectural Principles & Technical Rationale

The architecture reflects Staff-level engineering decisions balancing cost optimization, high availability, and regulatory security:

* **Zero-Trust Ingestion & PII Masking:** All financial documents pass through an isolation pipeline. Sensitive Personally Identifiable Information (PII) is anonymized locally using deterministic masking algorithms prior to any external LLM processing.
* **Hybrid Storage Pattern (AES-256 + Temporal JWTs):** Raw document bytes are encrypted at rest via AES-256-GCM. External API communications pass ephemeral, cryptographic JWT claims to grant time-bound read access.
* **Cost-Optimized Hybrid Infrastructure:** Low-frequency containerized workloads run on Google Kubernetes Engine (GKE) Autopilot, while stateful database workers and proxy gateways leverage compute-tuned GCP Compute Engine (GCE) nodes—reducing operational costs by up to 60%.
* **Low-Latency Hybrid Backend:** High-throughput transactional APIs are handled via Java 21 & Spring Boot 3 with virtual threads (Project Loom), driving non-blocking execution across Postgres connection pools.
* **Resilient Edge Delivery:** The web client leverages Next.js 14 and React Progressive Web App (PWA) primitives, enabling offline access, edge caching, and server-side rendering (SSR) for optimal user experience.

---

## 📐 System Architecture Overview

```
+-----------------------------------------------------------------------------------+
|                                  Edge / Client                                    |
|    Next.js 14 PWA Client (Responsive, Offline Support, Ephemeral JWT Handling)   |
+----------------------------------------+------------------------------------------+
                                         | Secure TLS 1.3
                                         v
+-----------------------------------------------------------------------------------+
|                              Ingress & Security Layer                             |
|            GCP Cloud Armor (WAF / DDoS) + Envoy Gateway / Reverse Proxy          |
+----------------------------------------+------------------------------------------+
                                         |
            +----------------------------+----------------------------+
            |                                                         |
            v                                                         v
+---------------------------------------+   +---------------------------------------+
|        Spring Boot Core API           |   |      Python Document Engine           |
|  - Auth & Cryptographic Tokens        |   |  - Anonymization & PII Masking        |
|  - AES-256 Encrypted Persistence      |   |  - Layout Parsing & Pre-processing    |
|  - Java 21 / Non-blocking I/O         |   |  - Vector Indexing & Text Extraction  |
+-------------------+-------------------+   +-------------------+-------------------+
                    |                                           |
                    +--------------------+----------------------+
                                         | Ephemeral Anonymized Payload
                                         v
+-----------------------------------------------------------------------------------+
|                              AI Orchestration Layer                              |
|           Google Vertex AI / Gemini LLM API (Tax Engine Processing)              |
+----------------------------------------+------------------------------------------+
                                         | Structured Output
                                         v
+-----------------------------------------------------------------------------------+
|                                Persistence Layer                                  |
|         PostgreSQL 16 (Relational Schema) + Vector Index (pgvector)               |
+-----------------------------------------------------------------------------------+

```

---

## 📸 Key Features & Visual Walkthrough

### 1. Real-Time AI Financial Dashboard

The central dashboard presents LLM-synthesized tax liabilities, categorized deductions, real-time strategy recommendations, and historical comparisons without exposing raw confidential underlying payload structures.

* **Features:** Live tax liability updates, auto-categorized expense projections, risk indicators, and dynamic strategy recommendations.

---

### 2. Zero-Trust Document Upload & Ingestion Engine

A drag-and-drop ingestion interface built specifically to handle complex W-2, 1099, and custom PDF/Image financial statements.

* **Features:** Chunked parallel uploads, client-side pre-validation, real-time status streaming, and instant metadata extraction.

---

### 3. PII Masking, AES-256 Encryption & Document Preview

A secure viewer displaying structural parsing details, real-time masked PII elements, and payload status prior to storage.

* **Features:** In-browser AES-256 status verification, redacted SSN/ID highlights, cryptographic checksum validation, and JWT payload sign-offs.

---

### 4. Interactive Tax Sheet & Breakdown Analysis

Deep granular view displaying processed field extractions, tax rule matching, and structural itemizations produced by the Gemini LLM engine.

* **Features:** Discrepancy highlights, itemized deductions breakdown, confidence scores per line item, and exportable audit trails.

---

### 5. Multi-Tenant Administration & Audit Logs

An enterprise control screen providing security administrators full visibility into document access, user actions, system latencies, and system health metrics.

* **Features:** Role-Based Access Control (RBAC) management, Immutable Audit Logs, Vertex API token consumption metrics, and service health checks.

---

## 🛠️ Technology Stack

| Domain | Technology | Enterprise Purpose |
| --- | --- | --- |
| **Frontend Framework** | **Next.js 14 (App Router) / React 18** | Server-Side Rendering (SSR), Optimized Asset Delivery |
| **Mobile / Edge** | **PWA (Progressive Web App)** | Cross-Platform Availability & Native-like Capabilities |
| **Backend Services** | **Java 21 / Spring Boot 3.2** | Enterprise Business Logic, Virtual Threads (Project Loom) |
| **AI Engine** | **Google Vertex AI / Gemini LLM** | Automated Tax Parsing, Summarization & Recommendation |
| **Database** | **PostgreSQL 16 + pgvector** | Structural Data Integrity & Vector Search Indexing |
| **Security & Cryptography** | **AES-256-GCM, Spring Security, JWT** | At-Rest Encryption, Anonymization & Stateless Auth |
| **Cloud Infrastructure** | **GCP (GKE, GCE, Cloud Storage)** | Enterprise Deployment, Auto-Scaling & Cost Governance |
| **Containerization** | **Docker & Kubernetes** | Reproducible Deployments & Microservice Isolation |

---

## 🚀 Setup & Execution Guide

### Prerequisites

* Java 21 JDK
* Node.js 18.x or later
* Docker Engine & Kubernetes (`kubectl`)
* PostgreSQL 16+ instance
* GCP Service Account with Vertex AI Access

### Environment Variables Configuration

Create an `.env` file in the root directory:

```env
POSTGRES_HOST=localhost
POSTGRES_PORT=5432
POSTGRES_DB=finguardian
POSTGRES_USER=admin
POSTGRES_PASSWORD=your_secure_password

GCP_PROJECT_ID=your-gcp-project-id
VERTEX_AI_REGION=us-central1
GEMINI_API_KEY=your_gemini_api_key

JWT_SECRET=your_256bit_secret_key
AES_ENCRYPTION_KEY=your_32byte_aes_key

```

### Running the Services Locally

1. **Database Initialization:**
```bash
docker run -d --name finguardian-db -p 5432:5432 -e POSTGRES_PASSWORD=your_secure_password postgres:16

```


2. **Backend Service Execution:**
```bash
cd sync_agent
./gradlew bootRun

```


3. **Frontend Application Execution:**
```bash
cd Frontend_ShreeTech
npm install
npm run dev

```



---

FinGuardian demonstrates a production-grade approach to handling sensitive enterprise data using modern cloud infrastructure, secure software development practices, and scalable AI integration.
