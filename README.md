/* ---------------
bigata.sql
This script creates a database with fair amount of dataL 
--------------- */
-- Create the database if it does not already exist
CREATE DATABASE IF NOT EXISTS bigdata;

-- Set database to be the current one in use
USE bigdata;

-- Remove/Drop tables of the database if they exist already -Get the Sequence right - many side first
DROP TABLE IF EXISTS orderitems;
DROP TABLE IF EXISTS productscategories;
DROP TABLE IF EXISTS Reviews;
DROP TABLE IF EXISTS Products;
DROP TABLE IF EXISTS categories;
DROP TABLE IF EXISTS Orders;
DROP TABLE IF EXISTS Customers;

-- Create tables of the database -Get the Sequence right - one side first
CREATE TABLE Customers (
  CustomerID INT PRIMARY KEY, 
  CustName VARCHAR(50), 
  Email VARCHAR(30), 
  City VARCHAR(30)
  ); 
  
CREATE TABLE Orders (
    OrderID INT PRIMARY KEY,
    CustomerID INT,
    OrderDate DATE,
    FOREIGN KEY (CustomerID) REFERENCES Customers(CustomerID)
);

CREATE TABLE Products (
    ProductID INT PRIMARY KEY,
    ProdName VARCHAR(100),
    Price DECIMAL(10, 2)
);

CREATE TABLE OrderItems (
    OrderID INT,
    ProductID INT,
    Quantity INT,
    PRIMARY KEY (OrderID, ProductID),
    FOREIGN KEY (OrderID) REFERENCES Orders(OrderID),
    FOREIGN KEY (ProductID) REFERENCES Products(ProductID)
);

CREATE TABLE Categories (
    CategoryID INT PRIMARY KEY,
    catName VARCHAR(100)
);

CREATE TABLE ProductsCategories (
    ProductID INT,
    CategoryID INT,
    PRIMARY KEY (ProductID, CategoryID),
    FOREIGN KEY (ProductID) REFERENCES Products(ProductID),
    FOREIGN KEY (CategoryID) REFERENCES Categories(CategoryID)
);

CREATE TABLE Reviews (
    ReviewID INT PRIMARY KEY,
    ProductID INT,
    CustomerID INT,
    Rating INT,
    Comment TEXT,
    FOREIGN KEY (ProductID) REFERENCES Products(ProductID),
    FOREIGN KEY (CustomerID) REFERENCES Customers(CustomerID)
);

-- Insert data into tables
INSERT INTO Customers (CustomerID, custName, Email, City) VALUES
(1, 'John Doe', 'john@example.com', 'New York'),(2, 'Jane Smith', 'jane@example.com', 'Los Angeles'),(3, 'Michael Johnson', 'michael@example.com', 'Chicago'),
(4, 'Emily Davis', 'emily@example.com', 'Houston'),(5, 'Sophia Brown', 'sophia@example.com', 'Phoenix'),(6, 'William Wilson', 'william@example.com', 'Philadelphia'),
(7, 'Olivia Lee', 'olivia@example.com', 'San Antonio'),(8, 'Daniel Martinez', 'daniel@example.com', 'San Diego'),(9, 'Ava Taylor', 'ava@example.com', 'Dallas'),
(10, 'Ethan Anderson', 'ethan@example.com', 'San Jose');

INSERT INTO Orders (OrderID, CustomerID, OrderDate) VALUES
(1, 1, '2024-04-01'),(2, 2, '2024-04-02'),(3, 3, '2024-04-03'),(4, 4, '2024-04-04'),(5, 5, '2024-04-05'),(6, 6, '2024-04-06'),
(7, 7, '2024-04-07'),(8, 8, '2024-04-08'),(9, 9, '2024-04-09'),(10, 10, '2024-04-10'),(11, 1, '2024-04-11'),(12, 2, '2024-04-12'),
(13, 3, '2024-04-13'),(14, 4, '2024-04-14'),(15, 5, '2024-04-15'),(16, 6, '2024-04-16'),(17, 7, '2024-04-17'),(18, 8, '2024-04-18'),
(19, 9, '2024-04-19'),(20, 10, '2024-04-20'),(21, 1, '2024-04-21'),(22, 2, '2024-04-22'),(23, 3, '2024-04-23'),(24, 4, '2024-04-24'),
(25, 5, '2024-04-25');

