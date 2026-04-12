# COMPONENTS KNOWLEDGE BASE

**Generated:** 2026-04-13
**Domain:** React Components (shadcn/ui + custom)

## OVERVIEW
This directory contains the UI layer of KCouper, built with React, Radix UI, and Tailwind CSS.

## STRUCTURE
```
src/components/
├── ui/                 # shadcn/ui primitives (Radix UI)
├── CouponCard.tsx      # Core display unit for coupons
├── CouponGrid.tsx      # Responsive grid container
├── SearchPanel.tsx     # Combined search and filter UI
└── ...                 # Other layout and feature components
```

## WHERE TO LOOK
- **shadcn/ui**: Check `src/components/ui/` for base components before creating new ones.
- **Card Logic**: `CouponCard.tsx` handles individual coupon formatting and favorite toggling.
- **Filtering UI**: `SearchPanel.tsx` and `ItemFilter.tsx` manage user input for filtering.

## CONVENTIONS
- **Component Pattern**: Use functional components with arrow functions.
- **Prop Types**: Define props using `interface` above the component.
- **Styling**: Prefer Tailwind classes. Use `cn()` utility for conditional classes.
- **Atomic Design**: Keep components small; lift state to hooks in `src/hooks/` when shared.

## ANTI-PATTERNS
- **Prop Drilling**: Don't pass data through more than 2 levels; use hooks or context.
- **Direct DOM Manipulation**: Always use React state/refs, never jQuery (only legacy v1 uses it).
- **Hardcoded Strings**: Extract common Chinese labels if used in multiple places.
