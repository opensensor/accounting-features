# eBay Integration Guide

*Last Updated: January 2025 | Compatible with: All Versions*

The eBay integration provides **comprehensive sales tracking** with proper **accrual accounting** that separates sales events from cash flow events, ensuring accurate financial reporting for e-commerce businesses.

## 🎯 Overview

### What This Integration Does
- **Imports eBay sales data** from Seller Hub transaction reports
- **Creates proper accounting entries** using accrual accounting principles
- **Separates sales from payouts** for accurate revenue timing
- **Tracks fees and taxes** with detailed breakdown
- **Links shipping costs** to sales transactions automatically
- **Handles refunds and adjustments** with proper accounting treatment

### Key Benefits
- **Accurate revenue recognition** - Sales recorded when they occur, not when paid
- **Complete fee tracking** - All eBay fees properly categorized as expenses
- **Tax compliance** - Proper handling of eBay-collected vs seller-collected taxes
- **Automated workflow** - Reduces manual data entry by 90%+
- **Audit trail** - Complete record of all eBay transaction data

## 🏗️ Accounting Methodology

### Accrual vs Cash Accounting
The eBay integration uses **proper accrual accounting** with two separate events:

#### 1. Sale Transaction (When Customer Purchases)
```
Date: 2025-01-15 (Sale Date)
Description: eBay Sale: Wireless Headphones (buyer123)
Reference: Order #12345

Accounts Receivable - eBay    $95.50  (Debit)
eBay Fees                     $9.50   (Debit)  
Sales Tax Payable             $5.00   (Credit)
Product Sales                 $90.00  (Credit)
Shipping Revenue              $10.00  (Credit)
```

#### 2. Payout Transaction (When eBay Pays You)
```
Date: 2025-01-17 (Payout Date)
Description: eBay payout - Ref #PAYOUT-789

Cash - Business Account       $95.50  (Debit)
Accounts Receivable - eBay    $95.50  (Credit)
```

### Benefits of This Approach
- **Accurate timing** - Revenue recognized when earned, not when paid
- **Better cash flow tracking** - Separate visibility into sales vs cash
- **Proper A/R management** - Track what eBay owes you
- **Compliance ready** - Meets GAAP requirements for accrual accounting

## 📥 Import Process

### Supported File Formats
- **eBay Seller Hub** transaction reports (CSV, Excel)
- **Transaction reports** with detailed fee breakdown
- **Order reports** from Seller Hub downloads
- **Custom CSV** exports with proper column mapping

### File Requirements
Your eBay export should include these columns:
- **Sales Record Number** or **Order Number**
- **Sale Date** / **Transaction Date**
- **Buyer Information** (username, name, email)
- **Item Details** (number, title, quantity, price)
- **Shipping Information** (cost, address, tracking)
- **Tax Information** (eBay-collected, seller-collected)
- **Fee Information** (final value fees, payment processing)

### Import Steps
1. **Download transaction report** from eBay Seller Hub
2. **Navigate to eBay Integration** in the system
3. **Upload your file** (CSV or Excel)
4. **Preview and validate** the data mapping
5. **Configure import settings** (accounts, date format, etc.)
6. **Run the import** and review results
7. **Handle any errors** or duplicates

## ⚙️ Configuration

### Required Accounts
The system will auto-create these accounts if they don't exist:

#### Assets
- **Accounts Receivable - eBay** (1135) - What eBay owes you
- **Cash** accounts for payout destinations

#### Revenue
- **Product Sales** (4110) - Main product revenue
- **Shipping Revenue** (4130) - Shipping charges to customers

#### Expenses
- **eBay Fees** (5450) - Final value fees, insertion fees, etc.

#### Liabilities
- **eBay Sales Tax Withholding** (2135) - Tax collected by eBay for government

### Import Settings
Configure these settings for consistent processing:

```yaml
Entity: Your business entity
Skip Duplicates: Yes (recommended)
Date Format: MM/DD/YYYY (match your eBay export)
Separate Shipping Revenue: Yes (recommended)
Use Accrual Accounting: Yes (required)
```

### Account Mapping
Map different transaction types to appropriate accounts:
- **Product sales** → Product Sales (4110)
- **Shipping charges** → Shipping Revenue (4130)
- **eBay fees** → eBay Fees (5450)
- **Sales tax** → eBay Sales Tax Withholding (2135)

## 📊 Transaction Processing

### Fee Calculations
The system handles all eBay fee types:
- **Final Value Fees** - Based on item + shipping price
- **Payment Processing Fees** - Credit card processing charges
- **International Fees** - Cross-border transaction fees
- **Regulatory Operating Fees** - Government-mandated fees
- **Performance Fees** - Fees for below-standard performance

### Tax Handling
Proper tax treatment based on collection method:
- **eBay-collected tax** → Recorded as liability (they pay government)
- **Seller-collected tax** → Recorded as your tax liability
- **No double-counting** of tax amounts
- **Proper reporting** for tax compliance

