# Repository Guidelines

## Response to Questions

- Please response to any questions or concerns in Japanese.

## Project Structure & Module Organization

- `src/pages/`: Astro pages (`index.astro` drives the storefront demo).
- `src/layouts/`: Shared layouts; `Layout.astro` wires navigation and cart UI.
- `src/components/`: Preact and Astro components (cart flyout, add-to-cart form, product description).
- `src/cartStore.ts`: Nanostores state (cart open flag, cart items).
- `src/utils.ts`: Small helpers (e.g., `withBase` for asset paths).
- `public/`: Static assets (favicon, product images). Served as-is.

## Build, Test, and Development Commands

- `npm install`: Install dependencies.
- `npm run dev`: Start Astro dev server (default http://localhost:4321/). Ideal for local testing.
- `npm run build`: Production build to `dist/`.
- `npm run preview`: Serve the built `dist/` for smoke-testing.
- `npm run astro -- <cmd>`: Run arbitrary Astro CLI commands when needed.

## Coding Style & Naming Conventions

- Language: TypeScript for logic, Astro for pages/layouts, CSS modules for component styles.
- Indentation: Tabs in existing files; match surrounding style.
- Components: PascalCase filenames for Preact/React-like components (`CartFlyout.tsx`), kebab or lowercase for Astro pages by route (`index.astro`).
- State: Use Nanostores (`atom`, `map`) for shared client state; colocate store updates in `cartStore.ts`.
- Imports: Prefer relative paths within `src/`; keep public assets under `public/`.

## Testing Guidelines

- No automated tests are present. For changes, at minimum run `npm run dev` and exercise:
  - Add to cart, toggle cart open/close, verify quantities increment.
  - Asset paths resolve via `withBase` when a non-root `BASE_URL` is set.
- If adding tests, align with Astro/Preact ecosystem (e.g., Vitest + @testing-library/preact).

## Commit & Pull Request Guidelines

- Commits: Keep messages imperative and scoped (e.g., `Add cart quantity badge`, `Fix base path for images`).
- Pull Requests: Include a short description, reproduction steps if fixing a bug, and screenshots/GIFs for UI changes.
- Note any dev-server commands used and manual checks performed (cart add, toggle, build/preview).

## Architecture Notes

- Astro islands: Interactive pieces (`CartFlyout`, `CartFlyoutToggle`, `AddToCartForm`) load via `client:load`; the rest is static.
- State flow: `cartStore.ts` holds the single source of truth; UI components subscribe with `useStore`.
- Base URLs: Use `withBase()` for public asset paths to support non-root deployments.
