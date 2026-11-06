# Krishi Market — Farmer-to-Consumer Agri Marketplace

**From Local Farms to Your Home.** Krishi Market is a full-stack prototype web
application that connects Indian farmers directly with consumers, removing
middlemen so farmers earn more and consumers pay less for fresh, traceable
produce.

> This is a **demo/prototype**. All data shown (farmers, products, orders,
> reviews, prices) is **sample data** for demonstration purposes only. No real
> transactions, payments, or deliveries occur.

---

## Features

### For Consumers
- Browse and shop fresh produce by category, location, farming method, price, and rating
- Product detail pages with a full **farm-to-fork traceability timeline**
- Add to cart, wishlist, and save favourite farmers
- Multi-step checkout (address → delivery slot → payment → confirmation)
- Order tracking with a live status timeline
- Write and read product and farmer reviews
- Consumer dashboard: orders, wishlist, saved farmers, addresses, reviews, notifications

### For Farmers
- 4-step guided farmer registration (Personal → Farm → Verification → Business)
- Farmer dashboard with sales charts, recent orders, and inventory tables
- Add / edit / delete products, toggle availability
- Manage orders and advance order status
- Sales analytics with monthly revenue charts and top-selling products
- Editable public farmer profile with cover image, story, and crops

### For Admins
- Admin dashboard with platform-wide stats and charts
- Farmer approval workflow (approve / reject / suspend)
- Product, order, category, and consumer management
- Analytics: orders, revenue, farmer growth, consumer growth, popular categories
- Commission tracking with 5% platform commission
- Platform settings (name, email, commission rate, delivery fees)

### Platform
- Role-based authentication (consumer / farmer / admin) with protected routes
- Toast notifications, search with suggestions, responsive mobile-first design
- All data persists to `localStorage` (structured for easy backend migration)
- INR (₹) pricing throughout, Indian locations and crop content

---

## Tech Stack

| Layer | Technology |
|------|-------------|
| Framework | React 18 + TypeScript |
| Build tool | Vite 5 |
| Styling | Tailwind CSS 3 |
| Routing | React Router v7 |
| Icons | Lucide React |
| State | React Context (Data, Auth, Cart, Toast) |
| Data layer | localStorage mock store (migration-ready) |

---

## Getting Started

### Prerequisites
- Node.js 18+ and npm

### Installation
```bash
npm install
npm run dev      # start dev server
npm run build    # production build → dist/
npm run preview  # preview production build
npm run typecheck # type-check only
```

---

## Demo Accounts

All three demo accounts share the password **`demo123`**.

| Role | Email | Use for |
|------|-------|---------|
| Consumer | `consumer@krishimarket.demo` | Shopping, cart, checkout, order tracking |
| Farmer | `farmer@krishimarket.demo` | Farmer dashboard, product/order management |
| Admin | `admin@krishimarket.demo` | Approvals, platform management, analytics |

On the **Login** page you can click a demo-account button to auto-fill the
credentials.

---

## Project Structure

```
src/
├── components/        # Reusable UI (Navbar, Footer, ProductCard, charts, etc.)
├── context/           # DataContext, AuthContext, CartContext, ToastContext
├── data/              # seed.ts — all sample/demo data
├── layouts/           # MainLayout, DashboardLayout
├── pages/
│   ├──                # Public pages (Home, Shop, ProductDetail, Cart, Checkout…)
│   ├── farmer/        # Farmer dashboard pages
│   ├── consumer/      # Consumer dashboard pages
│   ├── admin/         # Admin dashboard pages
│   └── shared/        # Notifications, Settings
├── types/             # TypeScript interfaces
├── utils/             # format helpers (INR, dates, ids)
├── App.tsx            # Routing
├── main.tsx           # Provider tree + render
└── index.css          # Tailwind + animations
```

---

## Data Layer

The app uses a `localStorage`-backed mock data layer seeded from `src/data/seed.ts`.

- `DataContext` is the central store (users, farmers, products, orders, reviews,
  notifications, categories) and auto-persists every mutation to
  `localStorage` under `krishi_market_data`.
- `AuthContext` persists sessions under `krishi_market_auth`.
- `CartContext` persists the cart under `krishi_market_cart`.

The store's CRUD interface is intentionally shaped like a database/ORM layer so
it can be swapped for Supabase or a MongoDB-backed Express API with minimal
changes to calling components.

### Migrating to a backend
Replace the methods inside `DataContext` with Supabase client calls (or fetch
calls to an Express API) that return the same shapes. Components consume data
through context hooks and do not reference the storage mechanism directly.

---

## Environment Variables

The current prototype requires **no** environment variables — all data is local.
When migrating to Supabase, the following are expected to be provisioned
automatically by the hosting environment:

- `SUPABASE_URL`
- `SUPABASE_ANON_KEY`
- `SUPABASE_SERVICE_ROLE_KEY`

Never commit real service-role keys to the repository.

---

## Disclaimer

Krishi Market is a portfolio/prototype project. All farmers, products, prices,
orders, reviews, and ratings are **fictional sample data**. Contact details,
legal pages, and payment screens are placeholders and should not be used for
real transactions.
