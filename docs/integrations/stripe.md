# Stripe Integration Guide

*Last Updated: January 2025 | Compatible with: All Versions*

The Stripe integration provides **automated payment processing** with real-time transaction synchronization, comprehensive fee tracking, and proper accounting treatment for all Stripe payment activities.

## 🎯 Overview

### What This Integration Does
- **Syncs payment data** automatically from Stripe accounts
- **Tracks payment processing fees** with detailed breakdown
- **Handles refunds and disputes** with proper accounting treatment
- **Supports multiple Stripe accounts** for complex business structures
- **Integrates with webhooks** for real-time updates
- **Links payments to sales** from other platforms (eBay, e-commerce)

### Key Benefits
- **Real-time payment tracking** - Immediate visibility into cash flow
- **Automated fee accounting** - All Stripe fees properly categorized
- **Multi-account support** - Handle multiple Stripe accounts from one system
- **Comprehensive reporting** - Complete payment analytics and trends
- **Webhook integration** - Stay synchronized without manual imports

## 🔧 Setup & Configuration

### Prerequisites
- **Active Stripe account** (Standard or Express)
- **API access** with read permissions
- **Webhook endpoint** (optional, for real-time sync)
- **Business verification** completed in Stripe

### Connection Steps
1. **Navigate to Integrations** → Stripe
2. **Click "Add Stripe Account"**
3. **Enter account details**:
   - Account name (your reference)
   - Stripe Account ID (acct_xxx for Connect, or leave blank for Standard)
   - API Secret Key (sk_live_xxx or sk_test_xxx)
   - Webhook Secret (optional, for real-time updates)
4. **Test connection** to verify credentials
5. **Configure sync settings** (frequency, date range)
6. **Run initial sync** to import historical data

### API Key Setup
#### For Stripe Standard Accounts:
```bash
# Get your secret key from Stripe Dashboard → Developers → API keys
Secret Key: sk_live_xxxxxxxxxxxxx (for production)
Secret Key: sk_test_xxxxxxxxxxxxx (for testing)
```

#### For Stripe Connect (Multi-account):
```bash
# Platform secret key + account ID
Secret Key: sk_live_xxxxxxxxxxxxx (platform key)
Account ID: acct_xxxxxxxxxxxxx (connected account)
```

### Security Configuration
- **API keys are encrypted** in the database
- **Read-only permissions** - No ability to create charges
- **Webhook signature verification** prevents tampering
- **Rate limiting** respects Stripe API limits

## 📊 Accounting Treatment

### Payment Processing
When a customer pays via Stripe:
```
Date: 2025-01-15
Description: Stripe Payment - Customer ABC
Reference: pi_xxxxxxxxxxxxx

Cash - Stripe Account       $97.00  (Debit)
Stripe Processing Fees      $3.00   (Debit)
Accounts Receivable         $100.00 (Credit)
```

### Refund Processing
When issuing a refund:
```
Date: 2025-01-16
Description: Stripe Refund - Order #12345
Reference: re_xxxxxxxxxxxxx

Accounts Receivable         $100.00 (Debit)
Stripe Processing Fees      $3.00   (Credit) [Fee refunded]
Cash - Stripe Account       $97.00  (Credit)
```

### Dispute Handling
When a dispute occurs:
```
Date: 2025-01-17
Description: Stripe Dispute - chb_xxxxxxxxxxxxx
Reference: dp_xxxxxxxxxxxxx

Dispute Reserve             $100.00 (Debit)
Dispute Fees               $15.00  (Debit)
Cash - Stripe Account       $115.00 (Credit)
```

### Payout Processing
When Stripe pays out to your bank:
```
Date: 2025-01-18
Description: Stripe Payout - po_xxxxxxxxxxxxx
Reference: po_xxxxxxxxxxxxx

Cash - Business Account     $485.00 (Debit)
Cash - Stripe Account       $485.00 (Credit)
```

## 🔄 Synchronization

### Automatic Sync
- **Webhook integration** for real-time updates
- **Scheduled sync** every hour/day (configurable)
- **Incremental updates** to avoid duplicate processing
- **Error handling** with retry mechanisms

### Manual Sync
- **Force full sync** to catch any missed transactions
- **Date range sync** for specific periods
- **Account-specific sync** for multi-account setups
- **Sync status monitoring** with detailed logs

### Sync Coverage
The integration synchronizes:
- **Payment Intents** - Customer payments and their status
- **Charges** - Individual payment attempts
- **Refunds** - Full and partial refunds
- **Disputes** - Chargebacks and dispute fees
- **Payouts** - Transfers to your bank account
- **Fees** - All Stripe processing fees

## 💰 Fee Management

### Fee Types Tracked
- **Payment processing fees** - Standard 2.9% + 30¢
- **International fees** - Additional 1.5% for international cards
- **Currency conversion** - Exchange rate fees
- **Dispute fees** - $15 per dispute
- **Chargeback fees** - Additional fees for lost disputes

### Fee Categorization
Fees are automatically categorized:
```yaml
Payment Processing Fees (5460):
  - Card processing fees
  - ACH fees
  - International transaction fees

Dispute Fees (5470):
  - Chargeback fees
  - Dispute processing fees
  - Evidence submission fees

Currency Conversion (5480):
  - Foreign exchange fees
  - Currency conversion costs
```

