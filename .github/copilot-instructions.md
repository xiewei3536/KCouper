---
applyTo: '**'
---
# KCouper Development Instructions

## Architecture Overview
KCouper is a web app that collects KFC coupon data from Taiwan's official API and displays it in a searchable interface. The backend (Python) gathers data via `script/kfc.py`, processes it into structured JSON/JS files (`coupon.json`, `js/coupon.js`), and the frontend (HTML/JS/CSS) renders coupons with filtering, sorting, and favorites.

Key components:
- **Backend**: `script/gatherer/coupon.py` converts API responses to Coupon objects with items/flavors.
- **Frontend**: `js/main.js` handles UI logic; uses jQuery/Bootstrap for DOM manipulation.
- **Data Flow**: API → Python processing → JSON storage → JS loading → HTML rendering.

## Developer Workflows
- **Update Coupons (Full)**: Run `pipenv run python script/kfc.py --mode main` after setting env vars (`SHOP_CODE`, `COUPON_RANGES`, `EXCLUDE_NAMES`).
- **Update Coupons (Quick)**: Run `pipenv run python script/kfc.py --mode quick` to incrementally update, reusing valid existing data.
- **Check Coupons**: Use `--mode check` to verify existence without full processing.
- **Single Query**: `--mode single` for querying each product prices.
- **Environment**: Use Pipenv for dependencies; Python 3.12 required.
- **Debugging**: Check `utils.LOG` for API errors; frontend logs to console for UI issues.
- **Linting**: Run `pylint script/` for Python code style checks.

## Code Patterns & Conventions

### Python Backend
- **Naming**: snake_case for functions/variables, PascalCase for classes, UPPER_CASE for constants
- **Formatting**: PEP 8, 100 char lines, 4 spaces indentation
- **Error Handling**: API calls retry up to 10 times on 502 with 0.3s delays; log errors with context
- **Data Structures**: Use normalize_name() to strip parentheses; convert_coupon_data() for structured Coupon objects

### React Frontend (Modern)
- **Components**: PascalCase, memo-wrapped for performance
- **Hooks**: camelCase, use prefix (useCoupons, useFavorites)
- **Variables**: camelCase, descriptive names
- **Booleans**: is/has/show prefix (isLoading, showFavoritesOnly)
- **Event Handlers**: on + ActionName (onSearchChange, onToggleFavorite)
- **TypeScript**: Full type safety, JSDoc for legacy JS

### Data Structures
- **Coupon**: {name, product_code, coupon_code, items, start_date, end_date, price, original_price, discount}
- **CouponItem**: {name, count, addition_price, flavors: [{name, addition_price}]}
- **Storage**: Favorites as Set<number> in localStorage; coupon data in COUPON_DICT

## Error Handling Patterns
- **API Resilience**: Auto-retry 502 errors up to 10x with 30s backoff
- **Data Validation**: Skip invalid coupons (message contains '無效的票劵' or starts with '此優惠代碼目前無法使用')
- **Logging**: Central logger in utils.py; console logs in frontend
- **User Feedback**: Toast notifications for errors; isLoading/error states

## Styling Guidelines
- **Tailwind CSS**: Mobile-first, custom colors via CSS variables
- **Dark Mode**: next-themes with class-based toggle
- **Components**: shadcn/ui on Radix UI primitives
- **Responsive**: sm: breakpoint at 640px
- **Icons**: lucide-react, consistent sizing
- **Font**: Noto Sans TC for Chinese text

## Integration Points
- **KFC API**: Calls via `utils.api_caller` with 0.3s delays; uses session from `init_session`.
- **Dependencies**: `requests`, `beautifulsoup4`, `python-dotenv` for backend; jQuery/Bootstrap for frontend.
- **Deployment**: Static files served; update via GitHub Pages (https://winedays.github.io/KCouper/) with GitHub Actions workflows.

Reference: `SPECIFICATION.md` for full details, `README.md` for overview, `AGENTS.md` for comprehensive guidelines.</content>
