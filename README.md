# SoftOne ERP Automations & Scripting Archive

A centralized repository of production-ready automations, custom business scripts, and enterprise integration tools designed for **SoftOne ERP** (the market-leading ERP platform in Greece and SE Europe).

---

### 📌 Architecture & Scope
This repository houses ERP tooling across two complementary operational paradigms:

#### 1. In-Process Automation (Embedded SBSL Scripts)
- **Runtime:** Executed directly within the embedded **SoftOne Script Editor**.
- **Scope:** Lightweight, fast, event-driven scripts (`OnPost`, `BeforePost`, `FieldChange`) written in SoftOne Basic Scripting Language (SBSL) and embedded SQL.
- **Purpose:** Immediate workflow optimization, automated business rules, accounting data validation, tax recalculations, and bulk record processing directly inside the ERP client without requiring external runtime dependencies.

#### 2. Out-of-Process Integrations (`Softone.Lib.dll` / External Daemons)
- **Runtime:** Standalone external applications, background CLI tools, and automated pipelines (.NET / C# / Python).
- **Scope:** Headless integration using the official **`Softone.Lib.dll`** (SoftOne COM / API Object Model).
- **Purpose:** Scheduled unattended batch processing, automated synchronization between third-party systems/APIs and SoftOne, bulk Excel/CSV data imports, and automated database reconciliation.

---

### 📂 Repository Modules

| Module Directory | Type | Description | Key Assets |
| :--- | :---: | :--- | :--- |
| **[`update_vat_in_softone/`](./update_vat_in_softone)** | **In-Process (SBSL)** | Automated batch update of VAT categories across commercial inventory items using external Excel sheets. Features automated error checking, rollback safeguards, and real-time execution feedback. | • `UpdateFPA3.txt` (SBSL Script)<br>• `UpdateVat.xlsx` (Data Template)<br>• Video Walkthrough & Demo |

---

### 🛠️ Technologies & Ecosystem
- **Platform:** SoftOne ERP (Series 5 / 6)
- **Languages:** SoftOne Basic Scripting Language (SBSL), Transact-SQL (T-SQL)
- **API & Libraries:** `Softone.Lib.dll` (SoftOne API / COM Interop)
- **Data Formats:** Excel (`.xlsx`), CSV, JSON
