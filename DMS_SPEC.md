# 🦆 DGCP Metadata Standard (DMS) — Specification v1.0.0

The **DGCP Metadata Standard (DMS)** defines the minimal, verifiable structure
required to create a **Real-Work Proof (RWD)** inside the DGCP™ protocol.

The DMS ensures **authenticity, integrity, privacy, and global auditability**
while remaining accessible to low-income and low-infrastructure environments.

DMS v1.0.0 is the *canonical, human-first specification* for all future DGCP Proofs.

---

# 1. Core Principles

### **1. Human-First**
The worker—not the machine—is the source of truth.  
DGCP rejects IoT, biometric, surveillance, and ML scoring systems.

### **2. Minimal Technology**
DGCP limits the technology stack to:

> **Phone → Metadata → IPFS → GitHub SHA256 → Minimal DLT Timestamp**

This avoids infrastructure barriers and preserves global accessibility.

### **3. Integrity via Open Cryptography**
No proprietary hardware or closed systems.  
All integrity comes from content addressing, cryptographic signatures,  
and public append-only registries.

### **4. Privacy by Default**
No GPS, no PII, no exact coordinates.  
Only coarse, human-readable location labels.

---

# 2. DMS v1.0.0 Schema Overview

The DMS file is a single JSON or YAML object.  
It is divided into four sections:

| Section | Role | Criticality |
|--------|------|-------------|
| **A. Core & Signature** | Identity + Versioning | Machine-Critical |
| **B. Context & Time** | When + Where | Hybrid |
| **C. Activity & Media** | What + Evidence | Hybrid |
| **D. Registry & Audit** | Proof Chain Linking | Machine-Critical |

---

# 3. Section A — Core & Signature (Machine-Critical)

These fields MUST pass the automated DGCP Metadata Validator.

| Field | Type | Constraint | Purpose |
|-------|------|------------|----------|
| `dms_version` | String | MUST be `"1.0.0"` | Version compatibility |
| `proof_id` | String (UUID) | Unique | Identifies this Proof event |
| `worker_id_public` | String | Public key | Pseudonymous human identity |
| `signature` | String | Signature of metadata (excluding this field) | Guarantees authenticity and integrity |

**Signature Rule:**  
The worker signs the canonical JSON/YAML representation of the metadata  
(without the `signature` field).  
This ensures the Proof cannot be altered after signing.

---

# 4. Section B — Context & Time (Hybrid)

Machine-critical + human-interpretive fields.

| Field | Type | Criticality | Purpose |
|-------|------|------------|----------|
| `timestamp_utc` | ISO 8601 | Machine-Critical | Global ordering of Proofs |
| `timestamp_local` | ISO 8601 + offset | Human-Interpretive | Human-readable context |
| `location_label` | String | Human-Interpretive | Coarse location (no GPS) |
| `work_type` | String | Human-Interpretive | Category from DGCP controlled vocabulary |

**Notes:**  
- `location_label` MUST NOT include coordinates.  
- `work_type` MUST align with DGCP vocabulary (e.g., `duck_care`, `field_maintenance`).  

---

# 5. Section C — Activity & Media (Hybrid)

These fields provide human-readable truth + cryptographic evidence.

| Field | Type | Criticality | Purpose |
|-------|------|------------|----------|
| `short_human_description` | String (≤ 256 chars) | Human-Interpretive | Worker’s own words |
| `tags` | Array of Strings | Human-Interpretive | Weather, tools, context |
| `ipfs_cid_primary` | CID v1 | Machine-Critical | Immutable Proof-of-Work media |
| `ipfs_cid_additional` | Array<CID> | Optional | Secondary evidence |

**Anti-AI Fabrication Rule:**  
`short_human_description` is required because  
AI cannot reliably fabricate consistent human-context language.

---

# 6. Section D — Registry & Audit (Machine-Critical)

These fields link the Proof into the global DGCP Proof Chain.

| Field | Type | Constraint | Purpose |
|-------|------|------------|----------|
| `git_repo_url` | URL | Public repo | Where the metadata is stored |
| `git_commit_sha256` | SHA256 | Commit hash | Immutable provenance |
| `ots_timestamp_ref` | TXID / proof URL | OTS/Bitcoin time-stamp | Global verifiability |

These three fields anchor the Proof in:

- **GitHub append-only history**
- **Cryptographic commit chain**
- **Minimal DLT (OTS/Bitcoin)** global timestamp

---

# 7. Validation Model

## 7.1 Machine Check (Automated)
The DGCP Metadata Validator checks:

- Required fields  
- Field types + formats  
- Signature validity  
- IPFS CID format  
- Version compliance  

This ensures **integrity**, not meaning.

## 7.2 Human Audit (Federated Groups)
Humans interpret:

- The truth of the work  
- Consistency with weather, season, tools  
- Worker narrative  
- Ethical context  

This ensures **truth**, not machine pattern scoring.

---

# 8. Versioning

DMS follows Semantic Versioning:

- **MAJOR** — breaking changes (affects Machine-Critical fields)  
- **MINOR** — non-breaking changes (add optional fields)  
- **PATCH** — clarifications / corrections  

DMS v1.x MUST always remain backward-compatible for all Proofs already committed.

---

# 9. Summary

DMS v1.0.0 is:

- **Minimal**  
- **Human-First**  
- **Cryptographically strong**  
- **Globally auditable**  
- **Privacy-safe**  
- **Low-infrastructure friendly**  

This document defines the foundation of the DGCP Proof Chain and  
forms the basis for all global adoption of Real-Work Proof (RWD).

---

# © DGCP™ – Human-Proof Protocol
Maintained by **MaMeeFarm™**, Lampang, Thailand  
Origin of the world’s first Real-Work Data System (RWD)
