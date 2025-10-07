# Generic Pricing & Quoting Solution

A Python/Streamlit application for managing multi-supplier tiered pricing, quotes, proposals, and invoices. Features dynamic pricing tiers, multi-product ordering, customizable markup, and professional document generation.

> **Note:** This is a portfolio/demo version with sample data. See [PORTFOLIO.md](PORTFOLIO.md) for more details.

**🌐 Live Demo:** [https://generic-pricing-data-solution.streamlit.app](https://generic-pricing-data-solution.streamlit.app)

**Status:** Production Ready | **Version:** 2.0 (Genericized Portfolio Version)

---

## Features

### Core Functionality
- **Multi-Supplier Support** - Manage products from multiple suppliers in one system
- **Tiered Pricing** - 7 quantity-based pricing tiers (1-25, 26-50, 51-100, 101-250, 251-500, 501-1000, 1000+)
- **Multi-Product Orders** - Add multiple products to a single order with independent configurations
- **Smart Pricing** - Automatic tier selection with intelligent fallback logic
- **Flexible Markup** - Per-product markup configuration with percentage-based calculation
- **Custom Branding** - Optional labels with minimum quantity enforcement and setup fees
- **Discount System** - Preset discounts (Wholesale, Volume, Partner) or custom discounts
- **Marketing Tools** - Charm pricing option (e.g., $60 → $59)
- **Custom Line Items** - Add unique services or customizations not in catalog

### Professional Outputs
- **Detailed Proposals** - Per-product tables with MOQ pricing
- **Professional Invoices** - 6-column format with line items and totals
- **Order Summaries** - Complete breakdown with all products and costs
- **CSV Downloads** - Export proposals, invoices, and order data

### User Experience
- **Order History** - Save and reload previous quotes
- **Edit & Update** - Modify products in cart before finalizing
- **Real-time Preview** - See pricing breakdowns as you customize
- **Minimum Qty Validation** - Warnings for orders below product minimums
- **Data Refresh** - Manual refresh option for latest supplier pricing

---

## Tech Stack

- **Language:** Python 3.x
- **Framework:** Streamlit
- **Data Source:** Google Sheets API
- **Authentication:** Google Cloud service account (gspread)
- **Data Processing:** pandas
- **Deployment:** Streamlit Cloud ready

---

## Quick Start

### 1. Install Dependencies
```bash
pip install -r requirements.txt
```

### 2. Configure Google Sheets Access

Create `.streamlit/secrets.toml`:
```toml
[gcp_service_account]
type = "service_account"
project_id = "your-project-id"
private_key_id = "your-private-key-id"
private_key = "-----BEGIN PRIVATE KEY-----\n...\n-----END PRIVATE KEY-----\n"
client_email = "your-service-account@your-project.iam.gserviceaccount.com"
client_id = "your-client-id"
auth_uri = "https://accounts.google.com/o/oauth2/auth"
token_uri = "https://oauth2.googleapis.com/token"
auth_provider_x509_cert_url = "https://www.googleapis.com/oauth2/v1/certs"
client_x509_cert_url = "your-cert-url"
```

**Important:** Never commit `.streamlit/secrets.toml` to version control (protected by .gitignore)

### 3. Set Up Data Source

Option A: **Use the demo sheet** (recommended for testing)
- The app expects a Google Sheet named `suppliers_demo`
- See [docs/DATA_STRUCTURE.md](docs/DATA_STRUCTURE.md) for required structure
- Demo sheet available at: [View Demo Sheet](https://docs.google.com/spreadsheets/d/YOUR_SHEET_ID)

Option B: **Create your own sheet**
- Copy the demo sheet structure
- Update the sheet name in `app.py` (line 340)
- Grant access to your service account email

### 4. Run the App
```bash
streamlit run app.py
```

### 5. Test Connection (Optional)
```bash
streamlit run scripts/test_connection.py
```

---

## Project Structure

```
generic-pricing-data-solution/
├── app.py                      # Main application
├── requirements.txt            # Python dependencies
├── README.md                   # This file
├── CLAUDE.md                   # Development guidelines
├── PORTFOLIO.md                # Portfolio context
│
├── .streamlit/
│   └── secrets.toml           # Google credentials (SECRET)
│
├── docs/                       # Documentation
│   ├── PLANNING.md            # Requirements & architecture
│   ├── DATA_STRUCTURE.md      # Data schema reference
│   ├── METHODOLOGY_LOGIC.md   # Calculation formulas
│   ├── INVOICE_REQUIREMENTS.md
│   └── ...
│
├── scripts/                    # Utility scripts
│   ├── test_connection.py
│   └── investigate_suppliers.py
│
└── backups/                    # Backup files
```

---

## Data Structure

The app expects a Google Sheet with this structure:

**Row 1:** Empty (reserved)
**Row 2:** Column headers
**Row 3+:** Product data

### Required Columns:
- `Product ID` - Unique identifier (e.g., PROD-001)
- `Product Name` - Display name
- `Supplier` - Supplier/vendor name
- `Category` - Product category
- `Minimum Qty` - Minimum order quantity
- `Unit Cost (1-25)` through `Unit Cost (1000+)` - 7 pricing tiers
- `Branding Setup Fee` - One-time setup cost
- `Label Cost per Unit` - Cost per custom label
- `Label Minimum Qty` - Minimum label order
- `Description` - Product description (optional)

See [docs/DATA_STRUCTURE.md](docs/DATA_STRUCTURE.md) for complete details and sample data.

---

## Usage

### Basic Workflow
1. **Select Product** - Choose supplier and product from dropdowns
2. **Customize** - Enter quantity and markup percentage
3. **Add Options** - Select custom labels if needed
4. **Add to Order** - Click "Add to Order" button
5. **Repeat** - Add more products as needed
6. **Configure Order** - Set shipping, tariff, and discounts
7. **Generate Outputs** - Copy/download proposals and invoices

### Pricing Formula

```
Product Total = (Base Price × Quantity) + Setup Fee + Label Costs + Markup
Order Total = Sum(Product Totals) - Discount + Shipping + Tariff

Where:
- Base Price: Selected from appropriate tier based on quantity
- Setup Fee: One-time branding setup (only if labels selected)
- Label Costs: Label unit cost × max(quantity, label minimum)
- Markup: (Base Price × Quantity) × (Markup % / 100)
- Discount: Products subtotal × (Discount % / 100)
```

**Important:** Markup applies to base product cost only, NOT to fees, shipping, or tariff.

---

## Configuration

### Modify Pricing Tiers
Edit tier ranges in `app.py` → `get_price_for_quantity()`:
```python
tier_columns = [
    {'min': 1, 'max': 25, 'column': 'Unit Cost (1-25)'},
    {'min': 26, 'max': 50, 'column': 'Unit Cost (26-50)'},
    # ... customize as needed
]
```

### Adjust Label Minimum
Edit in `app.py` → `calculate_additional_costs()`:
```python
label_minimum = int(label_minimum_raw) if label_minimum_raw else 100
```

### Change Discount Presets
Edit in `app.py` → Order Settings section:
```python
preset_options = [
    "Wholesale Discount (5%)",
    "Volume Discount (10%)",
    "Partner Discount (15%)"
]
```

---

## Deployment

### Streamlit Community Cloud (Recommended)

**Prerequisites:**
- GitHub repository (this project)
- Google Sheet created and populated with sample data
- Google Cloud service account credentials

**Steps:**
1. **Push to GitHub**
   - Ensure all changes are committed and pushed
   - Verify `.gitignore` excludes `secrets.toml`

2. **Connect to Streamlit Cloud**
   - Go to [share.streamlit.io](https://share.streamlit.io)
   - Sign in with GitHub
   - Click "New app"
   - Select your repository and branch
   - Set main file path: `app.py`

3. **Configure Secrets**
   - In app settings, click "Advanced settings"
   - Navigate to "Secrets" section
   - Copy entire contents of your local `.streamlit/secrets.toml`
   - Paste into the Secrets text box
   - Click "Save"

4. **Deploy**
   - Click "Deploy!"
   - Wait for deployment to complete (~2-3 minutes)
   - Your app will be live at `https://[your-app-name].streamlit.app`

**Important Notes:**
- The Google Sheet must be shared with your service account email (Editor access)
- Secrets are encrypted and never exposed in logs or to users
- You can update secrets anytime from the app settings
- Free tier includes: unlimited public apps, 1 GB resources per app

### Local Deployment

For development or testing:
```bash
streamlit run app.py --server.port 8501
```

**Production-like local setup:**
```bash
streamlit run app.py --server.port 8501 --server.address 0.0.0.0
```

---

## Development

This project follows beginner-friendly Python patterns:
- Simple, readable code structure
- Minimal dependencies
- Clear function names and comments
- Soft-coded configuration values
- Single-file architecture for simplicity

See [CLAUDE.md](CLAUDE.md) for complete development guidelines.

---

## Troubleshooting

**"Failed to load data" error:**
- Check Google Sheets access permissions
- Verify service account email has editor access to sheet
- Confirm sheet name matches in code (`suppliers_demo`)
- Check `.streamlit/secrets.toml` credentials are valid

**"No pricing available" error:**
- Verify product has pricing data in selected tier
- Check for empty cells in pricing columns
- Review fallback logic in `get_price_for_quantity()`

**Products not loading:**
- Confirm sheet structure matches expected format (Row 1 empty, Row 2 headers, Row 3+ data)
- Check `Product ID` column is not empty
- Verify column names match exactly (case-sensitive)

---

## Documentation

- **[CLAUDE.md](CLAUDE.md)** - Development guidelines and project rules
- **[PORTFOLIO.md](PORTFOLIO.md)** - Portfolio context and demo explanation
- **[docs/PLANNING.md](docs/PLANNING.md)** - Requirements and architecture decisions
- **[docs/DATA_STRUCTURE.md](docs/DATA_STRUCTURE.md)** - Complete data schema reference
- **[docs/METHODOLOGY_LOGIC.md](docs/METHODOLOGY_LOGIC.md)** - Pricing calculation formulas
- **[docs/INVOICE_REQUIREMENTS.md](docs/INVOICE_REQUIREMENTS.md)** - Invoice format specifications

---

## License

This is a portfolio/demo project. Feel free to use as reference or starting point for your own projects.

---

## Contact

For questions about this portfolio project, please open an issue on GitHub.

---

**Last Updated:** 2025-10-07
**Version:** 2.0 - Generic Portfolio Version
