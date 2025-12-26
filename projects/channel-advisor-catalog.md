# Channel Advisor Catalog

## Overview
Web application for managing product catalogs synced with Channel Advisor. Provides tools for product validation, AI-powered optimization, and multi-channel listing management for Black Hills Moto.

## Tech Stack
- **Language**: Python 3.12
- **Framework**: FastHTML (Python web framework with HTMX)
- **Infrastructure**: AWS Lambda, DynamoDB, S3, CloudFront, Cognito
- **Deployment**: AWS CDK
- **Key Dependencies**: channel-advisor-api-python, boto3, pandas, anthropic

## Architecture
```
CloudFront → Lambda (FastHTML App) → DynamoDB (bhm-products)
                                  → Channel Advisor API
                                  → S3 (CA exports)
```

### Key Tables
- `bhm-products`: 122K+ products synced from CA export (346 columns)
- `bhm-changes-queue`: Pending changes to sync back to CA
- `pim-cloud-review-queue`: AI-processed product data
- `pim-cloud-approved`: Approved products pending CA sync

## Key Features

### Channel Validation
- Validates products against Amazon attribute qualification rules
- Checks required fields for parent vs child SKUs
- Category-specific requirements (BOOT, COAT, SNOW_PANT, etc.)
- Updates "Amazon Readiness" attribute in CA

### AI Review Page
- AI-optimized product titles, descriptions, bullets
- Copy-to-children functionality for parent attributes
- Direct CA API updates or queued background sync

### Product Sync
- Daily sync from CA Excel export (S3) to DynamoDB
- 346 columns, 122K products
- Derived fields: days_of_stock, needs_reorder

## Key Learnings

### Channel Advisor API
- Product fields: `PUT Products({id})`
- Attributes: `POST Products({id})/UpdateAttributes`
- Child products can't use `.save()` - must use direct API calls

### Validation Gotchas
- Two "Warranty" fields in CA: Product Field vs Custom Attribute
- Custom attributes export as `Warranty.1` → syncs as `Warranty_1`
- Need field mappings for naming discrepancies

### Lambda Tips
- Force cold start: `aws lambda update-function-configuration --description "..."`
- 4GB memory needed for large Excel processing
- 15 min timeout for full sync

## Quick Reference

### URLs
- Production: https://catalog.aws.realtimeindustries.com
- GitHub: https://github.com/Black-Hills-Moto/channel-advisor-catalog

### Commands
```bash
# Deploy
PATH="/usr/local/bin:/opt/homebrew/bin:$PATH" uv run cdk deploy --all

# Force Lambda cold start
aws lambda update-function-configuration --function-name channel-advisor-catalog-app-WebApp... --description "Force $(date +%s)"

# Trigger product sync
aws lambda invoke --function-name bhm-product-sync --invocation-type Event --payload '{}' /tmp/out.json

# Check product in DynamoDB
aws dynamodb get-item --table-name bhm-products --key '{"sku":{"S":"SKU-HERE"}}'
```

### Secrets
- `channel-advisor-catalog-data` in Secrets Manager
- Contains: CA_REFRESH_TOKEN, CA_APPLICATION_ID, CA_SHARED_SECRET
