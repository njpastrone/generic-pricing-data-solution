# Sample Data for suppliers_demo Google Sheet

## Instructions for Creating Demo Sheet

1. Create a new Google Sheet named `suppliers_demo`
2. Structure: Row 1 = empty, Row 2 = headers (below), Row 3+ = data
3. Grant "Editor" access to your service account email
4. Copy/paste the data below

## Column Headers (Row 2)

```
Product ID | Product Name | Supplier | Category | Minimum Qty | Unit Cost (1-25) | Unit Cost (26-50) | Unit Cost (51-100) | Unit Cost (101-250) | Unit Cost (251-500) | Unit Cost (501-1000) | Unit Cost (1000+) | Branding Setup Fee | Label Cost per Unit | Label Minimum Qty | Description
```

## Sample Product Data (Row 3+)

### SupplierA Products (Office & Stationery)

**PROD-001: Executive Notebook Set**
- Supplier: SupplierA
- Category: Office Supplies
- Minimum Qty: 10
- Tier Pricing: $24.00, $20.40, $19.20, $18.00, $17.40, $16.80, $16.20
- Branding Setup: $50
- Label Cost: $1.20
- Label Min: 100
- Description: Premium leather-bound notebook set with pen

**PROD-002: Eco Pen Collection**
- Supplier: SupplierA
- Category: Office Supplies
- Minimum Qty: 25
- Tier Pricing: $8.00, $6.80, $6.40, $6.00, $5.80, $5.60, $5.40
- Branding Setup: $35
- Label Cost: $0.80
- Label Min: 100
- Description: Sustainable bamboo pens in display box

**PROD-003: Desk Organizer**
- Supplier: SupplierA
- Category: Office Supplies
- Minimum Qty: 5
- Tier Pricing: $32.00, $27.20, $25.60, $24.00, $23.20, $22.40, $21.60
- Branding Setup: $60
- Label Cost: $1.50
- Label Min: 50
- Description: Wooden desk organizer with multiple compartments

### SupplierB Products (Home & Lifestyle)

**PROD-101: Ceramic Mug Set**
- Supplier: SupplierB
- Category: Home Goods
- Minimum Qty: 12
- Tier Pricing: $16.00, $13.60, $12.80, $12.00, $11.60, $11.20, $10.80
- Branding Setup: $70
- Label Cost: $0.60
- Label Min: 100
- Description: Handcrafted ceramic mugs, set of 2

**PROD-102: Cotton Tote Bag**
- Supplier: SupplierB
- Category: Accessories
- Minimum Qty: 20
- Tier Pricing: $12.00, $10.20, $9.60, $9.00, $8.70, $8.40, $8.10
- Branding Setup: $45
- Label Cost: $0.95
- Label Min: 100
- Description: 100% organic cotton tote with reinforced handles

**PROD-103: Aromatherapy Candle**
- Supplier: SupplierB
- Category: Home Goods
- Minimum Qty: 15
- Tier Pricing: $18.00, $15.30, $14.40, $13.50, $13.05, $12.60, $12.15
- Branding Setup: $55
- Label Cost: $1.10
- Label Min: 75
- Description: Soy wax candle in glass jar with essential oils

### SupplierC Products (Tech & Gadgets)

**PROD-201: Wireless Charger**
- Supplier: SupplierC
- Category: Electronics
- Minimum Qty: 10
- Tier Pricing: $28.00, $23.80, $22.40, $21.00, $20.30, $19.60, $18.90
- Branding Setup: $80
- Label Cost: $1.35
- Label Min: 100
- Description: Qi-compatible wireless charging pad

**PROD-202: Bluetooth Speaker**
- Supplier: SupplierC
- Category: Electronics
- Minimum Qty: 8
- Tier Pricing: $36.00, $30.60, $28.80, $27.00, $26.10, $25.20, $24.30
- Branding Setup: $75
- Label Cost: $1.25
- Label Min: 100
- Description: Portable waterproof Bluetooth speaker

**PROD-203: Phone Stand**
- Supplier: SupplierC
- Category: Electronics
- Minimum Qty: 15
- Tier Pricing: $14.00, $11.90, $11.20, $10.50, $10.15, $9.80, $9.45
- Branding Setup: $40
- Label Cost: $0.75
- Label Min: 100
- Description: Adjustable aluminum phone stand

### SupplierD Products (Apparel)

