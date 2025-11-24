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
- **Fix**: Implemented a complete pagination system (prev/next, page jump, range indicator).
  - Added state management for `page` and `total` counts in `app/page.tsx`.
  - Updated data fetching logic to support `offset` based pagination.
  - Added "Previous" and "Next" navigation controls.
- **Why**: Users couldn't see all products. Pagination is standard for large lists.
- **Improvement**: Added a dynamic "Showing X-Y of Z" indicator and direct page input so users know where they are.

### [Functionality][UX] Filter Logic & Navigation
- **Issue**: Filtering had logic bugs (sticky dropdowns, incorrect subcategories) and inconsistent badge behavior across pages.
- **Fix**: Overhauled the filtering system to use URL parameters and fixed state synchronization.
  - Updated API fetching to correctly filter subcategories by the selected category.
  - Added logic to automatically clear the subcategory when the main category changes.
  - Added an "All Subcategories" option and used a `resetKey` to ensure dropdowns visually reset correctly.
  - Standardized all filter badges (on cards and details page) to use `Link` components with URL parameters.
  - Added `e.stopPropagation()` to product cards to prevent click conflicts between badges and the main card link.
- **Why**: URL-based filtering lets users share links. Consistent behavior stops users from getting confused.
- **Improvement**: Added "All Subcategories" option to make resetting filters easier.

### [Functionality] Unconfigured Image Host
- **Issue**: Images sourced from `images-na.ssl-images-amazon.com` failed to load due to missing domain configuration.
- **Fix**: Configured `next.config.ts` to include `images-na.ssl-images-amazon.com` in `remotePatterns`.
- **Why**: Next.js needs this config to optimize images from external sites.

### [Functionality] Product Image Runtime Crash
- **Issue**: The application encountered a `TypeError` runtime crash when attempting to render products with undefined `imageUrls`.
- **Fix**: Implemented defensive coding using optional chaining (`product.imageUrls?.[0]`) in `app/page.tsx`.
- **Why**: Stops the whole app from crashing if one product has bad data.

### [UI/Design] Card Alignment
- **Issue**: The "View Details" button wasn't aligned across cards because product tags have varying heights.
- **Fix**: Added `flex-1` to `CardContent` to push the footer to the bottom.
- **Why**: Makes the grid look much cleaner and aligned.

### [Security] Sensitive Data Exposure
- **Issue**: The application was passing the entire product object (including potentially sensitive fields) as a URL parameter (`?product={...}`).
- **Fix**: Changed the routing to pass only the product ID (`?id=...`) and fetch the product details securely from the API on the details page.
- **Why**: Passing full objects in URLs is insecure and can hit length limits. Fetching by ID ensures data is fresh.
