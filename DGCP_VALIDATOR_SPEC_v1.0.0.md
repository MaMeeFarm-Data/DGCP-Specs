# 🦆 DGCP Metadata Validator Specification v1.0.0  
### Machine-Critical Validation Standard for Real-Work Proofs (RWD)

This document defines the **official, canonical specification** for the  
DGCP Metadata Validator — the lightweight, open-source software that  
checks all **Machine-Critical** fields in the DMS before a proof enters  
the Global Proof Registry (GPR).

This validator enforces structural integrity, cryptographic authenticity,  
and metadata correctness **without** interpreting human meaning.

---

# 1. Purpose of the Validator

The DGCP Validator exists to:

1. Verify the metadata is structurally correct  
2. Confirm cryptographic signatures from workers  
3. Ensure IPFS CIDs and Git SHA256 hashes are valid  
4. Guarantee the DMS version is correct and compatible  
5. Prepare the metadata for append-only registry inclusion  

**The Validator does NOT evaluate:**

- truth  
- meaning  
- context  
- quality of labor  
- classification of human work  
- AI-based scoring of any kind  

These are exclusively governed by the **Federated Human Audit (FHA)**.

---

# 2. Inputs & Outputs

## Input
- A single DMS metadata file (JSON/YAML)
- Worker’s public key (embedded in metadata)
- Optional: local validator configuration

## Output
- PASS (metadata is valid)  
- FAIL (metadata violates Machine-Critical rules)  
- Signed validation report (optional per region)

---

# 3. Validation Steps (Strict Order)

The Validator follows a **deterministic, reproducible** sequence:

---

## Step 1 — Structural Format Check
Ensures metadata conforms to JSON/YAML syntax.

Fails if:
- malformed JSON/YAML  
- missing required fields  
- unexpected top-level structure  

---

## Step 2 — DMS Version Check
Reads:

dms_version: "1.0.0"

Fails if:
- version mismatch  
- unsupported or deprecated version  

Versioning ensures **forward compatibility** while protecting older proofs.

---

## Step 3 — Machine-Critical Fields Check
Validator confirms presence + type correctness:

| Field | Requirement |
|---|---|
| dms_version | MUST match canonical version |
| proof_id | MUST be UUIDv4 or valid unique ID |
| worker_id_public | MUST match allowed key formats |
| signature | MUST be valid length & format |
| timestamp_utc | MUST be valid ISO8601 |
| ipfs_cid_primary | MUST match CID v1/v0 format |
| git_repo_url | MUST be valid URL |
| git_commit_sha256 | MUST be 40–64 hex chars |

Fails if any field violates DMS rules.

---

## Step 4 — Cryptographic Signature Verification
The Validator recomputes the metadata hash (excluding the `signature` field)  
and verifies it with:

- `worker_id_public`  
- the provided `signature`  

Fails if:
- signature is invalid  
- hash mismatch  
- malformed key  

This step guarantees **human-origin authenticity**.

---

## Step 5 — IPFS CID Format Check
Performs format-level validation (not network fetch):

- Ensures CID syntax  
- Ensures no tampering  
- Ensures compatibility with IPFS pinning nodes  

Fails if CID is malformed.

---

## Step 6 — Git SHA256 Format Validation
Ensures correct hex format and length.

This is used later for global chronology tracking and SHA256 anchoring.

---

## Step 7 — Optional Minimal DLT Reference Check
If `ots_timestamp_ref` exists:

- MUST be valid OTS/Bitcoin TXID/attestation reference  
- MUST match allowed formats  

Not required for all proofs (depends on daily GitHub anchoring).

---

# 4. What the Validator MUST Never Do

To protect DGCP's Human-First nature:

The Validator MUST NEVER:

- interpret human descriptions  
- classify the meaning of work  
- score quality of labor  
- use AI/ML to “judge” content  
- evaluate photos/videos  
- fetch or analyze IPFS files  
- reject or accept proofs based on human content  

This is strictly forbidden.

All content meaning and truth is handled by humans.

---

# 5. Security Model

The Validator must be:

- deterministic  
- open-source  
- reproducible  
- portable  
- lightweight (runs on basic VPS or low-end machines)  
- vendor-neutral  
- audit-friendly  

It must NEVER require:

- IoT  
- biometric identity  
- surveillance inputs  
- GPU or ML hardware

---

# 6. Implementation Requirements

Minimum recommended stack:

- Python, Rust, Go, or TypeScript implementations  
- No external telemetry  
- No cloud lock-in  
- Local-only cryptographic operations  
- No auto-updates without explicit version control  

---

# 7. Governance & Updates

- Updates must be versioned (e.g., v1.0.1, v1.1.0, v2.0.0)  
- Changes must NEVER alter historical proofs  
- Changes must be approved by Federated Human Audit governance  
- Backward compatibility is mandatory for all minor versions  
- Validator cannot mutate stored metadata  

---

# 8. License

The DGCP Validator Specification is governed by the  
**MMFARM-POL-2025 License** with a CC BY-NC 4.0 compatibility layer.

