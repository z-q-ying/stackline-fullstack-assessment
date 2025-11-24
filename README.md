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

### [Functionality][UX] Filter Logic & UI State
- **Issue**: Filtering was buggy—subcategories didn't update when changing categories, and once a subcategory was picked, you couldn't unselect it without clearing everything.
- **Fix**:
  - Updated the API fetch to filter subcategories by the selected category.
  - Added an "All Subcategories" option to the dropdown for easy resetting.
  - Added logic to automatically clear the subcategory when the main category changes.
  - Used a `resetKey` to force the Category dropdown to visually reset when clicking "Clear Filters".

### [Functionality] Unconfigured Image Host
- **Issue**: Images sourced from `images-na.ssl-images-amazon.com` failed to load due to missing domain configuration.
- **Fix**: Configured `next.config.ts` to include `images-na.ssl-images-amazon.com` in `remotePatterns`, enabling secure image optimization and loading.

### [Functionality] Product Image Runtime Crash
- **Issue**: The application encountered a `TypeError` runtime crash when attempting to render products with undefined `imageUrls`.
- **Fix**: Implemented defensive coding using optional chaining (`product.imageUrls?.[0]`) in `app/page.tsx` to safely handle missing image data without crashing the UI.

### [UI/Design] Card Alignment
- **Issue**: The "View Details" button wasn't aligned across cards because product tags have varying heights.
- **Fix**: Added `flex-1` to `CardContent` to push the footer to the bottom, making all cards consistent.

### [Security] Sensitive Data Exposure
- **Issue**: The application was passing the entire product object (including potentially sensitive fields) as a URL parameter (`?product={...}`).
- **Fix**: Changed the routing to pass only the product ID (`?id=...`) and fetch the product details securely from the API on the details page.
