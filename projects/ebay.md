# eBay Integration Scripts

## Overview
Python scripts for comparing and managing eBay listings against Channel Advisor data. Used for duplicate detection, listing comparison, and data reconciliation.

## Tech Stack
- **Language**: Python
- **APIs**: eBay API, Channel Advisor API
- **Data Processing**: pandas

## Scripts

### Comparison Tools
- **eBay vs CA Comparison**: Compares eBay listings against Channel Advisor inventory
- **Duplicate Detection**: Finds duplicate listings across platforms
- **Price Reconciliation**: Identifies pricing discrepancies

### Data Flow
```
eBay API → Python Scripts → Comparison Reports
    ↓
Channel Advisor API ────────────↗
```

## Key Features
- Cross-platform listing comparison
- Duplicate SKU detection
- Price and inventory discrepancy reports
- Bulk listing analysis

## Directory Structure
```
ebay/
├── scripts/
│   ├── compare_listings.py
│   ├── find_duplicates.py
│   └── price_check.py
├── data/
│   └── exports/
└── requirements.txt
```

## Usage
```bash
# Compare eBay listings with CA
python scripts/compare_listings.py

# Find duplicate listings
python scripts/find_duplicates.py

# Check price discrepancies
python scripts/price_check.py
```

## Related Projects
- **channel-advisor-catalog** - Primary CA integration
- **pim-cloud** - Product data management

## Repository
- **GitHub**: bhmoto/ebay
- **Status**: Active, utility scripts
