
# Music Store Project

## Overview

This is a web-based music store built as a final project for the **Advanced Databases (NoSQL)** course. The project implements a RESTful API using **Node.js** and **MongoDB** to manage users, products, and orders. The project also includes a simple frontend that allows users to view products, create orders, and manage their profiles.

### Features:
- User authentication with JWT.
- Product catalog including guitars, pianos, and accessories.
- Order management for users and admins.
- Admin-only statistics endpoint to view total revenue and number of orders.
- CRUD operations for products, orders, and users.

## Project Setup

### Prerequisites:
- **Node.js**: Install the latest version from [nodejs.org](https://nodejs.org/).
- **MongoDB**: Install MongoDB locally or use [MongoDB Atlas](https://www.mongodb.com/cloud/atlas) for cloud-based database.

### Setup
1. Clone the repository:
   ```bash
   git clone https://github.com/your-username/music-store.git
   cd music-store
   ```

2. Install dependencies:
   ```bash
   npm install
   ```

3. Create `.env` file
In the root directory, create a `.env` file and add the following:

```bash
JWT_SECRET=your-secret-key
MONGO_URI=mongodb://localhost:27017/music_store
PORT=3000
```

4. Start the backend server:
   ```bash
   npm run dev
   ```

5. Frontend is available by opening `index.html` in a browser.

## API Endpoints

The backend exposes several RESTful API endpoints:

### Authentication
- **POST /auth/login**: Login to the system and receive a JWT token.
- **POST /auth/register**: Register a new user.

### Products
- **GET /products**: Retrieve a list of all products.
- **POST /products**: Add a new product (admin only).
- **PATCH /products/stock**: Update product stock (admin only).

### Orders
- **POST /orders**: Create a new order.
- **GET /orders/my**: Get the logged-in user's order history.

### Admin
- **GET /admin/stats/sales**: Retrieve sales statistics (admin only).

## Example Request and Response

### Login Request:
**POST /auth/login**

**Body:**
```json
{
  "email": "test1@mail.com",
  "password": "123456"
}
```

**Response:**
```json
{
  "token": "your-jwt-token"
}
```

### Create Order Request:
**POST /orders**

**Body:**
```json
{
  "items": [
    { "productId": "60d9c9b6b2f7c9d1a3bb4c59", "qty": 2 }
  ]
}
```

**Response:**
```json
{
  "userId": "60d9c9b6b2f7c9d1a3bb4c59",
  "items": [
    {
      "productId": "60d9c9b6b2f7c9d1a3bb4c59",
      "nameSnapshot": "Electric Guitar",
      "priceSnapshot": 500,
      "qty": 2
    }
  ],
  "total": 1000,
  "status": "pending",
  "createdAt": "2026-02-02T10:20:30.000Z"
}
```

## Database Schema

### Users Collection
```json
{
  "_id": ObjectId,
  "name": "John Doe",
  "email": "test1@mail.com",
  "passwordHash": "hashedPassword",
  "role": "user"
}
```

### Products Collection
```json
{
  "_id": ObjectId,
  "name": "Electric Guitar",
  "category": "guitar",
  "brand": "Fender",
  "price": 500,
  "stock": 10,
  "description": "An electric guitar for beginners.",
  "tags": ["electric", "beginner"],
  "ratingAvg": 4.5,
  "ratingCount": 25
}
```

### Orders Collection
```json
{
  "_id": ObjectId,
  "userId": ObjectId,
  "items": [
    {
      "productId": ObjectId,
      "nameSnapshot": "Electric Guitar",
      "priceSnapshot": 500,
      "qty": 2
    }
  ],
  "total": 1000,
  "status": "pending",
  "createdAt": "2026-02-02T10:20:30.000Z"
}
```

## Aggregation Example

### Sales Aggregation
**GET /admin/stats/sales**

**Response:**
```json
{
  "totalRevenue": 5000,
  "ordersCount": 150
}
```

This API endpoint calculates the total revenue and the number of orders placed by the users.

## Contribution

### Installation

1. Clone this repository using the following command:

```bash
git clone https://github.com/your-username/music-store.git
```

2. Install dependencies:
```bash
npm install
```

3. Create a `.env` file with the necessary environment variables as described in the setup section.

4. Run the application:
```bash
npm run dev
```


### Notes
1. You may also consider adding a **Swagger API documentation** for a more structured API description.
2. **Pagination and filtering** for products could be implemented for scalability.
3. Make sure your MongoDB setup is correct and properly connected.



### Additional Information
1. **MongoDB Aggregation** is used for generating statistics such as sales revenue and the number of orders.
2. **JWT Authentication** ensures that users are authorized to access the system, and **admin** routes are protected by roles.

1. **MongoDB Aggregation** is used for generating statistics such as sales revenue and the number of orders.
2. **JWT Authentication** ensures that users are authorized to access the system, and **admin** routes are protected by roles.
