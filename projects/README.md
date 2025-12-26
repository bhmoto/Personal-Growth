# BHM Projects Overview

## Active Projects

| Project | Description | Status |
|---------|-------------|--------|
| [channel-advisor-catalog](./channel-advisor-catalog.md) | Amazon listing validation and CA integration | Active |
| [pim-cloud](./pim-cloud.md) | AI-powered Product Information Management | Active |
| [aws-seller-reporting](./aws-seller-reporting.md) | SP-API data collection and reporting | Active |
| [ebay](./ebay.md) | eBay listing comparison scripts | Active |
| [systems](./systems.md) | Documentation and knowledge base | Active |

## Legacy Projects

| Project | Description | Status |
|---------|-------------|--------|
| [bhm-lambda](./bhm-lambda.md) | Java Lambda for CA↔SkuVault sync | Inactive |

## Architecture Overview

```
┌─────────────────────────────────────────────────────────────────┐
│                        Data Sources                              │
├──────────────┬──────────────┬──────────────┬───────────────────┤
│   Amazon     │   Channel    │    eBay      │     SkuVault      │
│   SP-API     │   Advisor    │    API       │       API         │
└──────┬───────┴──────┬───────┴──────┬───────┴────────┬──────────┘
       │              │              │                │
       ▼              ▼              ▼                ▼
┌──────────────────────────────────────────────────────────────────┐
│                    AWS Infrastructure                             │
├──────────────────────────────────────────────────────────────────┤
│  ┌────────────────┐  ┌────────────────┐  ┌────────────────────┐ │
│  │ aws-seller-    │  │ pim-cloud      │  │ channel-advisor-   │ │
│  │ reporting      │  │ (AI/Claude)    │  │ catalog            │ │
│  │                │  │                │  │                    │ │
│  │ • SP-API sync  │  │ • AI extract   │  │ • Validation       │ │
│  │ • Advertising  │  │ • Review queue │  │ • Amazon submit    │ │
│  │ • Settlements  │  │ • Multi-dest   │  │ • Feed tracking    │ │
│  └────────────────┘  └────────────────┘  └────────────────────┘ │
│                                                                  │
│  ┌────────────────────────────────────────────────────────────┐ │
│  │                    DynamoDB Tables                          │ │
│  │  bhm-products │ pim-review-queue │ orders │ inventory      │ │
│  └────────────────────────────────────────────────────────────┘ │
└──────────────────────────────────────────────────────────────────┘
```

## Tech Stack Summary

| Technology | Projects Using |
|------------|----------------|
| Python 3.12 | All current projects |
| AWS CDK | aws-seller-reporting, pim-cloud, channel-advisor-catalog |
| AWS Lambda | All AWS projects |
| DynamoDB | aws-seller-reporting, pim-cloud, channel-advisor-catalog |
| Claude AI | pim-cloud |
| Step Functions | pim-cloud |
| FastAPI | channel-advisor-catalog |

## Deployment

All CDK projects use similar deployment commands:

```bash
# Standard deployment
PATH="/usr/local/bin:/opt/homebrew/bin:$PATH" JSII_SILENCE_WARNING_UNTESTED_NODE_VERSION=1 /opt/homebrew/bin/uv run cdk deploy

# List stacks
PATH="/usr/local/bin:/opt/homebrew/bin:$PATH" /opt/homebrew/bin/uv run cdk list
```

## Last Updated
2025-12-25