INSERT INTO Products (ProductID, prodName, Price) VALUES
(1, 'Laptop', 1000.00),(2, 'Smartphone', 700.00),(3, 'Tablet', 500.00),(4, 'Headphones', 100.00),(5, 'Keyboard', 50.00),(6, 'Mouse', 30.00),
(7, 'Monitor', 300.00),(8, 'Printer', 200.00),(9, 'Desk', 150.00),(10, 'Chair', 80.00),(11, 'Backpack', 60.00),(12, 'Watch', 400.00),
(13, 'Sunglasses', 120.00),(14, 'Camera', 600.00),(15, 'Speakers', 180.00);

INSERT INTO OrderItems (OrderID, ProductID, Quantity) VALUES
(1, 1, 2),(1, 2, 1),(1, 3, 3),(2, 2, 3),(2, 3, 1),(2, 4, 2),(3, 1, 1),(3, 5, 2),(3, 6, 1),(4, 4, 1),
(4, 7, 2),(4, 8, 1),(5, 9, 1),(5, 10, 4),(5, 11, 2),(6, 1, 3),(6, 5, 2),(6, 6, 2),(7, 2, 1),(7, 7, 1),
(7, 8, 3),(8, 3, 4),(8, 9, 1),(8, 10, 2),(9, 4, 2),(9, 11, 1),(9, 12, 1),(10, 1, 1),(10, 2, 2),(10, 3, 1),
(11, 4, 3),(11, 5, 1),(11, 6, 2),(12, 7, 1),(12, 8, 1),(12, 9, 2),(13, 10, 3),(13, 11, 2),(13, 12, 1),
(14, 1, 2),(14, 2, 1),(14, 3, 3),(15, 4, 1),(15, 5, 2),(15, 6, 1),(16, 7, 3),(16, 8, 1),(16, 9, 2),
(17, 10, 1),(17, 11, 4),(17, 12, 2),(18, 1, 3),(18, 2, 2),(18, 3, 1),(19, 4, 2),(19, 5, 1),(19, 6, 1),
(20, 7, 1),(20, 8, 2),(20, 9, 3),(21, 10, 1),(21, 11, 1),(21, 12, 2),(22, 1, 2),(22, 2, 1),(22, 3, 3),
(23, 4, 3),(23, 5, 1),(23, 6, 2),(24, 7, 1),(24, 8, 1),(24, 9, 2),(25, 10, 3),(25, 11, 2),(25, 12, 1);

INSERT INTO Reviews (ReviewID, ProductID, CustomerID, Rating, Comment) VALUES
(1, 1, 1, 5, 'Great laptop, fast delivery!'),(2, 2, 2, 4, 'Good smartphone, but battery life could be better.'),
(3, 3, 3, 3, 'Average tablet, nothing special.'),(4, 4, 4, 4, 'Excellent headphones, very comfortable!'),
(5, 5, 5, 5, 'Perfect keyboard for gaming, highly recommended.'),(6, 6, 6, 3, 'Decent mouse, but scroll wheel feels cheap.'),
(7, 7, 7, 5, 'Fantastic monitor, amazing color accuracy!'),(8, 8, 8, 4, 'Solid printer, easy to set up and use.'),
(9, 9, 9, 3, 'Desk is sturdy, but assembly instructions were unclear.'),(10, 10, 10, 5, 'Comfortable chair, great for long gaming sessions.'),
(11, 11, 1, 4, 'Spacious backpack, lots of pockets.'),(12, 12, 2, 5, 'Stylish watch, keeps perfect time.'),
(13, 1, 3, 5, 'Love this laptop! It exceeded my expectations.'),(14, 2, 4, 4, 'Solid smartphone with a great camera.'),
(15, 3, 5, 3, 'Tablet is okay, but battery life is disappointing.');

INSERT INTO Categories (CategoryID, catName) VALUES
(1, 'Electronics'),(2, 'Clothing'),(3, 'Home Appliances'),(4, 'Books'),(5, 'Furniture'),(6, 'Sports Equipment'),
(7, 'Beauty Products'),(8, 'Toys'),(9, 'Jewelry'),(10, 'Automotive'),(11, 'Health & Wellness'),(12, 'Pet Supplies'),
(13, 'Outdoor Gear'),(14, 'Kitchenware'),(15, 'Tools');

INSERT INTO ProductsCategories (ProductID, CategoryID) VALUES
(1,1),(2,1),(3,1),(4,1),(4,6),(5,1),(6,1),(7,1),(8,1),(8,3),(9,5),(10,5),(11,6),
(11,13),(12,6),(12,9),(13,13),(13,11),(14,1),(14,13),(15,1);
