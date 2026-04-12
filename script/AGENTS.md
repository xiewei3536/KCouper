# PYTHON BACKEND KNOWLEDGE BASE

**Generated:** 2026-04-13
**Domain:** Python Data Scrapers (KFC API Interaction)

## OVERVIEW
This directory contains the Python backend responsible for collecting, verifying, and processing KFC coupon data from the official Taiwan API.

## STRUCTURE
```
script/
├── checker/             # Coupon existence verification
│   └── coupon.py        # Logic to check if code still exists
├── gatherer/            # Full data scraping logic
│   ├── coupon.py        # Main coupon scraper/converter
│   └── single.py        # Single item price scraper
├── kfc.py               # Root entry point with CLI arguments
└── utils.py             # Shared utilities (logging, API caller)
```

## WHERE TO LOOK
- **Entry Point**: `script/kfc.py` for CLI modes (`--mode main|quick|check|single`).
- **Scraper Logic**: `script/gatherer/coupon.py` for API requests and JSON conversion.
- **Robustness**: `script/utils.py` for the `api_caller` (retries and delays).
- **Data Model**: `convert_coupon_data()` for structured Coupon objects.

## CONVENTIONS
- **CLI Pattern**: Use `argparse` for mode switching in `kfc.py`.
- **API Retries**: Always use `utils.api_caller` for external requests to handle 502s.
- **Data Integrity**: Filter out invalid codes early (log as warning, don't crash).
- **Session Management**: Initialize session with `utils.init_session()`.

## ANTI-PATTERNS
- **Direct Requests**: Never use `requests.get()` directly; use `utils.api_caller`.
- **Magic Strings**: Store environment-specific values in `.env` (SHOP_CODE, etc.).
- **Unlogged Failures**: Log all API failures with `utils.LOG`.
- **Incomplete Cleanup**: Ensure session handles are closed or reused properly.
