# AWS Seller Reporting

## Overview
Comprehensive AWS CDK application for Amazon Seller Central data collection and reporting. Collects sales, inventory, FBA, and advertising data from multiple Amazon seller accounts via SP-API and Advertising API.

## Tech Stack
- **Language**: Python 3.12
- **Infrastructure**: AWS CDK (Python)
- **Runtime**: AWS Lambda
- **Database**: DynamoDB, S3, Athena
- **APIs**: Amazon SP-API, Amazon Advertising API
- **Scheduling**: EventBridge

## Architecture

### CDK Stacks (4 total)
1. **SftpStack** - SFTP server for data transfer
2. **SpApiStack** - SP-API data collection (sales, inventory, FBA)
3. **AdvertisingStack** - Advertising API data collection
4. **AthenaStack** - Data querying and analytics

### Lambda Functions (18+)
- `get-orders` - Fetch orders from SP-API
- `get-order-items` - Fetch order line items
- `get-inventory` - Inventory summaries
- `get-fba-inventory` - FBA-specific inventory
- `get-inbound-shipments` - FBA inbound shipments
- `get-settlements` - Settlement reports
- `process-settlements` - Process settlement data
- `get-catalog-items` - Product catalog data
- `get-advertising-reports` - Ad campaign reports
- `process-advertising-reports` - Process ad data
- And more...

### Data Storage
- **DynamoDB Tables**: Orders, OrderItems, Inventory, Settlements, Advertising
- **S3 Buckets**: Raw data, processed reports, Athena results
- **Athena**: SQL queries across all data

## Key Features
- Multi-account support (multiple Amazon seller accounts)
- Automated daily/hourly data collection
- Settlement reconciliation
- Advertising performance tracking
- FBA inventory and shipment monitoring
- SFTP integration for external data access

## Directory Structure
```
aws-seller-reporting/
├── cdk/
│   ├── app.py
│   ├── stacks/
│   │   ├── sftp_stack.py
│   │   ├── sp_api_stack.py
│   │   ├── advertising_stack.py
│   │   └── athena_stack.py
│   └── constructs/
├── src/
│   ├── handlers/          # Lambda function handlers
│   ├── services/          # Business logic
│   └── utils/             # Shared utilities
├── tests/
└── pyproject.toml
```

## Deployment Commands
```bash
# Deploy all stacks
PATH="/usr/local/bin:/opt/homebrew/bin:$PATH" uv run cdk deploy --all

# Deploy specific stack
PATH="/usr/local/bin:/opt/homebrew/bin:$PATH" uv run cdk deploy SpApiStack

# List stacks
PATH="/usr/local/bin:/opt/homebrew/bin:$PATH" uv run cdk list
```

## Related Projects
- **pim-cloud** - Uses SP-API data for product validation
- **channel-advisor-catalog** - Syncs with CA using similar patterns

## Repository
- **GitHub**: bhmoto/aws-seller-reporting
- **Status**: Active, production use
