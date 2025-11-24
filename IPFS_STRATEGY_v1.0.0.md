# 🦆 DGCP™ IPFS Strategy v1.0.0  
### Minimal, Immutable, Content-Addressed Storage for Real-Work Data (RWD)

This document defines the official IPFS storage strategy used by the  
DGCP Proof Chain. It ensures that every Proof Artifact (photo/video)  
is stored in a way that is:

- Immutable  
- Content-addressed  
- Censorship-resistant  
- Verifiable across jurisdictions  
- Affordable for low-income workers  

This strategy is optimized for **Human-Origin Data**, not IoT or high-volume streams.

---

## 1. Purpose of the IPFS Strategy

The IPFS layer ensures that every Proof Artifact has:

### ✔ A permanent, content-based identity  
### ✔ Zero dependency on centralized servers  
### ✔ A CID that changes with even one-pixel difference  
### ✔ A link that can be verified anywhere on Earth  

The goal is long-term verifiability and future-proof governance.

---

## 2. Required Format: CID v1 (Base32)

All DGCP Proof Artifacts **must** be pinned as **CID v1 Base32**,  
because it is:

- URL-safe  
- More compatible with modern gateways  
- Better for long-term standardization  
- Clearer for machine parsing  

CID v0 may appear from legacy tools, but CID v1 is the canonical format.

---

## 3. Upload & Pinning Rules

### 3.1. Required Fields from DMS
Every IPFS upload must produce:

ipfs_cid_primary

Optional supporting media (multi-angle, longer videos, sensor-free evidence)  
may produce:

ipfs_cid_additional[]

---

## 4. IPFS Upload Pipeline (Minimal)

The upload pipeline is intentionally simple:

Worker Phone → IPFS Upload (Pinata) → CID returned → Stored in DMS

### Why simple?  
Because complexity harms low-income workers.

DGCP rejects:
- IPFS clusters  
- Enterprise pinning networks  
- Automated IoT ingestion  
- Large-volume satellites  

**One phone + one gateway** is sufficient for cryptographic truth.

---

## 5. Pinning Requirements

To ensure long-term persistence:

| Layer | Requirement | Why |
|------|-------------|-----|
| Pinata | MUST pin | Worker affordability + reliability |
| GitHub | SHOULD reference CID | Public discovery + audit |
| Community Nodes | OPTIONAL | Federation improves redundancy |

DGCP Proofs do **not** rely on private servers.

---

## 6. File Type & Compression Guidelines

Workers must not alter media with heavy compression or editing tools.

Allowed:
- Native phone photos (JPEG/PNG)  
- Native phone videos (MP4)  

Forbidden:
- AI-edited images  
- Filters that alter the underlying scene  
- Recompression pipelines  
- Metadata-injected watermarks  

Reason:  
**Preserve the integrity of Real Work visual truth.**

---

## 7. File Naming Convention (Recommended)

DGCP recommends—but does not require—the following pattern:

Proof_<proof_id><worktype><YYYYMMDD_HHMM>.jpg

Naming is helpful for humans, but **CID is the source of truth**.

---

## 8. How IPFS Guarantees Integrity

| Layer | Guarantee |
|------|-----------|
| Hashing | Every byte is hashed into a content fingerprint |
| Content Addressing | File is located by cryptographic identity |
| Tamper Detection | Any change → New CID |
| Decentralization | Anyone can pin + verify, zero platform control |
| Gateway Agnostic | Works across gateways (Pinata, web3.storage, local node) |

This makes IPFS the most fair, open, and censorship-resistant solution  
for low-income labor documentation.

---

## 9. Why Not Use Private Storage, Cloud Buckets, IoT Streams?

Because they violate DGCP principles:

- They centralize control  
- They increase risk of deletion  
- They require trusted administrators  
- They enable silent modification  
- They cost money that workers cannot afford  

IPFS is the only viable long-term solution.

---

## 10. Forward Compatibility

All future versions of DGCP must preserve:

- CID v1 usage  
- Content-addressed immutability  
- Gateway neutrality  
- No requirement for high-bandwidth networks  
- No machine-reliant ingestion  

New versions may only add:
- optional fields  
- optional metadata  
- optional replication layers  

They may never remove the minimal structure.

---

## 11. License

This document is governed by:  
**MMFARM-POL-2025 License**  
Compatible with **CC BY-NC 4.0**.

