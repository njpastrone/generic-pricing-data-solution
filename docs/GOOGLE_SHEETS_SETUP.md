# Google Sheets Setup Guide

Complete step-by-step guide for setting up Google Sheets access for this application.

---

## Overview

This app uses Google Sheets as its database. You need to:
1. Create a Google Cloud project and service account
2. Enable the necessary APIs
3. Create and configure a Google Sheet
4. Set up credentials in the app

**Time Required:** ~15-20 minutes (first time)

---

## Part 1: Google Cloud Setup

### Step 1: Create Google Cloud Project

1. Go to [Google Cloud Console](https://console.cloud.google.com)
2. Sign in with your Google account
3. Click "Select a project" at the top
4. Click "New Project"
5. Enter a project name (e.g., "pricing-app-demo")
6. Click "Create"
7. Wait for the project to be created (notification will appear)

### Step 2: Enable Required APIs

1. In your project, go to "APIs & Services" > "Library"
2. Search for "Google Sheets API"
3. Click on it and click "Enable"
4. Go back to Library
5. Search for "Google Drive API"
6. Click on it and click "Enable"

### Step 3: Create Service Account

1. Go to "IAM & Admin" > "Service Accounts"
2. Click "Create Service Account"
3. Enter details:
   - **Name:** `pricing-app-service`
   - **Description:** `Service account for pricing application`
4. Click "Create and Continue"
5. Skip "Grant this service account access" (click Continue)
6. Skip "Grant users access" (click Done)

### Step 4: Create Service Account Key

1. Click on the service account you just created
2. Go to the "Keys" tab
3. Click "Add Key" > "Create new key"
4. Select "JSON" format
5. Click "Create"
6. A JSON file will download - **SAVE THIS SECURELY**

**Important:** This JSON file contains sensitive credentials. Never share it or commit it to git.

### Step 5: Note the Service Account Email

In the service account details, you'll see an email like:
```
pricing-app-service@your-project-id.iam.gserviceaccount.com
```

**Copy this email** - you'll need it to share the Google Sheet.

---

## Part 2: Google Sheet Setup

### Step 1: Create the Google Sheet

1. Go to [Google Sheets](https://sheets.google.com)
2. Create a new blank spreadsheet
3. Name it exactly: `suppliers_demo`

### Step 2: Set Up Sheet Structure

1. **Leave Row 1 completely empty** (reserved)
2. In **Row 2**, add these column headers (copy/paste recommended):

```
Product ID	Product Name	Supplier	Category	Minimum Qty	Unit Cost (1-25)	Unit Cost (26-50)	Unit Cost (51-100)	Unit Cost (101-250)	Unit Cost (251-500)	Unit Cost (501-1000)	Unit Cost (1000+)	Branding Setup Fee	Label Cost per Unit	Label Minimum Qty	Description
```

3. Starting in **Row 3**, paste the sample data from `docs/SAMPLE_DATA_FOR_SHEET.md`

**Tip:** Copy the CSV section from SAMPLE_DATA_FOR_SHEET.md and paste directly into the sheet.

### Step 3: Share Sheet with Service Account

1. Click the "Share" button in the top-right of your sheet
2. Paste the service account email (from Part 1, Step 5)
3. Set permission to **"Editor"**
4. Uncheck "Notify people" (it's a service account, not a person)
5. Click "Share"

---

## Part 3: App Configuration

### Step 1: Create secrets.toml File

1. Navigate to the project directory:
```bash
cd "/Users/nicolopastrone/Desktop/Development Projects/generic-pricing-data-solution"
```

2. Copy the template file:
```bash
cp .streamlit/secrets.toml.example .streamlit/secrets.toml
```

### Step 2: Fill in Credentials

1. Open the downloaded JSON key file from Part 1, Step 4
2. Open `.streamlit/secrets.toml` in your editor
3. Copy values from JSON to TOML:

**JSON field → TOML field:**
- `type` → `type`
- `project_id` → `project_id`
- `private_key_id` → `private_key_id`
- `private_key` → `private_key` (keep the \n characters)
- `client_email` → `client_email`
- `client_id` → `client_id`
- `auth_uri` → `auth_uri`
- `token_uri` → `token_uri`
- `auth_provider_x509_cert_url` → `auth_provider_x509_cert_url`
- `client_x509_cert_url` → `client_x509_cert_url`

**Important:** For `private_key`, keep it as a single line with `\n` characters. Don't try to format it as multiple lines.

### Step 3: Verify secrets.toml Format

Your file should look like this:

```toml
[gcp_service_account]
type = "service_account"
project_id = "pricing-app-demo-123456"
private_key_id = "abc123def456..."
private_key = "-----BEGIN PRIVATE KEY-----\nMIIEvQIBADANBgkqhki...\n-----END PRIVATE KEY-----\n"
client_email = "pricing-app-service@pricing-app-demo-123456.iam.gserviceaccount.com"
client_id = "123456789012345678901"
auth_uri = "https://accounts.google.com/o/oauth2/auth"
token_uri = "https://oauth2.googleapis.com/token"
auth_provider_x509_cert_url = "https://www.googleapis.com/oauth2/v1/certs"
client_x509_cert_url = "https://www.googleapis.com/robot/v1/metadata/x509/pricing-app-service%40pricing-app-demo-123456.iam.gserviceaccount.com"
```

---

## Part 4: Testing

### Step 1: Test Connection

```bash
cd "/Users/nicolopastrone/Desktop/Development Projects/generic-pricing-data-solution"
streamlit run scripts/test_connection.py
```

**Expected Result:** You should see:
- ✅ Successfully connected to Google Sheets
- ✅ Found sheet: suppliers_demo
- ✅ Sample data displayed

### Step 2: Run the App

```bash
streamlit run app.py
```

**Expected Result:**
- App loads without errors
- Message: "Loaded X products from suppliers catalog"
- Product dropdowns are populated
- You can select products and add to order

---

## Troubleshooting

### Error: "Failed to load data: [404] Requested entity was not found"

**Cause:** Sheet name doesn't match or sheet not found

**Solution:**
1. Verify sheet is named exactly `suppliers_demo` (case-sensitive)
2. Check that you shared the sheet with the service account email
3. Make sure you're using the correct Google account

### Error: "Failed to load data: [403] The caller does not have permission"

**Cause:** Service account doesn't have access to the sheet

**Solution:**
1. Go to your Google Sheet
2. Click "Share"
3. Add the service account email as "Editor"
4. Make sure you clicked "Share" to confirm

### Error: "No such file or directory: secrets.toml"

**Cause:** secrets.toml file not created

**Solution:**
1. Copy `.streamlit/secrets.toml.example` to `.streamlit/secrets.toml`
2. Fill in your credentials
3. Make sure file is in the `.streamlit/` directory

### Error: "Invalid private key"

**Cause:** Private key not formatted correctly in secrets.toml

**Solution:**
1. Copy the entire private_key value from the JSON file
2. Keep it as ONE line in secrets.toml
3. Keep the `\n` characters - don't replace them with actual line breaks
4. Make sure it starts with `-----BEGIN PRIVATE KEY-----\n`
5. Make sure it ends with `\n-----END PRIVATE KEY-----\n`

### Products Not Loading / Empty Dropdown

**Cause:** Data structure doesn't match expected format

**Solution:**
1. Verify Row 1 is empty
2. Verify Row 2 has the exact column headers (see Part 2, Step 2)
3. Verify data starts at Row 3
4. Check that Product ID column has values (not empty)
5. Verify column names match exactly (including spaces and capitalization)

---

## Security Best Practices

### ✅ DO:
- Keep secrets.toml on your local machine only
- Add `.streamlit/secrets.toml` to `.gitignore` (already done)
- Use service accounts (not personal accounts) for app access
- Regularly rotate service account keys (every 90 days recommended)
- Store JSON key file securely (password manager or encrypted storage)

### ❌ DON'T:
- Don't commit secrets.toml to git
- Don't share your service account JSON key with others
- Don't use personal Google account credentials in the app
- Don't grant unnecessary permissions to service account
- Don't reuse service accounts across different projects

---

## Deployment to Streamlit Cloud

If deploying to Streamlit Cloud:

1. Go to your Streamlit Cloud app settings
2. Click "Secrets"
3. Paste the entire contents of your `.streamlit/secrets.toml` file
4. Click "Save"

The app will restart with the new credentials.

---

## Alternative: Using Your Own Sheet Name

If you want to use a different sheet name:

1. Change the sheet name in `app.py` line 340:
```python
sheet = gc.open("your-custom-name").sheet1
```

2. Update the sheet name in `scripts/test_connection.py` similarly

3. Create/rename your Google Sheet to match

---

## Need Help?

- **Google Cloud Console:** [console.cloud.google.com](https://console.cloud.google.com)
- **Google Sheets API Docs:** [developers.google.com/sheets/api](https://developers.google.com/sheets/api)
- **Streamlit Secrets Docs:** [docs.streamlit.io/streamlit-cloud/get-started/deploy-an-app/connect-to-data-sources/secrets-management](https://docs.streamlit.io/streamlit-cloud/get-started/deploy-an-app/connect-to-data-sources/secrets-management)

For issues with this specific app, check the README.md troubleshooting section.

---

**Last Updated:** 2025-10-07