### Refund Processing
When processing refunds:
- **Full refunds** - Reverse the original sale transaction
- **Partial refunds** - Create adjustment transactions
- **Fee refunds** - Credit eBay fees when applicable
- **Tax adjustments** - Proper handling of refunded taxes

## 🔗 Shipping Integration

### Automatic Linking
The system can automatically link shipping costs to eBay sales:
- **Date-based matching** - Link shipments within date range of sales
- **Amount correlation** - Ensure shipping costs are reasonable vs sale value
- **Tracking number matching** - Link via tracking numbers when available
- **Confidence scoring** - Rate the quality of automatic matches

### Manual Linking
For complex cases, manually link transactions:
1. **Find the sale transaction** in the transaction list
2. **Identify shipping transactions** for the same period
3. **Use the linking tool** to connect related transactions
4. **Add notes** explaining the relationship

### Benefits of Linking
- **Clear expense categorization** - Business vs personal shipping costs
- **Accurate profit calculation** - True cost of each sale
- **Better reporting** - Complete picture of sale profitability
- **Audit compliance** - Clear trail of related transactions

## 📈 Reporting & Analysis

### eBay-Specific Reports
Generate reports specifically for eBay operations:
- **Sales by period** - Revenue trends over time
- **Fee analysis** - Track eBay fee percentages and trends
- **Profit margins** - Sales revenue minus eBay fees and shipping
- **Outstanding receivables** - What eBay still owes you
- **Tax liability** - Amount owed to tax authorities

### Integration with Standard Reports
eBay data appears in all standard financial reports:
- **Income Statement** - Revenue and expenses properly categorized
- **Balance Sheet** - Receivables and tax liabilities
- **Cash Flow** - Separate operating activities from cash flows
- **General Ledger** - Detailed transaction-by-transaction listing

## 🔧 Troubleshooting

### Common Import Issues

#### "Duplicate transaction detected"
- **Cause**: Same transaction imported multiple times
- **Solution**: Enable "Skip duplicates" or review import history
- **Prevention**: Keep track of what date ranges you've imported

#### "Unbalanced transaction error"
- **Cause**: Fee calculations don't match expected totals
- **Solution**: Check fee mapping and ensure all fees are accounted for
- **Prevention**: Use transaction reports with complete fee breakdown

#### "Account not found"
- **Cause**: Required accounts don't exist in chart of accounts
- **Solution**: Let system auto-create accounts or create them manually
- **Prevention**: Run account setup before first import

### Data Quality Issues

#### Missing tracking numbers
- **Impact**: Cannot auto-link shipping costs
- **Solution**: Use date/amount-based linking
- **Prevention**: Include tracking data in eBay exports when available

#### Incorrect fee amounts
- **Impact**: Inaccurate expense tracking
- **Solution**: Use transaction reports instead of sales reports
- **Prevention**: Always use detailed transaction reports from eBay

#### Tax amount confusion
- **Impact**: Double-counting or missing tax liabilities
- **Solution**: Verify eBay vs seller collection in settings
- **Prevention**: Understand your tax collection setup

## 🚀 Best Practices

### Regular Import Schedule
- **Daily imports** for high-volume sellers
- **Weekly imports** for moderate volume
- **Monthly imports** minimum for accurate reporting
- **End-of-month** imports for month-end closing

### Data Management
- **Consistent file naming** - Include date ranges in filenames
- **Archive source files** - Keep original eBay exports for audit
- **Review import results** - Check error logs after each import
- **Backup before imports** - Protect data during large imports

### Account Organization
- **Separate eBay accounts** from other revenue sources
- **Detailed fee tracking** - Use sub-accounts for different fee types
- **Clear account names** - Make chart of accounts user-friendly
- **Regular account review** - Ensure accounts match business needs

### Reconciliation
- **Monthly reconciliation** - Compare system totals to eBay statements
- **Payout verification** - Ensure all payouts are recorded
- **Fee validation** - Verify fee amounts match eBay billing
- **Tax compliance** - Regular review of tax liability accounts

## 🔐 Security & Compliance

### Data Protection
- **No API keys required** - File-based import only
- **Local file processing** - Data never sent to third parties
- **Secure storage** - Encrypted database storage
- **Access controls** - User permissions for sensitive data

### Audit Trail
Every eBay transaction maintains:
- **Original import data** - Raw data from eBay files
- **Processing details** - How the transaction was categorized
- **Import batch tracking** - Which import session created the transaction
- **User attribution** - Who performed the import

### Compliance Features
- **GAAP compliance** - Proper accrual accounting treatment
- **Tax reporting** - Accurate tax liability tracking
- **Retention policies** - Automatic data retention for required periods
- **Export capabilities** - Data export for external audits

---

*Next Steps: Set up your [Pirate Ship Integration](pirate-ship.md) to automatically link shipping costs to your eBay sales, or configure [Stripe Integration](stripe.md) if you use Stripe for payment processing.*