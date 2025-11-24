# 🦆 DGCP™ Global Proof Registry (GPR) Specification v1.0.0  
### Canonical Specification for Append-Only, Public, Immutable Proof History

The Global Proof Registry (GPR) is the **public, append-only ledger**  
that stores every DGCP proof’s metadata history.  
It serves as the global backbone of **truth, chronology, and auditability**.

This specification defines how the GPR is structured, updated, anchored,  
and verified.

---

# 1. Purpose of the Global Proof Registry (GPR)

The GPR ensures:

1. **Global Transparency** — Any proof can be verified by anyone  
2. **Immutable History** — No deletion or rewriting of records  
3. **Chronological Integrity** — Every proof tied to a real moment in time  
4. **Public Accessibility** — Hosted on public Git repositories  
5. **Auditability** — Readable by regulators, researchers, NGOs, journalists  

The GPR is the **truth layer** of DGCP.

---

# 2. Registry Architecture

The GPR operates on a **4-layer structure**:

| Layer | Purpose | Technology |
|---|---|---|
| Layer 1 | Proof Metadata | DMS file (JSON/YAML) |
| Layer 2 | GitHub Commit History | SHA256 commit hash |
| Layer 3 | Daily SHA256 Root Hash | Aggregated snapshot |
| Layer 4 | Minimal DLT Timestamp | OTS / Bitcoin TXID |

This pipeline ensures:  
**Phone → Metadata → GitHub → Global Clock**

---

# 3. Append-Only Commit Rules

The GPR is strictly append-only.

Therefore:

- No Git rebase  
- No history rewriting  
- No deletion of commits  
- No force-push allowed  
- Fixes must be new commits (“correction entries”)  

If a mistake happens → it becomes part of the permanent record  
(and corrected via a new metadata entry).

This protects the worker from coercion and manipulation.

---

# 4. Repository Structure

Recommended structure:

/proofs/
YYYY/
MM/
proof_<id>.json
proof_<id>.yaml (optional)
/daily_roots/
YYYY-MM-DD-root.json
/ots/
YYYY-MM-DD.ots (or .txt for TXID)
/registry_index/
index.json (optional for auditors)

This structure must be:

- simple  
- predictable  
- machine-readable  
- long-term safe  
- compatible with future scaling  

---

# 5. Daily SHA256 Root Hash Generation

Every 24 hours:

1. List all commits for that day  
2. Extract commit SHA256 for each proof  
3. Combine into a deterministic array  
4. Compute a Merkle-like root hash  
5. Save as:

daily_roots/YYYY-MM-DD-root.json

Fields:

| Field | Description |
|---|---|
| date | UTC date |
| commit_hashes | List of commit SHA256 hashes |
| root_sha256 | Final SHA256 of the aggregated structure |

This becomes the "day fingerprint".

---

# 6. Minimal DLT Timestamp (OTS / Bitcoin)

To achieve **global provability**, each day’s root hash is anchored:

### Acceptable methods:
- OpenTimestamps (OTS)
- Bitcoin OP_RETURN transaction
- Equivalent minimal attestation chain

### Required stored fields:
| Field | Purpose |
|---|---|
| txid / ots_file | Global clock proof |
| root_sha256 | Exact hash anchored |
| timestamp_utc | When anchoring occurred |

Stored under:

/ots/YYYY-MM-DD.ots

or

/ots/YYYY-MM-DD.txt

This ensures:
**No one on Earth can falsify DGCP’s history after anchoring.**

---

# 7. Verification Workflow (External Auditor)

Any auditor can verify a proof in 4 steps:

### Step 1 — Verify DMS Metadata (local)
- Validate JSON structure  
- Validate signature with worker’s public key  

### Step 2 — Verify IPFS CID
- Hash the file  
- Confirm CID match  

### Step 3 — Verify GitHub Commit
- Find commit SHA256 in public repo  
- Confirm chronology  

### Step 4 — Verify Global Timestamp
- Compare daily root hash to OTS/Bitcoin anchor  
- Confirm root existed on-chain before timestamp  

This requires:
- No permission  
- No API keys  
- No proprietary software  
- Only open-source tools  

---

# 8. Governance & Access

The GPR must be:

- Public  
- Globally accessible  
- Free to read  
- Free to fork  
- Verifiable without DGCP servers  
- Resistant to deletion  

Multiple mirror repos are allowed.

Governments, universities, NGOs may mirror it publicly to preserve truth.

---

# 9. Security Requirements

- HTTPS-only Git repos  
- Never store private keys  
- No automatic merges without review  
- Daily roots and OTS files must be immutable once created  
- GPR must be reproducible from raw commit history  

---

# 10. License

Everything in the GPR is governed under:

**MMFARM-POL-2025 License**  
with **CC BY-NC 4.0** compatibility layer.

