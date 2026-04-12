# HOOKS KNOWLEDGE BASE

**Generated:** 2026-04-13
**Domain:** Business Logic & State Management (Custom React Hooks)

## OVERVIEW
This directory contains custom hooks that encapsulate the business logic, state management, and data fetching for the KCouper application.

## STRUCTURE
```
src/hooks/
├── useCoupons.ts            # Data fetching and core coupon state
├── useFavorites.ts          # LocalStorage sync for favorite coupons
├── useCouponFilters.ts      # Logic for sorting and filtering logic
├── useAnnouncements.ts      # Fetching and state for announcements
├── useTour.ts               # Logic for user onboarding tour
└── ...                      # Feature-specific hooks
```

## WHERE TO LOOK
- **Coupon Data**: `useCoupons.ts` for initial load and data transformation from API/Static data.
- **Sorting/Filtering**: `useCouponFilters.ts` for search logic and tag-based filtering.
- **Persistence**: `useFavorites.ts` for `localStorage` interaction and state sync.

## CONVENTIONS
- **State Logic**: Encapsulate complex state logic in custom hooks to keep components thin.
- **Async Handling**: Use `@tanstack/react-query` or similar patterns for data fetching.
- **Return Pattern**: Always return an object `{ state, actions }` for consistency.
- **Memoization**: Use `useMemo` and `useCallback` for expensive filtering operations.

## ANTI-PATTERNS
- **Prop Overload**: Don't return too many variables from a hook; group by purpose.
- **Multiple Responsibilities**: Keep hooks focused; a hook should handle one feature domain.
- **Direct LocalStorage Access**: Use `useFavorites` or similar to centralize storage logic.
