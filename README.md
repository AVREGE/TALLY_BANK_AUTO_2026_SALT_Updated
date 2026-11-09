# Tally Bank Statement Importer — License Ledger & Update Distribution Hub

Centralized administrative repository hosting the remote license verification database (`ldb.json`) and automated release distribution feeds for the **Universal Bank Statement Importer for Tally Prime**.

---

## 📌 Repository Overview

This repository acts as the cloud infrastructure backend for the desktop client executable:

* **Remote License Ledger (`ldb.json`)**: Synchronizes client installations, hardware UUIDs, subscription validity tokens, and trial expirations across machines to prevent local trial tampering.
* **Auto-Update Delivery (`latest.json`)**: Serves update manifests containing the latest application version tag, release binary download targets, and SHA-256 integrity checksums for seamless in-app client updates.
* **Release Artifacts**: Hosts compiled, PyArmor-obfuscated standalone application builds (`Tally_Bank_Statement_Importer.exe`).

---

## 📂 Core Files & Structure

| File | Purpose |
| :--- | :--- |
| `ldb.json` | Hardware-bound customer licensing ledger updated securely via GitHub REST API endpoints. |
| `latest.json` | Auto-update discovery manifest consumed by client instances on launch. |
| `README.md` | Repository documentation and developer deployment runbook. |

---

## ⚙️ Administrative Deployment Workflow

### 1. Releasing a Client Build Update
When a new version is compiled using `build_bank_importer.bat`:
1. Locate the generated output inside your local `Github_Upload/` directory:
   * `Tally_Bank_Statement_Importer.exe`
   * `latest.json`
2. Update the `latest.json` file in the root of the `main` branch with the new version and SHA-256 hash.
3. Navigate to **Releases** ➔ **Draft a new release**:
   * **Tag version**: `v<VERSION>` (e.g., `v1.0.1`)
   * **Release title**: `Tally Bank Statement Importer v<VERSION>`
   * Attach `Tally_Bank_Statement_Importer.exe` as the binary release asset.
4. Click **Publish release**. Connected client apps will detect the new release and offer an automatic in-place upgrade.

### 2. Client License Management
* Active customer licenses and trial records are automatically registered under their unique **Hardware ID (HWID)** inside `ldb.json`.
* Activation keys are generated offline using `Generate_Bank_License_GUI.py` and validated cryptographically by client machines.

---

## 🔒 Security Notice
The contents of `ldb.json` contain hardware identification hashes and license statuses. Direct write access is restricted to authorized personal access tokens (PAT) managed by the system administrator.

## 📺 Workflow Demo

Watch the 10-second fast integration workflow:

<!-- Paste your dragged-and-dropped GitHub video link here -->
https://github.com/user-attachments/assets/your-video-link-here

### Demonstrated Steps:
1. Open Target Company in Tally Prime (ODBC Port 9000).
2. Select Bank Routing Profile & Target Bank Account.
3. Browse and parse bank statement PDF.
4. Review extraction totals and stream vouchers directly to Tally Prime.

https://github.com/user-attachments/assets/dc1ac41e-9c64-48e8-828f-0caf0e836ca5

