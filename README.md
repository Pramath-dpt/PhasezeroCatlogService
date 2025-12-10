PhaseZero Catalog Service

A Spring Boot application built using a 3-layer architecture (Controller → Service → Repository) to manage product catalog data.

 Technologies Used

Java 17

Spring Boot

Spring Web

In-Memory Repository (HashMap / ConcurrentHashMap)

Postman

 Project Architecture
src/main/java
└── com.org.phasezero_catlog_service
      ├── Product.java
      ├── PhasezeroCatlogServiceApplication.java
      │
      ├── controller
      │     └── ProductController.java
      │
      ├── service
      │     └── ProductService.java
      │
      └── Repository
            ├── ProductRepository.java
            └── InMemoryProductRepository.java

 Features

Add new product
Validate:
partNumber (required)
partName (required, stored lowercase)
category (required)
price must be ≥ 0
stock must be ≥ 0
Prevent duplicate partNumber
Search products by name
Filter by category
Sort by price (ascending)
Calculate total inventory value
Custom error messages:
"price is not acceptable"
"stock is not acceptable"
"Product with partNumber '...' already exists"

 API Endpoints: 
 1️ Add Product
POST http://localhost:8080/products
Body (JSON):

{
  "partNumber": "P-1001",
  "partName": "Hydraulic Filter",
  "category": "filter",
  "price": 500,
  "stock": 10
}

Possible Errors
{ "message": "price is not acceptable" }
{ "message": "stock is not acceptable" }
{ "message": "Product with partNumber 'P-1001' already exists" }

2️ Get All Products
GET http://localhost:8080/products

3️ Search by Name
GET http://localhost:8080/products/search?name=filter

4️ Filter by Category
GET http://localhost:8080/products/filter?category=filter

5️ Sort by Price
GET http://localhost:8080/products/sort/price

6️ Total Inventory Value
GET http://localhost:8080/products/inventory/value

In-Memory Repository

Products are stored in:
Map<String, Product> storage = new ConcurrentHashMap<>();


Key → partNumber

Value → Product

Auto-generated ID using AtomicLong

Data resets when the app restarts.

▶️ How to Run

Open project in Eclipse Spring Tools Suite

Run as: Spring Boot App

Test APIs using Postman