### Fee Reporting
- **Monthly fee summaries** - Total fees by category
- **Fee percentage analysis** - Fees as % of revenue
- **Trend analysis** - Fee costs over time
- **Account comparison** - Fee rates across different Stripe accounts

## 🔗 Payment Linking

### Automatic Linking
The system can automatically link Stripe payments to:
- **eBay sales** - Match payments to eBay order numbers
- **Invoice payments** - Link to outstanding invoices
- **Subscription payments** - Recurring payment recognition
- **E-commerce orders** - Integration with shopping platforms

### Linking Criteria
Automatic linking uses:
- **Payment amounts** - Exact or close amount matching
- **Date proximity** - Payments within reasonable timeframes
- **Customer information** - Email addresses and names
- **Reference data** - Order numbers and invoice IDs

### Manual Linking
For complex cases:
1. **Review unlinked payments** in the Stripe dashboard
2. **Search for related transactions** in other systems
3. **Create manual links** with explanatory notes
4. **Verify accounting impact** of the linkage

## 📈 Reporting & Analytics

### Stripe-Specific Reports
- **Payment volume trends** - Revenue over time
- **Payment method analysis** - Card vs ACH vs international
- **Fee analysis** - Processing costs and trends
- **Dispute tracking** - Chargeback rates and outcomes
- **Payout reconciliation** - Stripe balance vs bank deposits

### Integration with Financial Reports
Stripe data appears in:
- **Cash Flow Statement** - Operating activities section
- **Income Statement** - Revenue and processing fee expenses
- **Balance Sheet** - Stripe account balances
- **General Ledger** - Detailed transaction listing

### Dashboard Widgets
Real-time widgets show:
- **Today's payment volume**
- **Processing fees this month**
- **Outstanding disputes**
- **Pending payouts**
- **Account balances**

## 🚨 Troubleshooting

### Common Connection Issues

#### "Invalid API key"
- **Check key format** - Should start with sk_live_ or sk_test_
- **Verify permissions** - Key needs read access to all data
- **Check account status** - Ensure Stripe account is active
- **Test vs Live** - Make sure you're using the right environment

#### "Webhook verification failed"
- **Check webhook secret** - Must match Stripe dashboard setting
- **Verify endpoint URL** - Must be accessible from Stripe servers
- **Check SSL certificate** - HTTPS required for production webhooks
- **Review webhook logs** - Check Stripe dashboard for delivery status

### Sync Issues

#### "Missing transactions"
- **Check date ranges** - Ensure sync covers the right period
- **Verify account access** - API key might not have full permissions
- **Review filters** - Some transaction types might be filtered out
- **Manual sync** - Force a full resync to catch missed items

#### "Duplicate transactions"
- **Enable duplicate detection** - System should skip existing transactions
- **Check import history** - Review what's already been imported
- **Verify transaction IDs** - Ensure unique identification is working
- **Clean up duplicates** - Use admin tools to remove duplicates

### Data Quality Issues

#### "Incorrect fee amounts"
- **Verify fee calculations** - Check against Stripe dashboard
- **Review fee structure** - Rates might have changed
- **Check currency conversion** - Exchange rates affect fees
- **Update fee mapping** - Ensure fees go to correct accounts

#### "Unlinked payments"
- **Review linking criteria** - Adjust matching parameters
- **Check timing differences** - Payments might be delayed
- **Verify customer data** - Names/emails might not match exactly
- **Manual review required** - Some payments need manual attention

## 🔐 Security & Compliance

### Data Protection
- **Encrypted API keys** - All credentials encrypted at rest
- **Read-only access** - Cannot create or modify Stripe data
- **Webhook verification** - All webhooks cryptographically verified
- **Audit logging** - Complete log of all API interactions

### PCI Compliance
- **No card data storage** - System never stores payment details
- **Tokenized references** - Only Stripe IDs and metadata stored
- **Secure transmission** - All API calls over HTTPS
- **Access controls** - User permissions for financial data

### Business Compliance
- **Revenue recognition** - Proper timing of revenue recording
- **Fee deductibility** - Processing fees properly categorized
- **Multi-entity support** - Separate accounting for different businesses
- **Audit trail** - Complete record of all payment activities

## 🚀 Best Practices

### Account Management
- **Descriptive account names** - Clear identification in multi-account setups
- **Regular credential rotation** - Update API keys periodically
- **Monitor account status** - Watch for any Stripe account issues
- **Backup webhook configuration** - Document webhook settings

### Reconciliation
- **Daily balance checks** - Verify Stripe balances match system
- **Monthly fee review** - Ensure all fees are captured
- **Payout verification** - Confirm bank deposits match payouts
- **Dispute monitoring** - Track chargeback trends and responses

### Performance Optimization
- **Webhook over polling** - Use webhooks for better performance
- **Reasonable sync frequency** - Don't over-sync low-volume accounts
- **Monitor API usage** - Stay within Stripe rate limits
- **Archive old data** - Keep system performant with data retention

### Integration Strategy
- **Link with other systems** - Connect Stripe to eBay, e-commerce, etc.
- **Automate where possible** - Reduce manual transaction entry
- **Regular validation** - Check integration accuracy monthly
- **Plan for growth** - Ensure setup scales with business volume

---

*Next Steps: Configure [eBay Integration](ebay.md) to link sales with Stripe payments, or set up [Pirate Ship Integration](pirate-ship.md) to track shipping costs related to your online sales.*