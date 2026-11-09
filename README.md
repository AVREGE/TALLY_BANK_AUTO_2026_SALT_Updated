# Tally Bank Statement Importer — License Ledger & Update Distribution Hub

Centralized administrative repository hosting the remote license verification database (`ldb.json`) and automated release distribution feeds for the **Universal Bank Statement Importer for Tally Prime**.

---

## 📥 Prerequisites & Setup Guide

### 1. Tesseract OCR Setup (Mandatory for Scanned Statements)
To enable OCR recognition for scanned bank statements, install the official Windows 64-bit engine:
* **Download Installer:** [Tesseract OCR v5.4.0 (Windows 64-bit)](https://digi.bib.uni-mannheim.de/tesseract/tesseract-ocr-w64-setup-5.4.0.20240606.exe)
* **Installation Path:** Keep the default installation directory:
  ```text
  C:\Program Files\Tesseract-OCR\
  ```

### 2. Tally Prime Configuration
Before importing vouchers:
1. Open your target company in **Tally Prime**.
2. Ensure the ODBC server is enabled on Port 9000:
   * Navigate to: `F1: Help` ➔ `Settings` ➔ `Connectivity` ➔ `Client/Server configuration`
   * Set **TallyPrime acts as**: `Both`
   * Set **Port**: `9000`

### 3. Running the Importer
1. Download the latest release binary:  
   👉 [Download Tally_Bank_Statement_Import_V1.exe](https://github.com/AVREGE/TALLY_BANK_AUTO_2026_SALT_Updated/releases/latest/download/Tally_Bank_Statement_Import_V1.exe)
2. Double-click **`Tally_Bank_Statement_Import_V1.exe`** to launch the application.

---

## 📺 Workflow Demo

Watch the fast integration workflow:

https://github.com/user-attachments/assets/dc1ac41e-9c64-48e8-828f-0caf0e836ca5

### Demonstrated Steps:
1. Open Target Company in Tally Prime (ODBC Port 9000).
2. Select Bank Routing Profile & Target Bank Account.
3. Browse and parse bank statement PDF.
4. Review extraction totals and stream vouchers directly to Tally Prime.

---

## 📌 Repository Overview

This repository acts as the cloud infrastructure backend for the desktop client executable:

- **Remote License Ledger (`ldb.json`)**: Synchronizes client installations, hardware UUIDs, subscription validity tokens, and trial expirations across machines to prevent local trial tampering.
- **Auto-Update Delivery (`latest.json`)**: Serves update manifests containing the latest application version tag, release binary download targets, and SHA-256 integrity checksums for seamless in-app client updates.
- **Release Artifacts**: Hosts compiled standalone application builds (`Tally_Bank_Statement_Import_V1.exe`).

---

## 📂 Core Files & Structure

| File | Purpose |
| :--- | :--- |
| `ldb.json` | Hardware-bound customer licensing ledger updated securely via GitHub REST API endpoints. |
| `latest.json` | Auto-update discovery manifest consumed by client instances on launch. |
| `tally_bank_config.yaml` | Application configuration defaults for voucher numbering and routing. |
| `README.md` | Repository documentation, setup instructions, and deployment runbook. |

---

## ⚙️ Administrative Deployment Workflow

### 1. Releasing a Client Build Update
When a new version is compiled using `build_bank_importer.bat`:
1. Locate the generated output inside your local `Github_Upload/` directory:
   * `Tally_Bank_Statement_Import_V1.exe`
   * `latest.json`
2. Update the `latest.json` file in the root of the `main` branch with the new version and SHA-256 hash.
3. Navigate to **Releases** ➔ **Draft a new release**:
   * **Tag version**: `v<VERSION>` (e.g., `v1.0.0`)
   * **Release title**: `Tally Bank Statement Importer v<VERSION>`
   * Attach `Tally_Bank_Statement_Import_V1.exe` as the binary release asset.
4. Click **Publish release**. Connected client apps will detect the new release and offer an automatic in-place upgrade.

### 2. Client License Management
- Active customer licenses and trial records are automatically registered under their unique **Hardware ID (HWID)** inside `ldb.json`.
- Activation keys are generated offline using `Generate_Bank_License_GUI.py` and validated cryptographically by client machines.

---

## 🔒 Security Notice
The contents of `ldb.json` contain hardware identification hashes and license statuses. Direct write access is restricted to authorized personal access tokens (PAT) managed by the system administrator.