**PROD-301: Baseball Cap**
- Supplier: SupplierD
- Category: Apparel
- Minimum Qty: 24
- Tier Pricing: $15.00, $12.75, $12.00, $11.25, $10.88, $10.50, $10.13
- Branding Setup: $65
- Label Cost: $0.90
- Label Min: 100
- Description: Adjustable cotton baseball cap

**PROD-302: Performance T-Shirt**
- Supplier: SupplierD
- Category: Apparel
- Minimum Qty: 20
- Tier Pricing: $18.00, $15.30, $14.40, $13.50, $13.05, $12.60, $12.15
- Branding Setup: $50
- Label Cost: $1.00
- Label Min: 100
- Description: Moisture-wicking athletic t-shirt

## Copy-Paste Ready Format (CSV)

```csv
Product ID,Product Name,Supplier,Category,Minimum Qty,Unit Cost (1-25),Unit Cost (26-50),Unit Cost (51-100),Unit Cost (101-250),Unit Cost (251-500),Unit Cost (501-1000),Unit Cost (1000+),Branding Setup Fee,Label Cost per Unit,Label Minimum Qty,Description
PROD-001,Executive Notebook Set,SupplierA,Office Supplies,10,$24.00,$20.40,$19.20,$18.00,$17.40,$16.80,$16.20,$50.00,$1.20,100,Premium leather-bound notebook set with pen
PROD-002,Eco Pen Collection,SupplierA,Office Supplies,25,$8.00,$6.80,$6.40,$6.00,$5.80,$5.60,$5.40,$35.00,$0.80,100,Sustainable bamboo pens in display box
PROD-003,Desk Organizer,SupplierA,Office Supplies,5,$32.00,$27.20,$25.60,$24.00,$23.20,$22.40,$21.60,$60.00,$1.50,50,Wooden desk organizer with multiple compartments
PROD-101,Ceramic Mug Set,SupplierB,Home Goods,12,$16.00,$13.60,$12.80,$12.00,$11.60,$11.20,$10.80,$70.00,$0.60,100,Handcrafted ceramic mugs set of 2
PROD-102,Cotton Tote Bag,SupplierB,Accessories,20,$12.00,$10.20,$9.60,$9.00,$8.70,$8.40,$8.10,$45.00,$0.95,100,100% organic cotton tote with reinforced handles
PROD-103,Aromatherapy Candle,SupplierB,Home Goods,15,$18.00,$15.30,$14.40,$13.50,$13.05,$12.60,$12.15,$55.00,$1.10,75,Soy wax candle in glass jar with essential oils
PROD-201,Wireless Charger,SupplierC,Electronics,10,$28.00,$23.80,$22.40,$21.00,$20.30,$19.60,$18.90,$80.00,$1.35,100,Qi-compatible wireless charging pad
PROD-202,Bluetooth Speaker,SupplierC,Electronics,8,$36.00,$30.60,$28.80,$27.00,$26.10,$25.20,$24.30,$75.00,$1.25,100,Portable waterproof Bluetooth speaker
PROD-203,Phone Stand,SupplierC,Electronics,15,$14.00,$11.90,$11.20,$10.50,$10.15,$9.80,$9.45,$40.00,$0.75,100,Adjustable aluminum phone stand
PROD-301,Baseball Cap,SupplierD,Apparel,24,$15.00,$12.75,$12.00,$11.25,$10.88,$10.50,$10.13,$65.00,$0.90,100,Adjustable cotton baseball cap
PROD-302,Performance T-Shirt,SupplierD,Apparel,20,$18.00,$15.30,$14.40,$13.50,$13.05,$12.60,$12.15,$50.00,$1.00,100,Moisture-wicking athletic t-shirt
```

## Sheet Setup Checklist

- [ ] Create Google Sheet named exactly `suppliers_demo`
- [ ] Leave Row 1 completely empty
- [ ] Add column headers in Row 2
- [ ] Paste product data starting at Row 3
- [ ] Verify all pricing columns have $ formatting
- [ ] Grant Editor access to service account email
- [ ] Test connection using `scripts/test_connection.py`

## Notes

- All prices include 15% volume discount built in per tier
- Label minimums vary by supplier (50-100 units typical)
- Branding setup fees range from $35-$80 depending on complexity
- Product categories help organize the catalog
- Descriptions are optional but recommended for clarity
