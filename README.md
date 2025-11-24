# Stackline Full Stack Assignment

## Overview

This is a sample eCommerce website that includes:
- Product List Page
- Search Results Page
- Product Detail Page

## Getting Started

```bash
yarn install
yarn dev
```

## Bug Fixes & Improvements

### [Functionality][UX] Page Navigation & Pagination
- **Issue**: The product list page lacked navigation controls, limiting access to only the first 20 products.
- **Fix**: Implemented a complete pagination system to improve data accessibility and user navigation.
  - Added state management for `page` and `total` counts in `app/page.tsx`.
  - Updated data fetching logic to support `offset` based pagination.
  - Added "Previous" and "Next" navigation controls.
  - Implemented a dynamic page indicator (e.g., "1 / 25") with direct page jump functionality via input.
  - Enhanced the product count display to show the specific range of visible items (e.g., "Showing 1-20 of 500 products").

### [Functionality] Unconfigured Image Host
- **Issue**: Images sourced from `images-na.ssl-images-amazon.com` failed to load due to missing domain configuration.
- **Fix**: Configured `next.config.ts` to include `images-na.ssl-images-amazon.com` in `remotePatterns`, enabling secure image optimization and loading.

### [Functionality] Product Image Runtime Crash
- **Issue**: The application encountered a `TypeError` runtime crash when attempting to render products with undefined `imageUrls`.
- **Fix**: Implemented defensive coding using optional chaining (`product.imageUrls?.[0]`) in `app/page.tsx` to safely handle missing image data without crashing the UI.
