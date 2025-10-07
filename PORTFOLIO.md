# Portfolio Project Context

**🌐 Live Demo:** [https://generic-pricing-data-solution.streamlit.app](https://generic-pricing-data-solution.streamlit.app)

## About This Project

This is a **genericized portfolio version** of a real production application I built for a client. The original application was designed for a small international business to streamline their pricing, quoting, and invoicing processes for products sourced from multiple artisan partners worldwide.

## Why a Generic Version?

While I'm proud of the work I did on the original project, I cannot share the client's proprietary data, business logic, or partner relationships publicly. This generic version allows me to:

1. **Showcase Technical Skills** - Demonstrate my ability to build full-stack data solutions
2. **Share Code Patterns** - Provide a reference implementation others can learn from
3. **Respect Confidentiality** - Protect client data and business relationships
4. **Portfolio Use** - Have a public project to discuss in job interviews and applications

## What Changed from the Original?

### Genericized Elements:
- **Company Names** - "Peace by Piece International" → "Acme Supply Co"
- **Partner Names** - Specific artisan partners → Generic suppliers (SupplierA, SupplierB, etc.)
- **Product Data** - Real product catalog → Sample/demo products
- **Business Context** - Artisan/social impact language → Generic B2B terminology
- **Discount Types** - NGO-specific discounts → General wholesale/volume discounts
- **Column Names** - Company-specific terms → Industry-standard terms

### Preserved Elements:
- **All Core Features** - Tiered pricing, multi-product ordering, markup calculations
- **Architecture** - Python/Streamlit + Google Sheets approach
- **Code Quality** - Beginner-friendly, well-documented patterns
- **Calculation Logic** - Real pricing methodologies and formulas
- **User Experience** - Complete workflow from product selection to invoice generation

## Real-World Impact

The original version of this application:
- ✅ Reduced quote generation time from 30+ minutes to under 5 minutes
- ✅ Eliminated pricing calculation errors from manual spreadsheet work
- ✅ Provided consistent proposal formatting across sales team
- ✅ Enabled easy price updates when supplier costs changed
- ✅ Created audit trail with order history and downloadable records

## Technical Highlights

This project demonstrates:

### Python/Streamlit Development
- Clean, maintainable single-file architecture
- Effective use of session state for multi-step workflows
- Real-time data validation and user feedback
- Professional UI/UX for business users

### Data Engineering
- Google Sheets as database (appropriate for small business scale)
- Pandas for data transformation and validation
- Smart tier selection with fallback logic
- Structured data flow from source to output

### Business Logic Implementation
- Complex pricing calculations with multiple variables
- Per-product vs. order-level cost allocation
- Discount application with edge case handling
- Minimum quantity enforcement

### User Experience Design
- Progressive disclosure (add one product at a time)
- Edit/update workflow for order modifications
- Multiple output formats (screen, CSV download)
- Clear validation messages and warnings

## Sample Data

This demo uses fictional data that represents the structure and complexity of real supplier pricing:
- Multiple suppliers with different product categories
- 7-tier quantity-based pricing (realistic for wholesale/bulk ordering)
- Optional branding/customization with minimums
- Various product types with different cost structures

## Try It Yourself

While this is a portfolio version, the code is fully functional and can be adapted for real use cases:

- **Small Businesses** - Adapt for your own supplier pricing management
- **Learning** - Study the code to understand Streamlit and data workflows
- **Extension** - Build on this foundation for more complex requirements
- **Reference** - Use as a pattern for similar business applications

## Questions?

If you're interested in discussing this project, the original implementation, or how I approach building data solutions for small businesses, I'm happy to chat!

---

**Note:** All data in this repository is fictional and created specifically for demonstration purposes.
