# SoftOne ERP Automations — Batch VAT Correction (SBSL Script)

An automated batch processing script written in **SBSL (SoftOne Scripting Language)** for **SoftOne ERP** (leading Greek ERP), designed to correct cents rounding discrepancies in supplier invoice VAT amounts using Excel input.

> 🇬🇷 **Ελληνική Έκδοση:** [Διαβάστε το README στα Ελληνικά εδώ](./README_GR.md)

---

### 📌 Business Context & Problem
During automated invoice logging or batch imports, system-calculated VAT values often introduce small cents rounding discrepancies (e.g., $\pm 0.01$ € or $\pm 0.02$ €) compared to the actual physical supplier invoice. Manually searching, locating, and editing each invoice in the ERP is extremely tedious, time-consuming, and prone to human error.

---

### 🚀 Key Features

- **Precise Invoice Identification:** Automatically queries and matches the exact database document (`FINDOC`) by combining:
  1. Transaction Date (`TRNDATE`)
  2. Document Reference Number / Series & Number (`INVOICE` / `cmpfincode`)
  3. Supplier Tax Identification Number (`SUPPLIERAFM` / Greek AFM)

- **Dynamic VAT Selector (1 Category per Run):**
  - Uses an integrated SoftOne selector linked directly to the system's `VAT` table, allowing the user to select any VAT category (default: `1410 - VAT 24%`).
  - **Invoices with Multiple VAT Rates:** The script processes one VAT category per execution. For invoices containing multiple VAT rates, simply run the script corresponding times (e.g., 2 or 3 runs), specifying the targeted VAT value in the Excel column and selecting the matching VAT rate in the selector for each run.

- **Live Progress Monitoring (Counters):**
  - **Current (Τρέχουσα):** The invoice record currently being checked in real time.
  - **Cancelled / Unmatched (Άκυρες):** Total count of Excel invoices that could **not be matched** in SoftOne.
  - **Total (Συνολικές):** Total number of records imported from the Excel spreadsheet.

- **Detailed Execution Logging (Transfer Messages):**  
  For each processed invoice row, the script outputs the invoice code, supplier Tax ID, and status:
  1. **Found & Already Accurate:**  
     `FPA did not need change, value is: [value]`
  2. **Found & Updated:**  
     `FPA changed from [old value] to [new value]`
  3. **Not Found in SoftOne:**  
     `Invoice Cancel: [invoice], Supplier: [AFM] ===============`

---

### 📊 Excel Input Specifications
The input Excel spreadsheet must contain the following 4 columns with the **exact header names**:
1. `TRNDATE`: Invoice date (formatted as `DD/MM/YYYY`).
2. `INVOICE`: Alphanumeric Document/Invoice Reference Number.
3. `SUPPLIERAFM`: Supplier Tax Identification Number (AFM).
4. `FPA`: The correct VAT amount to update.

> ⚠️ **Important:** Column headers must strictly match these exact names for the script to map fields correctly.

---

### 📁 Repository Structure
- `UpdateFPA3.txt`: The SBSL source script (Form & Import Job definition).
- `UpdateVat.xlsx`: Sample sanitized Excel template with sample input rows.
- `README_GR.md`: Documentation in Greek.

---

### 🛠️ Installation & Execution Guide
1. Launch **SoftOne ERP**.
2. Click the **Tools** icon (sidebar) and navigate to:  
   **S.D.K. ➔ Customization tools ➔ S1 Scripts ➔ New**.
3. **Copy and paste** the script code from `UpdateFPA3.txt`.
4. Provide a **Name** and **Description**, then save the script.
5. Click **Preview** to display the execution dialog form.
6. In the dialog:
   - Select your **Excel input file**.
   - Choose the targeted **VAT Category** from the dropdown selector.
7. Click **Run (Εκτέλεση)**.

> 💡 **Pro-Tip during execution:**  
> Whenever SoftOne updates an invoice, it prompts a confirmation dialog requiring an **Enter** (or OK) keystroke.  
> You can press the **Enter** key repeatedly ahead of time: SoftOne queues (buffers) keystrokes, instantly dismissing dialog popups without having to wait and click each one individually!
