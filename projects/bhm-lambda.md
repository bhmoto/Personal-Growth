# BHM Lambda

## Overview
Java-based AWS Lambda function for synchronizing product data between Channel Advisor and SkuVault. This is a legacy system that appears to be inactive since February 2024.

## Tech Stack
- **Language**: Java 17
- **Build**: Gradle
- **Runtime**: AWS Lambda
- **APIs**: Channel Advisor API, SkuVault API

## Architecture

### Lambda Function
Single Lambda function that:
1. Fetches product data from Channel Advisor
2. Transforms data to SkuVault format
3. Syncs inventory and product info to SkuVault

### Integration Points
- **Channel Advisor**: Source of product/inventory data
- **SkuVault**: Destination warehouse management system

## Directory Structure
```
bhm-lambda/
├── src/
│   └── main/
│       └── java/
│           └── com/
│               └── bhm/
│                   ├── handlers/
│                   ├── services/
│                   └── models/
├── build.gradle
└── settings.gradle
```

## Status
- **Last Activity**: February 2024
- **Current State**: Likely inactive/deprecated
- **Replacement**: Python-based solutions (pim-cloud, channel-advisor-catalog)

## Notes
This Java Lambda was likely replaced by Python-based solutions that offer:
- Faster development iteration
- Better integration with AWS CDK
- Consistency with other BHM projects

## Repository
- **GitHub**: bhmoto/bhm-lambda
- **Status**: Inactive (legacy)
