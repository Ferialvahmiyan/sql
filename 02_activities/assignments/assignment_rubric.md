# Assignment 1: Design a Logical Model Rubric

## General
  - Criteria: Participant Name on Assignment
  - Criteria: Written content is no longer than two pages
  - Criteria: Assignment is free of noticeable typos
  - Criteria: Two ERDs exist

## Question 1

  - **Tables**
    - Employee: Relates to employees.
    - Order: Relates to order processing.
    - Sales: Relates to sales transactions.
    - Customer: Relates to customer information.
    - Book: Relates to inventory of books.

  - **Tables Exist**: All five tables need to exist.
  - **Column Relevance**: Each table must have named columns that relate to their respective entities and include columns relevant for bookstore administration. (**🚨EACH table will be graded as complete or incomplete🚨**)
  - **Relationships Indicated**: Clear relationships between the aforementioned tables must be established.
  - **Date Table**: 
    - Must exist with typical columns.
    - Must have correct relationships with other relevant tables indicated.
   
      
CREATE TABLE Employee (
    EmployeeID INT PRIMARY KEY,
    FirstName VARCHAR(50),
    LastName VARCHAR(50),
    Position VARCHAR(50),
    HireDate DATE,
    Salary DECIMAL(10, 2),
    PhoneNumber VARCHAR(15)
);

CREATE TABLE "Order" (
    OrderID INT PRIMARY KEY,
    CustomerID INT,
    OrderDate DATE,
    TotalAmount DECIMAL(10, 2),
    FOREIGN KEY (CustomerID) REFERENCES Customer(CustomerID)
);

CREATE TABLE Sales (
    SaleID INT PRIMARY KEY,
    OrderID INT,
    BookID INT,
    EmployeeID INT,
    SaleDate DATE,
    Quantity INT,
    SalePrice DECIMAL(10, 2),
    FOREIGN KEY (OrderID) REFERENCES "Order"(OrderID),
    FOREIGN KEY (BookID) REFERENCES Book(BookID),
    FOREIGN KEY (EmployeeID) REFERENCES Employee(EmployeeID)
);

CREATE TABLE Customer (
    CustomerID INT PRIMARY KEY,
    FirstName VARCHAR(50),
    LastName VARCHAR(50),
    Email VARCHAR(100),
    PhoneNumber VARCHAR(15),
    RegistrationDate DATE
);

CREATE TABLE Book (
    BookID INT PRIMARY KEY,
    Title VARCHAR(100),
    Author VARCHAR(100),
    Genre VARCHAR(50),
    Price DECIMAL(10, 2),
    StockQuantity INT,
    PublishedDate DATE
);

## Question 2
- Employee Shift Table exists, and we can discern morning/evening shifts from its design**

CREATE TABLE EmployeeShift (
    ShiftID INT PRIMARY KEY,
    EmployeeID INT,
    ShiftDate DATE,
    ShiftType VARCHAR(10),  -- 'Morning' or 'Evening'
    FOREIGN KEY (EmployeeID) REFERENCES Employee(EmployeeID)
);

## Question 3: 
- **Two distinct architectures are proposed**
- **One design for Customer Addresses table would retain changes**

This is a Type 2 Slowly Changing Dimension (SCD) model, where historical data is preserved. A new record is created for each address change, while previous addresses are maintained.

CREATE TABLE Customer_Address (
    AddressID INT PRIMARY KEY AUTO_INCREMENT,
    CustomerID INT,
    AddressLine1 VARCHAR(255),
    AddressLine2 VARCHAR(255),
    City VARCHAR(100),
    State VARCHAR(100),
    PostalCode VARCHAR(20),
    Country VARCHAR(100),
    StartDate DATE NOT NULL,
    EndDate DATE NULL,
    IsCurrent BOOLEAN NOT NULL,
    FOREIGN KEY (CustomerID) REFERENCES Customer(CustomerID)
);
  
- **One design for Customer Addresses table would overwrite changes**

This is a Type 1 Slowly Changing Dimension (SCD) model where each customer has one current address, and new address information overwrites the existing data.

CREATE TABLE Customer_Address (
    CustomerID INT PRIMARY KEY,
    AddressLine1 VARCHAR(255),
    AddressLine2 VARCHAR(255),
    City VARCHAR(100),
    State VARCHAR(100),
    PostalCode VARCHAR(20),
    Country VARCHAR(100),
    LastUpdatedDate DATE,
    FOREIGN KEY (CustomerID) REFERENCES Customer(CustomerID)
);

- **Each architecture is properly labelled as either Type 1 or Type 2 SCD**
    - Both Correct (Complete)
    - One Wrong (Incomplete)
    - Both Wrong (Incomplete)

## Question 4: 
- **AdventureWorks ERD has been examined**
- **Two interesting differences between participant ERDs and AdventureWorks ERDs highlighted**
- **Student reflection on differences between the ERDs**

## Criteria

|Criteria|Complete|Incomplete|
|--------|----|----|
|Question 1 Requirements|All requirements are met.|At least one requirement is not met.|
|Question 2 Requirements|All requirements are met.|At least one requirement is not met.|
|Question 3 Requirements|All requirements are met.|At least one requirement is not met.|
|Question 4 Requirements|All requirements are met.|At least one requirement is not met.|
