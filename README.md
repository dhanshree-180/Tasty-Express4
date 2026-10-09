# Tasty Express 2.0

A modernized React rebuild of the original Tasty Express site
(https://dhanshree-11.github.io/TastyExpress_1/), preserving the brand's
name, logo, menu, prices, and personality while upgrading the frontend to a
component-based React app with a working cart, search/filtering, and full
responsiveness.

## Run it

```bash
npm install
npm run dev       # local dev server
npm run build     # production build → dist/
npm run preview   # preview the production build
```

## Structure

```
src/
  components/   Navbar, Footer, Hero, MenuCard, CartDrawer, Testimonials, SectionHeading
  pages/        Home, Menu, About, DineIn, Contact, Account, NotFound
  layouts/      MainLayout (navbar + footer + cart drawer shell, used by every route)
  context/      CartContext (cart state + localStorage), ToastContext (notifications)
  hooks/        useLocalStorage, useReveal (scroll-in animation)
  data/         menuData.js — all menu items, categories, testimonials, brand info
```

## Content decisions carried over from the original site

- **All menu items, categories, and prices are unchanged** from the original
  (`indexM.html`) — sourced directly from the live site.
- **"Veggie Loaded Pizza"** was shown on the original homepage but was
  missing from the Menu page entirely. It's now added under a new "Pizza"
  category with an **estimated price of ₹149** (marked with `priceIsEstimate`
  in `menuData.js` and a `*` next to the price in the UI) — the original
  site never listed a price for it, so double check this before launch.
- **The Contact page** was leftover template copy for a different business
  ("The Gourmet Spoon") in the original site. It's been rebuilt using Tasty
  Express's real address, phone, email, and hours (pulled from the
  footer/Dine-In page of the original site).
- **Images** currently point at the original site's asset files (same
  AI-generated/Freepik-watermarked stock photos used before) so nothing
  visually "breaks" — but they carry a visible watermark and aren't licensed
  for production use. Swap `image` fields in `src/data/menuData.js` for
  licensed photography before this goes live or into a portfolio.

## Backend-readiness

- `CartContext` and `ToastContext` are the only global state; swapping mock
  `menuData.js` for an API call (e.g. `fetch('/api/menu')`) requires no
  component changes — `Menu.jsx` and `Home.jsx` just consume whatever array
  the data layer returns.
- The Account page (`src/pages/Account.jsx`) currently mocks login/signup —
  wire its `handleSubmit` to a real auth endpoint when ready.
- The cart's "Proceed to Checkout" button is a placeholder — plug in your
  payment gateway/order API where indicated in `CartDrawer.jsx`.
