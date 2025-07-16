# Accounting Fundamentals

*Last Updated: July 9th, 2025 | Compatible with: All Versions*

The SMB Accounting System is built on **proper double-entry bookkeeping principles** to ensure accurate financial records and compliance with accounting standards.

## 📊 Double-Entry Bookkeeping

### Core Principles
Every transaction in the system follows double-entry bookkeeping rules:
- **Every transaction** must have at least two entries (debit and credit)
- **Debits must equal credits** for each transaction
- **Account balances** are maintained automatically
- **Audit trail** is preserved for all changes

### Account Types
The system supports all standard account types:

| Account Type | Normal Balance | Increases With | Examples |
|--------------|----------------|----------------|----------|
| **Assets** | Debit | Debits | Cash, Accounts Receivable, Inventory |
| **Liabilities** | Credit | Credits | Accounts Payable, Loans, Taxes Owed |
| **Equity** | Credit | Credits | Owner's Equity, Retained Earnings |
| **Revenue** | Credit | Credits | Sales Revenue, Service Revenue |
| **Expenses** | Debit | Debits | Office Supplies, Rent, Utilities |

### Transaction Validation
All transactions are automatically validated:
- **Balance verification** - Debits = Credits
- **Account type validation** - Proper debit/credit usage
- **Date validation** - Reasonable transaction dates
- **Amount validation** - Positive amounts only

## 🏗️ Chart of Accounts

### Account Structure
The chart of accounts uses a **hierarchical numbering system**:

```
1000-1999: Assets
  1100-1199: Current Assets
    1110: Cash - Operating Account
    1120: Cash - Savings Account
    1130: Accounts Receivable
    1140: Inventory
  1200-1299: Fixed Assets
    1210: Equipment
    1220: Accumulated Depreciation

2000-2999: Liabilities
  2100-2199: Current Liabilities
    2110: Accounts Payable
    2120: Accrued Expenses
    2130: Sales Tax Payable
  2200-2299: Long-term Liabilities
    2210: Business Loan

3000-3999: Equity
  3110: Owner's Equity
  3120: Retained Earnings
  3130: Owner Draws

4000-4999: Revenue
  4110: Product Sales
  4120: Service Revenue
  4130: Shipping Revenue

5000-5999: Expenses
  5110: Cost of Goods Sold
  5200: Office Expenses
  5300: Shipping Expenses
  5400: Professional Services
```

### Account Management
- **Custom account codes** - Follow your preferred numbering system
- **Account hierarchies** - Parent/child relationships for reporting
- **Active/inactive status** - Control which accounts are available
- **Account descriptions** - Clear naming for user understanding

## 💰 Transaction Management

