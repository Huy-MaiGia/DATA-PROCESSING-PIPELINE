⚙️ #DATA-PROCESSING-PIPELINE
Data Transformation: From Uncleaned Excel Records to Uniform Audit Formats.

📖 Project Overview
In corporate environments, data arrives in fragmented Excel sheets that require specific "Actions" (like DELETEADD) before they can be uploaded to a master registry. This project provides a Python-based ETL pipeline that reads raw company data, identifies interview records, and generates a multi-sheet output formatted for high-accuracy data migration.

🛠️ Tools & Technologies
Language: Python 3.x

Core Library: Pandas (for high-speed DataFrame manipulation)

File Handling: Openpyxl / XlsxWriter

Environment: Jupyter Notebook

🎯 The Problem
Manual data entry for large-scale registries is:

Time-Consuming: Restructuring one row into multiple audit-compliant rows takes minutes per record.

Error-Prone: Human copy-pasting often leads to inconsistent "Duns Number" formatting or missing audit trail timestamps.

Inflexible: Hardcoded metadata (like "Source of Information" notes) is tedious to apply across thousands of rows.

💡 The Solution
The script implements a logic-driven expansion engine:

Conditional Processing: It scans the 'Interview result' column. If a result exists, it triggers a transformation.

Row Expansion: For every one valid input row, it generates two distinct output rows:

Row 1: The "Data Row"—contains the mapping of Duns Numbers, names, and results with a DELETEADD tag.

Row 2: The "Audit Row"—appends standardized bilingual (English/Vietnamese) source notes and local registry office timestamps.

🏗️ How the Pipeline Works
1. Data Ingestion
The script utilizes pd.read_excel() to load the source file (VNM.xlsx).

2. The Transformation Loop
It iterates through the DataFrame using a custom logic block:

Python
if pd.notna(row['Interview result']):
    # Logic for generating formatted 'Data Row'
    # Logic for generating bilingual 'Source/Audit Row'
3. Output Generation
Instead of overwriting data, the pipeline uses a pd.ExcelWriter to create a new file (processed_data.xlsx) with organized tabs:

Original Data: A mirror of the input for verification.

New Rows: The final, processed, and expanded dataset ready for upload.

⚠️ Limitations & Future Scope
Static File Names: Currently hardcoded to VNM.xlsx. Future versions could utilize a file picker or CLI arguments.

Hardcoded Timestamps: The audit row uses a static date (18/10/2024). This could be updated to pull the datetime.now() dynamically.

Validation: Future iterations could include a Duns Number format validator to ensure data integrity before the DELETEADD action.
