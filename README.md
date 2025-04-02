Shopping Cart Database Project

Project Overview : 
This project implements a Shopping Cart System using SQL queries. The database stores information about users, products, orders, and carts, enabling seamless shopping experiences by managing inventory, tracking orders, and handling payments.

Features : 
1. User Management: Register, login, and manage user profiles.
2. Product Catalog: Store product details, categories, and pricing.
3. Cart Operations: Add, remove, and update products in the cart.
4. Order Processing: Place and manage orders with payment tracking.
5. Inventory Management: Monitor stock levels and update inventory.
6. Admin Controls: Manage users, products, and orders.

Database Schema 
The system consists of multiple tables:

1. Users - Stores user information.

   CREATE TABLE Users (
    user_id INT PRIMARY KEY AUTO_INCREMENT,
    username VARCHAR(50) UNIQUE NOT NULL,
    password_hash VARCHAR(255) NOT NULL,
    email VARCHAR(100) UNIQUE NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

2. Products - Stores product details.

   CREATE TABLE Products (
    product_id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(100) NOT NULL,
    description TEXT,
    price DECIMAL(10,2) NOT NULL,
    stock INT NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

4. Cart - Manages shopping cart items.

   CREATE TABLE Cart (
    cart_id INT PRIMARY KEY AUTO_INCREMENT,
    user_id INT,
    product_id INT,
    quantity INT NOT NULL,
    FOREIGN KEY (user_id) REFERENCES Users(user_id),
    FOREIGN KEY (product_id) REFERENCES Products(product_id)
);

5. Orders - Stores placed orders.

   CREATE TABLE Orders (
    order_id INT PRIMARY KEY AUTO_INCREMENT,
    user_id INT,
    total_amount DECIMAL(10,2) NOT NULL,
    status ENUM('Pending', 'Completed', 'Cancelled') DEFAULT 'Pending',
    order_date TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (user_id) REFERENCES Users(user_id)
);

7. Order_Items - Stores products in each order.

    CREATE TABLE Order_Items (
    order_item_id INT PRIMARY KEY AUTO_INCREMENT,
    order_id INT,
    product_id INT,
    quantity INT NOT NULL,
    price DECIMAL(10,2) NOT NULL,
    FOREIGN KEY (order_id) REFERENCES Orders(order_id),
    FOREIGN KEY (product_id) REFERENCES Products(product_id)
);

SQL Queries

Here are some key queries for interacting with the database:

1. Register a New User

INSERT INTO Users (username, password_hash, email) VALUES ('user1', 'hashed_password', 'user1@example.com');

2. Add a Product to Cart

INSERT INTO Cart (user_id, product_id, quantity) VALUES (1, 2, 1);

3. View Cart Items

SELECT Products.name, Cart.quantity, Products.price
FROM Cart
JOIN Products ON Cart.product_id = Products.product_id
WHERE Cart.user_id = 1;

4. Place an Order

INSERT INTO Orders (user_id, total_amount, status) VALUES (1, 100.00, 'Pending');

