Automated Transaction Reconciliation Tool (Side-by-Side Report)

📌 Project Overview
As a Financial Analyst, manual transaction reconciliation across multiple systems (ERP/Internal Ledger vs. Bank Statements) used to be a time-consuming and error-prone process. 

This project provides an automated, Python-based solution that performs a robust **three-way validation** (matching by **ID, Amount, and Status**) of financial data. It replaces tedious Excel manual matching with a scalable script that highlights discrepancies in a clean, user-friendly **Side-by-Side** layout.

💼 Business Problem
Manual reconciliation often leads to several pain points:
* High risk of human error when processing thousands of rows.
* Hard-to-spot mismatched details (e.g., matching IDs but differing amounts or statuses).
* Inefficient workflow caused by jumping between separate source files.

🛠️ Solution & Key Features
This script automates data pipeline steps using `pandas`:
1. **Data Standardization**: Automatically strips trailing spaces, normalizes statuses to lowercase, and rounds transaction amounts to 2 decimal places to prevent floating-point mismatches.
2. **Robust Multi-Key Join**: Uses an outer join approach to combine datasets without losing missing records.
3. **Automated Exception Detection**: Instantly filters and flags four types of errors:
   * **Amount Mismatches** (IDs match, but amounts differ).
   * **Status Mismatches** (IDs match, but transaction statuses differ).
   * **Missing in Bank** (Recorded internally, but not found in the bank statement).
   * **Missing in Ledger** (Unaccounted bank entries like hidden fees or direct deposits).
4. **Side-by-Side Excel Report**: Generates a consolidated output with two clean tabs (`All Discrepancies` and `Perfect Matches`), placing internal data next to bank data for immediate audit.

📁 Repository Structure
* `reconcile.py` — The core Python script containing the data cleaning and matching logic.
* `internal_ledger.xlsx` — Synthetic test data representing internal ledger/ERP records.
* `bank_statement.xlsx` — Synthetic test data representing bank statement records.
* `reconciliation_report_side_by_side.xlsx` — The final generated report.

🚀 How to Run the Project
1. Clone or download this repository.
2. Ensure you have `pandas` and `openpyxl` installed:
   ```bash
   pip install pandas openpyxl
   ```
3. Place your data files named `internal_ledger.xlsx` and `bank_statement.xlsx` in the project directory.
4. Run the script via your terminal or Jupyter Notebook cell:
   ```bash
   python reconcile.py
   ```

📊 Sample Output Format
The generated Excel sheet (`All Discrepancies`) structures mismatched data like this:

| ID (Internal System) | ID (Bank Statement) | Amount (Internal System) | Amount (Bank Statement) | Status (Internal System) | Status (Bank Statement) |
| :--- | :--- | :--- | :--- | :--- | :--- |
| TXN002 | TXN002 | 2700.50 | 2700.50 | success | declined |
| TXN003 | TXN003 | 500.00 | 450.00 | failed | failed |
| TXN004 | NaN | 9900.00 | NaN | success | NaN |

*Note: All data used in this project is entirely synthetic and created for demonstration purposes to protect corporate NDA.*
