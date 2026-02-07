Music Store Project - Final Project for Advanced Databases (NoSQL)
Project Overview

This project is a web-based music store where users can view products (musical instruments), place orders, and manage their profile. The backend is built using Node.js and MongoDB as the database, with a frontend built using basic HTML, CSS, and JavaScript.

Technologies Used:

Backend: Node.js, Express.js

Database: MongoDB

Frontend: HTML, CSS, JavaScript

Authentication: JWT (JSON Web Token)

RESTful API: Exposed for communication between frontend and backend

Aggregation Framework: For generating statistics such as total revenue and order counts

Features:

User Authentication: Users can sign in using their email and password, and they are assigned roles (user or admin).

Product Listings: Users can view products (instruments) with their details like name, category, price, and stock.

Create Orders: Logged-in users can add products to their cart and create an order.

Admin Features: Admin users can view sales statistics and manage products.

Frontend Pages:

Login Page: Users can log in to access their account.

Products Page: Users can see a list of products.

Orders Page: Users can view their order history.

Create Order Page: Users can place a new order by selecting products.

Database Structure

The application uses MongoDB with the following collections:

Users Collection

_id: Unique identifier for the user.

name: The user's full name.

email: User's email (unique).

passwordHash: Hashed password for security.

role: User's role (user or admin).

Products Collection

_id: Unique identifier for the product.

name: Name of the product (e.g., "Acoustic Guitar").

category: Category of the product (e.g., "guitar", "piano").

brand: Brand name (e.g., "Fender").

price: Price of the product.

stock: Available stock.

description: Detailed description of the product.

tags: Keywords for product filtering (e.g., "beginner", "acoustic").

ratingAvg: Average rating from customers.

ratingCount: Number of ratings.

Orders Collection

_id: Unique order identifier.

userId: The user who placed the order (references the Users collection).

items: Embedded array of products in the order, including product name, price, and quantity.

total: Total price of the order.

status: Order status (e.g., pending, shipped).

createdAt: Date and time the order was placed.

API Endpoints

The backend exposes the following RESTful API endpoints:

Authentication

POST /auth/login: Logs in a user and returns a JWT token.

POST /auth/register: Registers a new user.

Products

GET /products: Retrieves a list of all products.

POST /products: Adds a new product (admin only).

PATCH /products/stock: Updates stock for a product (admin only).

Orders

POST /orders: Creates a new order for the logged-in user.

GET /orders/my: Retrieves the order history for the logged-in user.

GET /orders/stats/sales: Retrieves sales statistics for the admin user.

Admin

GET /admin/stats/sales: Retrieves sales statistics (total revenue and order count) for the admin.

Installation and Setup
Requirements

Node.js installed on your machine.

MongoDB running locally or a MongoDB Atlas account.

Setup

Clone the repository:

git clone https://github.com/your-username/music-store.git


Navigate to the project directory:

cd music-store


Install dependencies:

npm install


Create a .env file in the root directory and add your environment variables:

JWT_SECRET=your-secret-key
MONGO_URI=mongodb://localhost:27017/music_store
PORT=3000


Start the backend server:

npm run dev


Frontend is available by opening index.html in a browser.

API Documentation

Here are some example API calls:

Login Example

Request:

POST /auth/login


Body:

{
  "email": "test1@mail.com",
  "password": "123456"
}


Response:

{
  "token": "your-jwt-token"
}

MongoDB Aggregation Example

Sales Aggregation Endpoint: /admin/stats/sales
Example:

Request:

GET /admin/stats/sales


Response:

{
  "totalRevenue": 5000,
  "ordersCount": 120
}


This example aggregates the total revenue and number of orders.

Conclusion

This project is a simple music store application that allows users to browse products, place orders, and admins to view sales statistics. The application uses MongoDB as the backend database, and MongoDB aggregation pipelines are utilized for advanced data analysis.
