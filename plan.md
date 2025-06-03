# System Architecture and Implementation Plan for Atendimento Site Echodoor

## Overview
Build a full-stack Next.js application with authentication, role-based access, and management for representatives, clients, products, and orders. Includes admin area for full control.

## Tech Stack
- Frontend: Next.js, React, Tailwind CSS, shadcn UI components
- Backend: Next.js API routes
- Database: Prisma ORM with SQLite (or PostgreSQL if preferred)
- Authentication: NextAuth.js with email/password and role-based access (admin, representative)
- Email: Nodemailer for sending order confirmation emails
- PDF Generation: pdf-lib or similar for order PDF export

## Database Schema (Prisma)
- User (id, name, email, passwordHash, role [admin|representative], createdAt, updatedAt)
- Client (id, representativeId (FK), name, fantasyName, address, city, state, cep, cnpj, phone1, phone2, email, buyer, storePhotoUrl, createdAt, updatedAt)
- Product (id, name, description, basePrice, sizes [size, price], createdAt, updatedAt)
- Order (id, representativeId (FK), clientId (FK), orderNumber, paymentCondition, paymentMethod, freight, transport, observation, status [Received, In Expedition, Sent, Delivered], totalValue, createdAt, updatedAt)
- OrderItem (id, orderId (FK), productId (FK), size, quantity, unitPrice, totalPrice)

## Features
### Representative Area
- Login/Register (admin creates reps)
- Manage clients (CRUD)
- Create orders: select client, add products with size and quantity, cart with total price
- Submit order: confirmation message, email copy sent
- View orders with status (cannot change status)
- Download order PDF

### Admin Area
- Login as admin
- Manage representatives (CRUD)
- Manage clients of all reps (CRUD)
- Manage products (CRUD)
- Manage orders: change status, edit orders and clients
- View all orders

## API Routes
- /api/auth/* (NextAuth)
- /api/clients/* (CRUD, filtered by rep or all for admin)
- /api/products/* (CRUD for admin)
- /api/orders/* (CRUD, filtered by rep or all for admin)
- /api/representatives/* (CRUD for admin)
- /api/send-order-email (send order confirmation email)

## UI Pages
- /login
- /admin/dashboard
- /admin/representatives
- /admin/clients
- /admin/products
- /admin/orders
- /representative/dashboard
- /representative/clients
- /representative/orders
- /representative/create-order
- /representative/create-client

## Next Steps
- Setup Next.js project with Prisma and NextAuth
- Implement database schema and migrations
- Build authentication and role-based access
- Develop admin and representative UI pages and API routes
- Implement email sending and PDF generation
- Test and deploy

---

This plan covers all user requirements and screenshots provided. Please confirm or provide feedback before I start implementation.
