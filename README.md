# 🎨 PINCELETAS
### E-Commerce Platform · Microservices Architecture · Full Stack Project

---

## 🚀 Overview

**Pinceletas** is a full-stack e-commerce platform developed as a Final Integrative Project for the Programming Technician degree at Universidad Tecnológica Nacional (UTN), Regional Córdoba. The platform was designed specifically to address the needs of artisanal product businesses, providing a scalable and production-ready solution.

The system delivers:

- 🛍️ A complete online shopping experience for end customers
- 📊 A consolidated administrative dashboard with real-time metrics, reporting, and configuration tools
- 🔐 Secure authentication via JWT and Firebase (Google OAuth)
- 🔔 Real-time notification system powered by asynchronous messaging
- 📦 A distributed microservices backend architecture ready for production

This project was built with a strong focus on **clean architecture, service decoupling, security, scalability, and maintainability**.

🌐 **Live Site:** [pinceletas-frontend.onrender.com](https://pinceletas-frontend.onrender.com/)

---

## 🧰 Tech Stack

### 🎨 Frontend
- **Angular** — SPA framework for both the customer-facing storefront and the admin panel
- **Bootstrap** — Responsive UI components

### ⚙️ Backend
- **Java + Spring Boot** — Microservices implementation
- **REST APIs** — Synchronous inter-service and client-server communication
- **Swagger / OpenAPI** — API documentation for all services

### 🔐 Security
- **JWT** — Stateless authentication and authorization across all services
- **Firebase** — Google OAuth and social login integration
- **Shared Security Library** — Common authentication module reused across microservices

### 📡 Asynchronous Communication
- **RabbitMQ (CloudAMQP)** — Message broker for event-driven workflows between services

### 🗄️ Database
- **PostgreSQL** — Primary relational database for all services

### ☁️ External Services Integrated
| Service | Purpose |
|---|---|
| **Mercado Pago** | Secure online payment processing |
| **Firebase** | Social authentication (Google) |
| **ImgBB API** | Product image storage and management |
| **Resend** | Transactional email delivery |
| **RabbitMQ / CloudAMQP** | Asynchronous inter-service messaging |
| **CountriesNow / RestCountries** | Address autocomplete (country & province) |

### 🚢 Deployment
- **Render** — Cloud deployment platform for all services and the frontend

### 🧪 Testing & Tooling
- **JUnit + Mockito** — Unit and integration testing
- **Jira Software** — Sprint planning and project tracking
- **Git** — Version control, one repository per microservice

---

## 🏗️ System Architecture

Pinceletas follows a **distributed microservices architecture**, where each service owns a specific business domain and can be deployed, scaled, and maintained independently.

```
┌─────────────────────────────────────────────────────────┐
│                     Angular Frontend                    │
│          (Customer Storefront + Admin Panel)            │
└──────────────────────────┬──────────────────────────────┘
                           │ REST (JWT-secured)
           ┌───────────────┼───────────────┐
           │               │               │
    ┌──────▼──────┐  ┌──────▼──────┐  ┌──────▼──────┐
    │  User &     │  │  Commerce   │  │  Admin &    │
    │ Auth Svc    │  │   Service   │  │ Config Svc  │
    └──────┬──────┘  └──────┬──────┘  └─────────────┘
           │                │
           └───────┬────────┘
                   │ RabbitMQ (Async Events)
           ┌───────▼────────┐
           │  Notification  │
           │    Service     │
           └────────────────┘
```

The architecture guarantees:
- 🔹 Separation of concerns by business domain
- 🔹 Independent deployment per service
- 🔹 Horizontal scalability
- 🔹 Secure inter-service communication via shared JWT validation
- 🔹 Asynchronous, event-driven processing via RabbitMQ

---

## 🧩 Services Breakdown

### 🔐 User & Auth Service
Handles everything related to identity and access management.

**Responsibilities:**
- User registration, profile editing, and account management
- Role management (`USER`, `ADMIN`)
- JWT token generation and validation
- Firebase / Google OAuth integration
- Password recovery via temporary email tokens
- User address management with country/province autocomplete
- Terms & conditions acceptance tracking
- User activity reporting (active/inactive)

📁 Repository: [pinceletas-user-auth-service](https://github.com/agustinoliver/pinceletas-user-auth-service)

---

### 🛒 Commerce Service
The core business domain service, covering the full shopping lifecycle.

**Responsibilities:**
- Product catalog with CRUD, multi-image support, variants (e.g., color), and discounts
- Hierarchical category management with audit trail
- Advanced product search and filtering
- Favorites management with automatic event notifications
- Shopping cart with dynamic subtotal, shipping cost, and total calculation
- Order processing with full lifecycle tracking
- Mercado Pago integration: payment creation, webhook handling, session restoration post-payment
- Audit logging for products and orders
- Reporting: best-selling products, orders by date/status — exportable to Excel

📁 Repository: [pinceletas-commerce-service](https://github.com/agustinoliver/pinceletas-commerce-service)

---

### ⚙️ Admin & Config Service
Centralizes all platform-level configuration and administrative reporting.

**Responsibilities:**
- Site contact information management
- Physical store information
- Shipping configuration
- Purchase and return policy management
- Consolidated administrative dashboard with cross-module metrics:
  - Active/inactive users
  - Product statistics (total, active, inactive, by category)
  - Best-selling product charts
  - Order analysis by date and status
  - Purchase reports by user with date filters

📁 Repository: [pinceletas-admin-config-service](https://github.com/agustinoliver/pinceletas-admin-config-service)

---

### 🔔 Notification Service
Decoupled service responsible for the real-time notification system.

**Responsibilities:**
- Listens to system events via RabbitMQ (orders, payments, favorites, etc.)
- Persists notifications to the database with `NEW` / `READ` status
- Unread notification count per user
- Individual and bulk mark-as-read
- Notification filtering by user and status
- Transactional email dispatch via Resend

**Notification Flow:**
```
System Event → Backend publishes to RabbitMQ
    → Notification Service consumes event
    → Creates notification (status: NEW) in DB
    → Frontend polls every 30s
    → User views & marks as READ
```

📁 Repository: [pinceletas-notification-service](https://github.com/agustinoliver/pinceletas-notification-service)

---

### 🎨 Frontend Application
Single Angular application serving both the customer storefront and the admin panel.

**Responsibilities:**
- Product browsing, filtering, and detail views
- Favorites and shopping cart management
- Checkout flow with Mercado Pago redirect and session restoration
- Order history and status tracking
- User profile and address management
- AI Chatbot for common customer inquiries
- Direct messaging channel between users and admin (WhatsApp integration)
- Full admin panel: products, categories, orders, configurations, dashboard, and reports
- JWT interceptor for automatic token attachment to all API requests

📁 Repository: [pinceletas-frontend](https://github.com/agustinoliver/pinceletas-frontend)

---

## 🔁 Inter-Service Communication

The architecture uses a **hybrid communication model**:

| Type | Technology | Use Case |
|---|---|---|
| **Synchronous** | REST API | Client ↔ Backend, Admin queries |
| **Asynchronous** | RabbitMQ | Order events → Notification dispatch, Favorites events → Notifications |

---

## 👤 Core Features

### 🛍️ Customer Experience
- Secure registration and login (email/password or Google)
- Product catalog with search, filters, and variants
- Favorites list with automatic notifications
- Shopping cart with real-time cost calculation
- Checkout via Mercado Pago with session restoration
- Order history and status tracking
- Editable user profile and multiple delivery addresses
- AI Chatbot for FAQ resolution
- Direct WhatsApp communication channel with administrators

### 📊 Administrative Panel
- Full product and category CRUD with audit trail
- Order management and status updates
- Platform configuration (contact, shipping, policies, store locations)
- Real-time metrics dashboard
- Detailed reports exportable to Excel
- User management with role assignment

---

## 🎯 Architectural Decisions

| Decision | Rationale |
|---|---|
| Domain-driven service separation | Each service owns its data and logic, enabling independent evolution |
| Stateless JWT authentication | Enables scalability without server-side session management |
| Shared security library | Prevents duplication and ensures consistent auth enforcement |
| RabbitMQ for notifications | Decouples event producers from consumers; improves fault tolerance |
| PostgreSQL per service | Each service has its own database to avoid tight coupling |
| Render for deployment | Unified cloud platform for all services and frontend |
| One Git repo per microservice | Independent versioning and deployment pipelines |

---

## 📌 Project Management

- **Methodology:** Agile — 2-week sprints
- **Tool:** Jira Software
- **Jira Board:** [pinceletas-tesis.atlassian.net](https://pinceletas-tesis.atlassian.net/jira/software/projects/SCRUM/boards/1)

---

## 👥 Authors

Developed by:

**Tomás Herrado** ·
**Agustín Olivera** 
