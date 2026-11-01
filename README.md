<img width="1877" height="1493" alt="Zrzut ekranu 2026-01-06 123957" src="https://github.com/user-attachments/assets/1ae4a94f-20c7-48fb-82bf-ae1c52b0285f" />
 
<img width="1877" height="1493" alt="Restaurant system screenshot" src="https://github.com/user-attachments/assets/1ae4a94f-20c7-48fb-82bf-ae1c52b0285f" />

# 🍽️ Restaurant & Online Ordering System – Frontend

A **React.js** frontend application for a full restaurant ordering and management platform. It provides a complete user experience for customers, staff, and administrators by consuming a RESTful API backend ([restaurant-pos-backend](https://github.com/RafalSprengel/restaurant-pos-backend)) that is responsible for all business logic, authentication, payments, and data persistence.

The application is structured as a production-style system with a clear separation between the **public interface**, the **customer dashboard**, and the **administrative panel**.

## 🚀 Live Demo

👉 [restaurant.rafalsprengel.com](https://restaurant.rafalsprengel.com/)

---

## 🔑 Key Features

- **Menu Browser** – Dynamically renders products and categories fetched from the backend API, with category filtering, URL-driven pagination and a product details modal.
- **Cart Management** – Persistent shopping cart built on React Context and `localStorage`; on load, cart items are re-validated against the API and removed if a product no longer exists. Multi-step order flow (selection → checkout → payment).
- **Order Flow** – Full ordering process with **delivery**, **pickup** and **dine-in** options, ASAP or scheduled time, order notes, guest checkout and order history tracking.
- **User Accounts** – Cookie-based JWT authentication with registration, login (email/password, **Google** and **Facebook**) and profile management.
- **Admin / Staff Panel** – Role-based access control for managing products, categories, orders, customers, staff, reservations, messages, and system settings.
- **Table Reservations** – Table availability checked against the API for the selected date, with reservation creation and management.
- **Messaging System** – Contact form integrated with the backend messaging system; staff inbox with unread notification badge.
- **Payments Integration** – Secure Stripe-hosted checkout with a payment success / cancel flow and order confirmation.
- **Responsive UI** – Optimized for mobile, tablet, and desktop devices (including a collapsible admin sidebar).
- **Order Status Tracking** – UI feedback for payment state and order updates, with validation during checkout.

---

## 🧭 Application Overview

### 🍽 Public Restaurant Interface

- Landing page (hero, specials tabs, events slider, testimonials, team cards, image gallery with lightbox)
- Food menu generated from the backend database
- Shopping cart (cart modal + floating cart button) for online ordering
- Full order creation flow (delivery, pickup, dine-in)
- Stripe checkout integration
- Table reservation form with availability validation
- Contact form connected to the backend messaging system
- Cookie-consent banner and Google Tag Manager page-view tracking for the SPA

### 👤 Authentication & User System

- Cookie-based JWT authentication – tokens live in `httpOnly` cookies set by the API and are never accessible to JavaScript
- Session restored on page load via `GET /auth/session`
- **Automatic token refresh:** an Axios interceptor catches `401` responses, calls `/auth/refresh-token` and transparently retries the original request
- Graceful handling of API downtime – network errors and `502/503/504` redirect to a dedicated *No connection* page
- Secure login and registration flow; social login through Google and Facebook
- Role-based UI rendering (Customer / Staff roles: `guest`, `member`, `moderator`, `admin`)
- Separate login screens for customers (`/customer/login`) and staff (`/management/login`)

### 🛒 Customer Dashboard

Authenticated customers can manage their account and orders:

- View order history and order details (and remove orders from their list)
- Manage personal details and delivery address
- Change password
- Delete account

### 🛠 Admin Panel

A full-featured administrative interface for managing restaurant operations:

| Module | Description |
|--------|-------------|
| 📊 Dashboard | Overview of key business metrics with **Recharts** visualisations – most popular products, last 7 days revenue, top 5 product sales and latest transactions |
| 🍔 Product Management | Create, update, delete, and search products with image upload – dynamically reflected in the public menu |
| 🗂 Category Management | Manage product categories and menu structure |
| 👥 Customer Management | Search, edit, and manage registered users; account moderation and deletion |
| 📦 Order Management | View and update customer orders; track payment state and order status |
| 👨‍💼 Staff Management | Manage administrative users with role-based permissions and access control |
| 💬 Messaging System | Inbox for customer messages, read/unread tracking, reply, bulk delete and notification badges |
| 🪑 Table Reservations | View, search and manage reservations |
| ⚙️ System Settings | Reservation time rules, the maximum advance booking period, and email (SMTP) configuration |

> Buttons and actions are hidden in the UI according to the user's role (for example, `member` cannot add or delete categories). Permissions are always enforced again on the server.

---

## 🗺 Routes

| Area | Path | Description |
|------|------|-------------|
| Public | `/` | Landing page, menu, reservation and contact forms |
| Order | `/order/checkout`, `/order/success`, `/order/cancel` | Checkout and Stripe return pages |
| Customer | `/customer/login`, `/customer/register` | Customer authentication |
| Customer | `/customer`, `/customer/recent-orders`, `/customer/personal-details` | Customer dashboard |
| Management | `/management/login` | Staff login |
| Management | `/management` | Dashboard |
| Management | `/management/products`, `/products/:id`, `/add-product` | Products |
| Management | `/management/categories`, `/categories/:id`, `/add-category` | Categories |
| Management | `/management/customers`, `/customers/:id`, `/add-customer` | Customers |
| Management | `/management/orders`, `/orders/:id` | Orders |
| Management | `/management/mgnts`, `/mgnts/:id`, `/add-mgmt` | Staff |
| Management | `/management/messages`, `/messages/:id` | Messages |
| Management | `/management/reservations`, `/reservations/:id` | Reservations |
| Management | `/management/settings` | System settings |
| Utility | `/no-connection`, `*` | API-offline page, 404 |

---

## ⚙️ Technical Implementation

- **React 18** (component-based architecture, hooks) bootstrapped with **Create React App**
- **React Router v6** – nested routes and protected areas
- **REST API integration** with a shared **Axios** instance (`withCredentials`, response interceptors)
- **Context-based state management** – `AuthProvider` (session), `ShoppingCartProvider` (cart & product modal), `UnreadMessagesProvider` (admin badge)
- Custom hooks: `useFetch`, `useLocalStorage`, `useLocalStorageWithValidation`
- **Mantine 8** UI library (forms, modals, notifications, date pickers) with custom overrides
- **SCSS** styling with shared variables, BEM-style class naming, mobile-first responsive layout
- **Recharts** for dashboard charts
- UI polish: Framer Motion, AOS scroll animations, GLightbox gallery, lazy-loaded images, Tabler / Lucide / Font Awesome icons
- Modular structure separating public, customer, and admin areas
- **Stripe Checkout** – the frontend creates a checkout session through the API and redirects to the Stripe-hosted page, then confirms the payment on the success page
- **CI/CD:** GitHub Actions builds the app and deploys it to a VPS on every push to `main`

---

## 📌 Project Structure

```
├── public/               # Static assets, index.html (Google Tag Manager snippet)
└── src/
    ├── pages/            # Application routes (public, customer, admin, checkout, payment results)
    ├── components/       # Reusable UI components
    │   ├── customerPanel/    # Order history, personal details
    │   └── managementPanel/  # Admin modules: products, categories, customers, orders,
    │                         # staff, messages, reservations, settings, dashboard
    ├── context/          # Global state management (auth, cart, unread messages)
    ├── hooks/            # Custom hooks (useFetch, localStorage helpers)
    ├── layouts/          # Layouts for different application areas (Header, Footer, MainLayout)
    ├── utils/            # Axios instance, API error handling, helpers
    ├── styles/           # Global and component SCSS
    ├── img/              # Images
    ├── App.js            # Routes and providers
    └── config.js         # API URL
```

## 🧠 Purpose

This frontend application serves as the user-facing layer of a full-stack restaurant management system, designed as a production-ready SaaS-style platform for handling orders, reservations, payments, and restaurant operations.

## 🧰 Tech Stack

| Category | Technology |
|----------|------------|
| Framework | React 18, Create React App (`react-scripts` 5) |
| Routing | React Router v6 |
| UI | Mantine 8, SCSS (Sass) |
| HTTP | Axios |
| Charts | Recharts |
| Animation & media | Framer Motion, AOS, GLightbox, react-lazy-load-image-component |
| Dates | Day.js, date-fns, Flatpickr |
| Icons | Tabler Icons, Lucide, Font Awesome, React Icons |
| Analytics | Google Tag Manager (with cookie consent) |
| Payments | Stripe Checkout (via backend) |
| Tooling | Prettier, ESLint (CRA config), Jest + Testing Library |
| Deployment | GitHub Actions, rsync over SSH |

---

## 🚀 Getting Started

### Prerequisites

- Node.js 18+ and npm
- The [backend API](https://github.com/RafalSprengel/restaurant-pos-backend) running and reachable

### Installation

```bash
git clone <this-repository-url>
cd restaurant-system-frontend
npm install
```

### Configure the API address

The API address is currently set in code rather than in an `.env` file. To work against your own backend, update it in:

- `src/utils/axios.js` – `apiURL` (e.g. `https://localhost:3001/v1`)
- `src/config.js` – `API_URL`
- `src/pages/LoginCustomer.js` – Google / Facebook login redirect URLs

The backend must allow your frontend origin in its CORS list and, because authentication cookies are `Secure` + `SameSite=None`, both apps should be served over HTTPS.

### Available scripts

| Command | Description |
|---------|-------------|
| `npm start` | Start the development server (http://localhost:3000) |
| `npm run build` | Create a production build in `build/` |
| `npm test` | Run tests |
| `npm run deploy` | Build and publish to GitHub Pages (`gh-pages`) |

### Deployment

Pushing to `main` triggers the GitHub Actions workflow in `.github/workflows/deploy.yml`, which runs `npm ci`, builds the app and syncs the `build/` folder to the VPS over SSH (requires the `VPS_SSH_KEY` repository secret).

---

## 🔗 Related

- **Backend API:** [restaurant-pos-backend](https://github.com/RafalSprengel/restaurant-pos-backend) – Node.js, Express, MongoDB, Stripe
