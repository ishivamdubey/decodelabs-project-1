# Project 1 — Data Cleaning & Preparation
**DecodeLabs Data Analytics Internship | Batch 2026**

## 🎯 Goal
Clean a raw e-commerce orders dataset (1,200 rows / 14 columns) by handling missing
values, duplicates, and inconsistent formatting — turning raw data into a
production-ready "gold standard" source of truth.

## 📁 Repository Structure
```
project1-data-cleaning/
├── data/
│   └── raw_dataset.xlsx           # Original, untouched raw data
├── scripts/
│   ├── clean_data.py              # Main cleaning pipeline (pandas)
│   └── generate_changelog_pdf.py  # Builds the stakeholder change-log PDF
├── output/
│   ├── cleaned_dataset.xlsx       # Final cleaned dataset (Excel)
│   ├── cleaned_dataset.csv        # Final cleaned dataset (CSV)
│   ├── change_log.csv             # Machine-readable change log
│   └── change_log.pdf             # Stakeholder-facing change-log report
├── requirements.txt
└── README.md
```

## 🧹 Cleaning Process

| Phase | What was done |
|---|---|
| **1. Strategic Imputation** | Identified missing values (309 blank `CouponCode` entries). Imputed with an explicit `"NONE"` category rather than deleting rows, to avoid the statistical-power loss caused by listwise deletion. Added a generic median/mode fallback for any other numeric/text nulls. |
| **2. Integrity Audit** | Checked for fully duplicated rows and duplicate `OrderID` values. Verified **0% duplicate rate** on the unique identifier. |
| **3. Standardize Formats** | Converted `Date` to ISO 8601 (`YYYY-MM-DD`); trimmed whitespace; applied consistent Title Case to categorical text fields (`Product`, `PaymentMethod`, `OrderStatus`, `ReferralSource`); standardized IDs/codes to uppercase; enforced 2-decimal precision on currency fields. |
| **4. Logical Validation** | Recomputed `TotalPrice = Quantity × UnitPrice` for every row and corrected any mismatches; flagged (without silently deleting) any non-positive quantity/price values. |

**Verification Gate (required by project brief):**
- ✅ 0% error rate on unique identifiers (`OrderID`)
- ✅ 0% error rate on date formats
- ✅ 0 remaining null values

## ▶️ How to Run
```bash
# 1. Install dependencies
pip install -r requirements.txt

# 2. Run the cleaning pipeline
cd scripts
python clean_data.py

# 3. Generate the stakeholder change-log PDF
python generate_changelog_pdf.py
```
Outputs are written to the `output/` folder.

## 🛠 Tech Stack
- Python 3
- pandas, numpy — cleaning & transformation
- openpyxl — Excel I/O
- reportlab — PDF report generation

## 📊 Dataset Overview
| Column | Description |
|---|---|
| OrderID | Unique order identifier |
| Date | Order date (ISO 8601) |
| CustomerID | Unique customer identifier |
| Product | Product purchased |
| Quantity | Units ordered |
| UnitPrice | Price per unit ($) |
| ShippingAddress | Delivery address |
| PaymentMethod | Payment method used |
| OrderStatus | Current order status |
| TrackingNumber | Shipment tracking number |
| ItemsInCart | Total items in cart at checkout |
| CouponCode | Coupon applied (`NONE` if not used) |
| ReferralSource | Marketing channel that drove the order |
| TotalPrice | `Quantity × UnitPrice` ($) |

## 👤 Author
Data Analyst Intern — DecodeLabs, Batch 2026

## 📄 License
This project is for educational/portfolio purposes as part of the DecodeLabs
Industrial Training Kit.