### Transaction Structure
Each transaction contains:
- **Transaction date** - When the business event occurred
- **Description** - Clear explanation of the transaction
- **Reference number** - Optional external reference (invoice #, check #)
- **Entity** - Which business entity this affects
- **Total amount** - Sum of all debit amounts (equals sum of credit amounts)
- **Transaction lines** - Individual debit/credit entries

### Transaction Lines
Each line within a transaction specifies:
- **Account** - Which chart of accounts entry is affected
- **Debit amount** - Amount to debit (increase assets/expenses, decrease liabilities/equity/revenue)
- **Credit amount** - Amount to credit (decrease assets/expenses, increase liabilities/equity/revenue)
- **Description** - Line-specific description (optional)

### Example Transaction
**Sale of Products ($1,200)**
```
Date: 2025-01-15
Description: Sale to ABC Company - Invoice #INV-001
Reference: INV-001
Total Amount: $1,200

Transaction Lines:
- Accounts Receivable (1130)    Debit: $1,200   Credit: $0
- Product Sales (4110)          Debit: $0       Credit: $1,200
```

## 🔄 Accounting Methods

### Accrual Accounting (Default)
Records transactions **when they occur**, regardless of cash flow:
- **Sales** recorded when goods/services are delivered
- **Expenses** recorded when incurred
- **Better matching** of revenues and expenses
- **Required for larger businesses** and better financial analysis

**Example**: eBay sale is recorded when the item is sold, even though payment from eBay comes later.

### Cash Accounting (Optional)
Records transactions **when cash changes hands**:
- **Income** recorded when payment is received
- **Expenses** recorded when payment is made
- **Simpler** for small businesses
- **Tax advantages** for qualifying small businesses

### Integration-Specific Handling
Different integrations support different timing:
- **Stripe**: Typically cash basis (payment received)
- **eBay**: Supports both (sale vs payout)
- **Expenses**: Usually accrual basis (expense incurred)

## 🏢 Multi-Entity Support

### Entity Isolation
Each business entity maintains:
- **Separate chart of accounts** - Customized for business type
- **Isolated transactions** - No cross-entity mixing
- **Independent reporting** - Entity-specific financial statements
- **User permissions** - Control access per entity

### Entity Types
The system supports various business structures:
- **Sole Proprietorship** - Single owner, unlimited liability
- **Partnership** - Multiple owners, shared profits/losses
- **Corporation** - Separate legal entity, limited liability
- **LLC** - Hybrid structure with flexible tax treatment

### Cross-Entity Transactions
When one entity pays for another:
- **Owner investment** - Properly track personal vs business expenses
- **Inter-company loans** - Record amounts owed between entities
- **Shared expenses** - Allocate costs across multiple entities
- **Management fees** - Service charges between entities

## 📈 Financial Reporting

### Standard Reports
The system generates standard financial reports:
- **Balance Sheet** - Assets, Liabilities, and Equity at a point in time
- **Income Statement** - Revenue and Expenses over a period
- **Cash Flow Statement** - Cash inflows and outflows
- **General Ledger** - Detailed transaction listing by account

### Report Customization
- **Date ranges** - Custom periods for analysis
- **Entity filtering** - Single or multiple entities
- **Account grouping** - Summary or detailed views
- **Comparison periods** - Year-over-year or month-over-month

### Real-Time Updates
All reports reflect the current state:
- **Immediate updates** after transaction entry
- **Live calculations** of account balances
- **Dynamic filtering** and sorting options
- **Export capabilities** for external analysis

## 🔍 Audit Trail

### Transaction History
Every transaction maintains:
- **Creation timestamp** - When the transaction was entered
- **Created by user** - Who entered the transaction
- **Modification history** - Any changes made after creation
- **Source information** - Import batch or manual entry
- **Integration data** - Original data from external systems

### Change Tracking
The system tracks:
- **Account modifications** - Changes to chart of accounts
- **Transaction edits** - Modifications to existing transactions
- **User actions** - Complete audit log of system usage
- **System events** - Automated processes and integrations

### Compliance Features
Built-in compliance support:
- **Immutable records** - Transactions cannot be deleted, only voided
- **Backup procedures** - Regular data backups for recovery
- **User authentication** - Secure access controls
- **Data encryption** - Sensitive information protection

## 🔧 System Configuration

### Default Accounts
The system can auto-create standard accounts:
- **Required accounts** for basic operations
- **Integration-specific accounts** for automated processing
- **Tax accounts** for compliance tracking
- **Owner equity accounts** for sole proprietorships

### Validation Rules
Configurable validation:
- **Account code formats** - Enforce numbering standards
- **Transaction limits** - Maximum amounts for approval workflows
- **Date restrictions** - Prevent backdating beyond specified periods
- **User permissions** - Control who can modify what

### Integration Mapping
Automatic account mapping for imports:
- **Default expense accounts** for different transaction types
- **Revenue recognition** rules for sales transactions
- **Tax handling** for different jurisdictions
- **Fee processing** for payment processor charges

---

*For detailed setup instructions, see the [Getting Started Guide](../user-guide/getting-started.md). For integration-specific accounting treatment, refer to the individual [Integration Guides](../integrations/).*