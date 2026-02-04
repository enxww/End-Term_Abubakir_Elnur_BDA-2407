# Music Store – Advanced NoSQL Project

Course: Advanced Databases (NoSQL)  
Full-stack web application built with MongoDB, Node.js and a vanilla frontend.

---

## Project Overview

Music Store is an online instrument shop system where users can:
- Register and login
- Browse musical instruments
- Create orders
- View their orders
- Admin can manage products
- Perform analytical queries using MongoDB aggregation

The goal of the project is to demonstrate advanced NoSQL modeling, MongoDB queries, and REST API design.

---

## System Architecture

Frontend (HTML/JS/CSS)  
→ REST API (Express.js)  
→ MongoDB (Mongoose ODM)

JWT tokens are used for authentication and role-based authorization.

---

## Database Design

### Collections

#### users
- _id
- name
- email (unique)
- passwordHash
- role

#### products
- _id
- name
- category
- brand
- price
- stock
- description
- tags[]
- ratingAvg
- ratingCount

Indexes:
- compound { category, price }
- text index on name, brand, description

#### orders
- _id
- userId → users._id
- items[] (embedded)
  - productId → products._id
  - nameSnapshot
  - priceSnapshot
  - qty
- total
- status
- createdAt

Indexes:
- compound { userId, createdAt }

---

## Embedded & Referenced Models

- Orders embed order items
- Orders reference users and products
- Snapshot fields preserve historical prices

---

## Security

- JWT authentication
- Authorization middleware
- Admin role
- Protected routes

---

## Aggregation Pipelines

Implemented multi-stage pipelines:
- Total sales statistics
- Orders summary per user
- Revenue calculations

Stages include:
$match → $group → $unwind → $sort

---

## REST API Endpoints

### Auth
POST /auth/login  
POST /auth/register  

### Products
GET /products  
GET /products/:id  
POST /products  
PATCH /products/:id  
DELETE /products/:id  

### Orders
POST /orders  
GET /orders/my  
GET /orders/stats/sales  

---

## Setup

### Backend
