# Quick Start Guide

Get this app running in under 30 minutes.

---

## Prerequisites

- Python 3.x installed
- Google account
- Basic terminal/command line knowledge

---

## Step 1: Install Dependencies (2 minutes)

```bash
cd "/Users/nicolopastrone/Desktop/Development Projects/generic-pricing-data-solution"
pip install -r requirements.txt
```

---

## Step 2: Set Up Google Cloud (10-15 minutes)

### Quick Checklist:
1. ☐ Go to [Google Cloud Console](https://console.cloud.google.com)
2. ☐ Create new project (e.g., "pricing-app")
3. ☐ Enable Google Sheets API
4. ☐ Enable Google Drive API
5. ☐ Create service account
6. ☐ Download JSON key
7. ☐ Copy service account email

**Need detailed steps?** See [docs/GOOGLE_SHEETS_SETUP.md](docs/GOOGLE_SHEETS_SETUP.md)

---

## Step 3: Create Google Sheet (5 minutes)

### Quick Checklist:
1. ☐ Create new Google Sheet
2. ☐ Name it exactly: `suppliers_demo`
3. ☐ Leave Row 1 empty
4. ☐ Add column headers in Row 2 (see below)
5. ☐ Paste sample data starting Row 3
6. ☐ Share with service account email as Editor

### Column Headers (Row 2):
```
Product ID | Product Name | Supplier | Category | Minimum Qty | Unit Cost (1-25) | Unit Cost (26-50) | Unit Cost (51-100) | Unit Cost (101-250) | Unit Cost (251-500) | Unit Cost (501-1000) | Unit Cost (1000+) | Branding Setup Fee | Label Cost per Unit | Label Minimum Qty | Description
```

### Sample Data:
Copy from [docs/SAMPLE_DATA_FOR_SHEET.md](docs/SAMPLE_DATA_FOR_SHEET.md) (CSV section at bottom)

---

## Step 4: Configure App (5 minutes)

### Create secrets.toml:
```bash
cp .streamlit/secrets.toml.example .streamlit/secrets.toml
```

### Fill in credentials:
1. ☐ Open the JSON key file you downloaded
2. ☐ Open `.streamlit/secrets.toml` in editor
3. ☐ Copy values from JSON to TOML (field by field)
4. ☐ Save file

**Important:** Keep `private_key` as one line with `\n` characters

---

## Step 5: Test & Run (2 minutes)

### Test connection:
```bash
streamlit run scripts/test_connection.py
```

**Expected:** ✅ Successfully connected message

### Run the app:
```bash
streamlit run app.py
```

**Expected:** App opens in browser with products loaded

---

## Troubleshooting

### "Failed to load data: [404]"
- Sheet not named `suppliers_demo` exactly
- Sheet not shared with service account

### "Failed to load data: [403]"
- Service account doesn't have Editor permission
- Share the sheet with the service account email

### "No such file: secrets.toml"
- Copy `.streamlit/secrets.toml.example` to `.streamlit/secrets.toml`
- Fill in your credentials

### Products not loading
- Check Row 1 is empty
- Check Row 2 has headers
- Check data starts Row 3
- Check Product ID column has values

**More help:** [docs/GOOGLE_SHEETS_SETUP.md](docs/GOOGLE_SHEETS_SETUP.md)

---

## Usage Overview

1. **Select Product** - Choose supplier and product
2. **Customize** - Enter quantity, markup %
3. **Add Labels** - Optional branding (checkbox)
4. **Add to Order** - Click button
5. **Repeat** - Add more products
6. **Set Order Settings** - Shipping, tariff, discounts
7. **Generate** - Proposals and invoices

---

## What's Next?

- Explore the app features
- Try multi-product orders
- Test discount calculations
- Generate proposals and invoices
- Download CSVs
- Save quotes to history

---

## Documentation

- **[README.md](README.md)** - Full documentation
- **[PORTFOLIO.md](PORTFOLIO.md)** - Project context
- **[docs/GOOGLE_SHEETS_SETUP.md](docs/GOOGLE_SHEETS_SETUP.md)** - Detailed Google setup
- **[docs/SAMPLE_DATA_FOR_SHEET.md](docs/SAMPLE_DATA_FOR_SHEET.md)** - Sample data

---

## Common Commands

```bash
# Run app
streamlit run app.py

# Test connection
streamlit run scripts/test_connection.py

# Install dependencies
pip install -r requirements.txt

# Update dependencies
pip install --upgrade -r requirements.txt
```

---

**Questions?** Check [README.md](README.md) troubleshooting section or [docs/GOOGLE_SHEETS_SETUP.md](docs/GOOGLE_SHEETS_SETUP.md)

**Last Updated:** 2025-10-07
