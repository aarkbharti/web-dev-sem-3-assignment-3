# Inventory and Data Management System

Lab Assignment 3 - Web Dev III (Node.js, Express, MongoDB, Mongoose)

REST API to manage products of a store. You can add, view, update and delete products, update stock (restock / sale), filter, sort and paginate products, and get reports using aggregation.

## Run
```
npm install
npm run seed     (adds sample products)
npm run dev
```
Create a `.env` file (see `.env.example`):
```
MONGO_URI=mongodb://127.0.0.1:27017/inventoryDB
PORT=5050
```
Server runs at http://localhost:5050

## Endpoints
| Method | Route | Description |
|---|---|---|
| POST | /api/products | Add a product |
| GET | /api/products | Get all products (filter, sort, pagination) |
| GET | /api/products/:id | Get one product |
| PUT | /api/products/:id | Update product |
| PATCH | /api/products/:id/stock | Restock or sale `{ "change": 20 }` / `{ "change": -5 }` |
| DELETE | /api/products/:id | Delete product |
| GET | /api/products/low-stock | Products with low quantity (`?threshold=10`) |
| GET | /api/products/summary | Category wise summary (aggregation) |

### Query params for GET /api/products
- `category` - e.g. `?category=Electronics`
- `search` - search by name, e.g. `?search=chair`
- `minPrice`, `maxPrice` - e.g. `?minPrice=500&maxPrice=3000`
- `sort` - e.g. `?sort=price` or `?sort=-price`
- `page`, `limit` - e.g. `?page=2&limit=5`

## Folder Structure
- config/db.js - database connection
- model/product.model.js - product schema with validation
- controller/product.controller.js - all the logic
- routes/product.routes.js - routes
- middleware/validate.middleware.js - id and stock validation
- middleware/error.middleware.js - 404 and error handler
- seed.js - sample data
- server.js - main file

## Postman Screenshots

### 1. Create Product
`POST /api/products`

![Create Product](screenshots/1.png)

### 2. Get All Products
`GET /api/products`

![Get All Products](screenshots/2.png)

### 3. Get Product by ID
`GET /api/products/:id`

![Get Product by ID](screenshots/3.png)

### 4. Update Product
`PUT /api/products/:id`

![Update Product](screenshots/4.png)

### 5. Delete Product
`DELETE /api/products/:id`

![Delete Product](screenshots/5.png)

### 6. Filter by Category + Sort by Price
`GET /api/products?category=Electronics&sort=-price`

![Filter by Category + Sort by Price](screenshots/6.png)

### 7. Price Range
`GET /api/products?minPrice=500&maxPrice=3000&sort=price`

![Price Range](screenshots/7.png)

### 8. Search
`GET /api/products?search=chair`

![Search](screenshots/8.png)

### 9. Pagination
`GET /api/products?page=2&limit=5`

![Pagination](screenshots/9.png)

### 10. Restock (+20)
`PATCH /api/products/:id/stock`

![Restock (+20)](screenshots/10.png)

### 11. Sale (-15)
`PATCH /api/products/:id/stock`

![Sale (-15)](screenshots/11.png)

### 12. Not Enough Stock (error)
`PATCH /api/products/:id/stock`

![Not Enough Stock (error)](screenshots/12.png)

### 13. Low Stock Report
`GET /api/products/low-stock`

![Low Stock Report](screenshots/13.png)

### 14. Category Summary (aggregation)
`GET /api/products/summary`

![Category Summary (aggregation)](screenshots/14.png)

### 15. Validation Error
`POST /api/products`

![Validation Error](screenshots/15.png)

### 16. Duplicate SKU
`POST /api/products`

![Duplicate SKU](screenshots/16.png)

### 17. Invalid ID
`GET /api/products/123`

![Invalid ID](screenshots/17.png)

### 18. Product Not Found
`GET /api/products/64b000000000000000000000`

![Product Not Found](screenshots/18.png)
