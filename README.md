# Automated MAP Compliance & Violation Notice Pipeline

An automated data pipeline and reporting system built in Python to monitor e-commerce marketplace listings, identify Minimum Advertised Price (MAP) violations, and programmatically compile and dispatch formal PDF compliance notices.

---

## Business Problem & Context
In multi-channel e-commerce ecosystems, third-party sellers frequently discount products below authorized price floors (Lowest Permissible Price / LPP). Unchecked violations erode brand value, trigger partner disputes, and reduce overall profit margins. 

Auditing thousands of SKUs and manually drafting enforcement notices is slow and prone to administrative error. This project automates the entire detection, variance calculation, and multi-document generation workflow.

---

## Key Features
* Automated Audit & Filtering: Ingests e-commerce pricing logs across marketplaces (such as Amazon and Snapdeal) and extracts non-compliant listings where advertised_price < LPP.
* Variance Deficit Computation: Calculates exact price variance (price_diff = LPP - advertised_price) to assess violation severity.
* Dynamic PDF Notice Generation: Uses the ReportLab engine to compile formal, standardized violation notices populated with seller details, SKU, product line, timestamps, and required actions.
* Batch Document Dispatch: Iterates through identified violation records to generate individualized PDFs and interfaces with system-level commands (os.startfile) for instant verification.

---

## Tech Stack
* Language: Python
* Data Manipulation: pandas
* Document Compilation: ReportLab
* Environment: Jupyter Notebook

---

## Pipeline Workflow

1. Data Ingestion & Cleaning:
   Load marketplace audit data and inspect listing price versus authorized LPP thresholds.
   
2. Deficit Calculation:
   Compute the margin difference and structure the active violation dataset.

3. Programmatic PDF Assembly:
   Iterate over flagged records using iterrows(). Dynamically draw text, metadata, and compliance deadlines onto structured ReportLab canvas objects.

4. Automated Verification:
   Persist distinct, serialized PDF files (MAP_notice_{index}_{seller}_{sku}.pdf) and trigger local system preview for immediate audit logging.

---

## Sample Violation Notice Output

Each generated PDF notice includes:
* Notice Identifier & Date: Audit timestamp and serialized tracking ID.
* Target Partner: Offending seller name and target sales channel/region.
* Violation Specifications: Product SKU, product line, authorized LPP ($), advertised listing price ($), and calculated deficit ($).
* Corrective Action Window: Formal 24-hour price rectification and response terms.

---
