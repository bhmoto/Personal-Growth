# PIM Cloud

## Overview
AI-powered Product Information Management system that uses Claude AI for intelligent product attribute extraction and validation. Processes product data through a multi-step workflow with human review capabilities.

## Tech Stack
- **Language**: Python 3.12
- **Infrastructure**: AWS CDK (Python)
- **AI**: Claude API (Anthropic)
- **Runtime**: AWS Lambda, Step Functions
- **Database**: DynamoDB (6 tables)
- **Storage**: S3
- **Scheduling**: EventBridge

## Architecture

### Step Functions Workflow
1. **Trigger** - Webhook or scheduled event
2. **Fetch Product Data** - Get product info from sources
3. **AI Processing** - Claude extracts/validates attributes
4. **Review Queue** - Human review for uncertain items
5. **Approval** - Approved items sync to destinations
6. **Sync** - Push to Channel Advisor, Amazon, etc.

### Lambda Functions (8)
- `pim-cloud-processor` - Main orchestrator
- `pim-cloud-ai-processor` - Claude AI integration
- `pim-cloud-review-handler` - Review queue management
- `pim-cloud-approval-handler` - Approval workflow
- `pim-cloud-sync-handler` - Destination sync
- `pim-cloud-webhook` - External webhook receiver
- `pim-cloud-scheduler` - Scheduled processing
- `pim-cloud-config-handler` - Configuration management

### DynamoDB Tables (6)
- `pim-cloud-products` - Product master data
- `pim-cloud-review-queue` - Items pending review
- `pim-cloud-approved` - Approved items ready to sync
- `pim-cloud-processing-locks` - Concurrency control
- `pim-cloud-configs` - Category configurations
- `pim-cloud-audit-log` - Processing history

## Key Features
- **AI-Powered Extraction**: Claude extracts attributes from product descriptions
- **Category Configurations**: Custom rules per product category
- **Review Workflow**: Human-in-the-loop for quality assurance
- **Multi-Destination Sync**: Push to CA, Amazon, eBay
- **Webhook Integration**: Real-time processing triggers
- **Audit Trail**: Full history of all processing

## AI Processing
```python
# Example: Claude extracts attributes
{
    "sku": "190103-1000-01",
    "category": "BOOT",
    "extracted": {
        "Color": "Black",
        "Size": "10",
        "Material": "Leather",
        "Warranty": "1 Year"
    },
    "confidence": 0.95
}
```

## Directory Structure
```
pim-cloud/
├── cdk/
│   ├── app.py
│   └── stacks/
│       └── pim_stack.py
├── src/
│   ├── handlers/
│   ├── services/
│   │   ├── ai_service.py
│   │   ├── review_service.py
│   │   └── sync_service.py
│   └── utils/
├── tests/
└── pyproject.toml
```

## Deployment Commands
```bash
# Deploy
PATH="/usr/local/bin:/opt/homebrew/bin:$PATH" JSII_SILENCE_WARNING_UNTESTED_NODE_VERSION=1 /opt/homebrew/bin/uv run cdk deploy

# Invoke processor manually
AWS_DEFAULT_REGION=us-east-1 aws lambda invoke \
  --function-name pim-cloud-processor \
  --cli-binary-format raw-in-base64-out \
  --payload '{"source": "webhook", "sku": "190103"}' \
  /tmp/response.json
```

## Related Projects
- **channel-advisor-catalog** - Consumes PIM data for validation
- **aws-seller-reporting** - Provides Amazon data for validation

## Repository
- **GitHub**: bhmoto/pim-cloud
- **Status**: Active, production use
