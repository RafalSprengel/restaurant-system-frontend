<img width="1877" height="1493" alt="Zrzut ekranu 2026-01-06 123957" src="https://github.com/user-attachments/assets/1ae4a94f-20c7-48fb-82bf-ae1c52b0285f" />
 
# 🍽️ Restaurant & Online Ordering System – Frontend

A **React.js** frontend application for a full restaurant ordering and management platform. It provides a complete user experience for customers, staff, and administrators by consuming a RESTful API backend responsible for all business logic, authentication, payments, and data persistence.

The application is structured as a production-style system with clear separation between the public interface, customer dashboard, and administrative panel.

---

## 🚀 Live Demo

👉 [restaurant.rafalsprengel.com](https://restaurant.rafalsprengel.com/)

---

## 🔑 Key Features

- **Menu Browser** – Dynamically renders products and categories fetched from the backend API
- **Cart Management** – Persistent shopping cart using React Context with a multi-step order flow (selection → checkout → payment)
- **Order Flow** – Full ordering process including delivery, dine-in, and takeaway options with order history tracking
- **User Accounts** – JWT-based authentication with registration, login, and profile management
- **Admin / Staff Panel** – Role-based access control for managing products, categories, orders, reservations, messages, and system settings
- **Table Reservations** – Real-time table availability checking with reservation creation and management
- **Messaging System** – Contact form integration with backend messaging system and notification tracking
- **Payments Integration** – Secure Stripe-based payment processing with order confirmation flow
- **Responsive UI** – Fully optimized for mobile, tablet, and desktop devices
- **Order Status Tracking** – Real-time UI feedback for order states and validation during checkout

---

## 🧭 Application Overview

### 🍽 Public Restaurant Interface

The public-facing part of the application allows users to interact with the restaurant system:

- Landing page with dynamic content
- Food menu generated from backend database
- Shopping cart system for online ordering
- Full order creation flow (delivery, dine-in, takeaway)
- Stripe checkout integration
- Table reservation form with real-time availability validation
- Image gallery showcasing restaurant content
- Contact form connected to backend messaging system

### 👤 Authentication & User System

- JWT-based authentication system
- Secure login and registration flow
- Role-based UI rendering (Customer / Admin / Staff)
- Persistent session handling via token storage

### 🛒 Customer Dashboard

Authenticated users can manage their account and orders:

- View order history and order details
- Manage delivery address
- Change password
- Delete account
- Track personal order activity

---

## 🛠 Admin Panel

A full-featured administrative interface for managing restaurant operations:

| Module | Description |
|---|---|
| 📊 **Dashboard** | Overview of key business metrics and system status |
| 🍔 **Product Management** | Create, update, delete, and search products — dynamically reflected in the public menu |
| 🗂 **Category Management** | Manage product categories and menu structure |
| 👥 **Customer Management** | Search, edit, and manage registered users; account moderation and deletion |
| 📦 **Order Management** | View and update customer orders; track order lifecycle and status changes |
| 👨‍💼 **Staff Management** | Manage administrative users with role-based permissions and access control |
| 💬 **Messaging System** | Inbox for customer messages, read/unread tracking, quick reply, and notification badges |
| 🪑 **Table Reservations** | View and manage reservations with conflict detection and real-time availability logic |
| ⚙️ **System Settings** | Reservation time rules, booking constraints (min/max advance time), and email configuration |

---

## ⚙️ Technical Implementation

- **React.js** (component-based architecture)
- REST API integration with backend
- Role-based routing system (protected routes)
- Context-based state management (auth, cart, UI state)
- Modular structure separating public, customer, and admin areas
- Responsive design (mobile-first approach)
- API-driven UI rendering
- Stripe checkout integration
- Real-time UI feedback for order and reservation flows

---

## 📌 Project Structure

```
├── pages/        # Application routes (public, customer, admin)
├── components/   # Reusable UI components
├── context/      # Global state management (auth, cart)
├── services/     # API communication layer
├── layouts/      # Layouts for different application areas
└── utils/        # Helper functions
```

---

## 🧠 Purpose

This frontend application serves as the user-facing layer of a full-stack restaurant management system, designed as a production-ready SaaS-style platform for handling orders, reservations, payments, and restaurant operations.

---

## 📄 License

This project is licensed under the MIT License.
