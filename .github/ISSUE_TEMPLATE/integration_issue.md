---
name: Integration Issue
about: Report issues with third-party integrations (Stripe, eBay, Pirate Ship, etc.)
title: '[INTEGRATION] '
labels: integration
assignees: ''
---

## 🔌 Integration Details
**Which integration is having issues?**
- [ ] Stripe
- [ ] eBay
- [ ] Pirate Ship
- [ ] DigitalOcean
- [ ] Saleor
- [ ] Bank Imports
- [ ] AI/Document Processing

**Integration Account/Version**: [e.g., Stripe Connect, eBay Seller Hub, Pirate Ship API v2]

## 🔍 Issue Description
A clear and concise description of the integration issue.

## 🔄 Sync/Import Details
**Import Type**: [e.g., Manual import, Scheduled sync, Webhook trigger]
**File Type**: [e.g., CSV, Excel, PDF, API response]
**Batch ID**: [If applicable, provide the import batch ID]
**Date Range**: [What date range were you trying to sync/import?]

## 📊 Data Details
**Number of Records**: [e.g., 150 transactions, 25 products]
**File Size**: [e.g., 2.5 MB, 500 KB]
**Sample Data**: [If possible, provide sanitized sample data]

```
Paste sample data here (remove sensitive information)
```

## ❌ Error Information
**Error Message**: 
```
Paste the full error message here
```

**Error Code**: [If applicable]
**When Error Occurs**: [e.g., During file upload, During processing, After import completes]

## 🔐 Authentication Status
- [ ] API credentials are valid and active
- [ ] Permissions are correctly configured
- [ ] No recent changes to third-party account settings
- [ ] Webhook endpoints are accessible (if applicable)

## 🔄 Steps to Reproduce
1. Go to integration settings...
2. Upload/sync file...
3. Configure options...
4. See error...

## ✅ Expected Behavior
What should happen during a successful sync/import?

## 🌐 Environment
- **Integration Environment**: [e.g., Sandbox, Production]
- **API Version**: [If known]
- **Last Successful Sync**: [Date/time of last working sync]

## 🔍 Debug Information
**Import Settings Used**:
- Skip duplicates: [Yes/No]
- Date format: [MM/DD/YYYY, etc.]
- Custom field mappings: [If any]

**Transaction Processing**:
- Accounting method: [Accrual/Cash]
- Entity allocation: [Single/Multiple entities]
- Auto-categorization: [Enabled/Disabled]

## 📈 Impact Assessment
**Business Impact**:
- [ ] Cannot process payments
- [ ] Cannot sync sales data
- [ ] Cannot track shipping costs
- [ ] Cannot generate reports
- [ ] Data integrity concerns

**Urgency**:
- [ ] Critical - Business operations stopped
- [ ] High - Significant workflow disruption
- [ ] Medium - Some features unavailable
- [ ] Low - Minor inconvenience

## 🔧 Troubleshooting Attempted
What have you already tried?
- [ ] Refreshed API credentials
- [ ] Retried the import/sync
- [ ] Checked third-party service status
- [ ] Verified file format and content
- [ ] Checked system logs
- [ ] Contacted third-party support

## 📎 Additional Context
- Recent changes to integration settings?
- Changes to third-party account configuration?
- File format changes from the provider?
- Network connectivity issues?

## 🤝 Third-Party Support
Have you contacted the third-party service (Stripe, eBay, etc.) about this issue?
- [ ] Yes, they confirmed the issue is on their side
- [ ] Yes, they confirmed the issue is not on their side
- [ ] Yes, still investigating with them
- [ ] No, haven't contacted them yet

**Third-party ticket/case number**: [If applicable]