# 🔴 PINCELETAS  
### E-Commerce Platform · Microservices Architecture · Full Stack Project  

---

## 🚀 Overview

**Pinceletas** is a full-stack e-commerce platform developed as a thesis project, designed for an artisanal products business.

The system provides:

- 🛍 A complete online shopping experience for customers  
- 📊 An administrative dashboard with metrics and configuration tools  
- 🔐 Secure authentication with JWT and Firebase  
- 📦 A scalable microservices-based backend architecture  

This project was built with a strong focus on **clean architecture, service decoupling, security, and scalability**.

---

## 🧰 Tech Stack

### 🎨 Frontend
- Angular  
- Bootstrap  

### ⚙ Backend
- Java + Spring Boot  
- Microservices Architecture  
- REST APIs  

### 🔐 Security
- JWT Authentication  
- Firebase (Google OAuth + Email/Password)  
- Shared Security Library between services  

### 📡 Communication
- RabbitMQ (Asynchronous messaging)  

### 🗄 Database
- MySQL  

### 🧪 Testing
- JUnit  
- Mockito  

---

# 🏗 System Architecture

Pinceletas follows a **distributed microservices architecture**, where each service is responsible for a specific business domain.

The system is designed to ensure:

- 🔹 Separation of concerns  
- 🔹 Independent deployment  
- 🔹 Scalability  
- 🔹 Secure inter-service communication  
- 🔹 Asynchronous event-driven processing  

---

## 🧩 Services Breakdown

### 🔐 User & Auth Service
- User management  
- Role management  
- JWT generation & validation  
- Firebase authentication integration  

Repository:  
👉 https://github.com/agustinoliver/pinceletas-user-auth-service  

---

### 🛒 Commerce Service
- Product catalog  
- Categories  
- Shopping cart  
- Favorites  
- Order processing  
- Order status tracking  

Repository:  
👉 https://github.com/agustinoliver/pinceletas-commerce-service  

---

### ⚙ Admin & Config Service
- Site configuration  
- Contact information  
- Shipping methods  
- Platform metrics dashboard  

Repository:  
👉 https://github.com/agustinoliver/pinceletas-admin-config-service  

---

### 🔔 Notification Service
- Asynchronous event handling  
- Inter-service communication via RabbitMQ  
- Notification dispatch logic  

Repository:  
👉 https://github.com/agustinoliver/pinceletas-notification-service  

---

### 🎨 Frontend Application
- Customer interface  
- Admin panel  
- JWT token handling  
- API integration with backend services  

Repository:  
👉 https://github.com/agustinoliver/pinceletas-frontend  

---

# 🔁 Inter-Service Communication

The architecture combines:

- **Synchronous communication** (REST APIs)  
- **Asynchronous communication** (RabbitMQ message broker)  

This hybrid approach allows:

- Reduced coupling  
- Better fault tolerance  
- Event-driven workflows (e.g., order creation → notification dispatch)  

JWT validation is shared through a common security module to ensure consistent authentication across services.

---

# 👤 Core Features

## 🛍 Customer Experience
- Secure registration & login (Email / Google)  
- Product exploration with filters  
- Favorites & shopping cart  
- Order history & status tracking  
- WhatsApp contact integration  
- AI Chatbot for common inquiries  
- Editable user profile  

## 📊 Administrative Panel
- CRUD operations for products & categories  
- Order management  
- Platform configuration  
- Real-time metrics dashboard  

---

# 🎯 Architectural Decisions

✔ Domain-driven service separation  
✔ Stateless authentication using JWT  
✔ Shared security module for consistency  
✔ Event-driven communication for notifications  
✔ Clean layered structure inside each service  
✔ Independent repository per microservice  

---

# 📌 Authors

Developed by:

**Tomas Herrado**  
**Agustín Olivera**

📍 Thesis Project – Programming Technician Degree  
