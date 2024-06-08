# Assignment 1: Design a Logical Model

## Question 1
Create a logical model for a small bookstore. 📚

At the minimum it should have employee, order, sales, customer, and book entities (tables). Determine sensible column and table design based on what you know about these concepts. Keep it simple, but work out sensible relationships to keep tables reasonably sized. Include a date table. There are several tools online you can use, I'd recommend [_Draw.io_](https://www.drawio.com/) or [_LucidChart_](https://www.lucidchart.com/pages/).

## Establishing Relationships
## • Employee can have multiple Orders (1-to-Many).
## • Customer can have multiple Orders (1-to-Many).
## • Order can have multiple Sales (1-to-Many).
## • Sales is associated with Books (Many-to-1).
## • OrderDate is associated with the Date table (Many-to-1)
+-----------------+          +-----------------+          +----------------+
|    Employee     |          |      Order      |          |      Sales     |
|-----------------|          |-----------------|          |----------------|
| EmployeeID (PK) | 1      M | OrderID (PK)    | 1      M | SalesID (PK)   |
| FirstName       |----------| CustomerID (FK) |----------| OrderID (FK)   |
| LastName        |          | EmployeeID (FK) |          | BookID (FK)    |
| Position        |          | OrderDate       |          | Quantity       |
| HireDate        |          | DateID (FK)     |          | SalePrice      |
+-----------------+          +-----------------+          +----------------+
        |                           |                           |
        |                           |                           |
        |                           |                           |
        |                           |                           |
        |                           |                           |
        |                           |                           |
        |                           |                           |
+-----------------+                 |                 +----------------+
|    Customer     |                 |                 |      Book      |
|-----------------|                 |                 |----------------|
| CustomerID (PK) | 1              M|                 | BookID (PK)    |
| FirstName       |-----------------|                 | Title          |
| LastName        |                 |                 | Author         |
| Email           |                 |                 | ISBN           |
| PhoneNumber     |                 |                 | Price          |
+-----------------+                 |                 +----------------+
                                    |
                                    |
                                    |
                                    |
                                    |
                                    |
                                    |
                              +-----------------+
                              |      Date       |
                              |-----------------|
                              | DateID (PK)     |
                              | Date            |
                              | Day             |
                              | Month           |
                              | Year            |
                              +-----------------+




## Question 2
We want to create employee shifts, splitting up the day into morning and evening. Add this to the ERD.
##
+-----------------+          +-----------------+          +----------------+
|    Employee     |          |      Order      |          |      Sales     |
|-----------------|          |-----------------|          |----------------|
| EmployeeID (PK) | 1      M | OrderID (PK)    | 1      M | SalesID (PK)   |
| FirstName       |----------| CustomerID (FK) |----------| OrderID (FK)   |
| LastName        |          | EmployeeID (FK) |          | BookID (FK)    |
| Position        |          | OrderDate       |          | Quantity       |
| HireDate        |          | DateID (FK)     |          | SalePrice      |
+-----------------+          +-----------------+          +----------------+
        |                           |                           |
        |                           |                           |
        |                           |                           |
        |                           |                           |
        |                           |                           |
        |                           |                           |
        |                           |                           |
+-----------------+                 |                 +----------------+
|    Customer     |                 |                 |      Book      |
|-----------------|                 |                 |----------------|
| CustomerID (PK) | 1              M|                 | BookID (PK)    |
| FirstName       |-----------------|                 | Title          |
| LastName        |                 |                 | Author         |
| Email           |                 |                 | ISBN           |
| PhoneNumber     |                 |                 | Price          |
+-----------------+                 |                 +----------------+
                                    |
                                    |
                                    |
                                    |
                                    |
                                    |
                                    |
                              +-----------------+
                              |      Date       |
                              |-----------------|
                              | DateID (PK)     |
                              | Date            |
                              | Day             |
                              | Month           |
                              | Year            |
                              +-----------------+
                                    |
                                    |
                                    |
+-----------------+                 |
| EmployeeShift   |                 |
|-----------------|                 |
| EmployeeShiftID (PK) |            |
| EmployeeID (FK) |------------------
| ShiftType       |
| StartTime       |
| EndTime         |
+-----------------+

## Question 3
The store wants to keep customer addresses. Propose two architectures for the CUSTOMER_ADDRESS table, one that will retain changes, and another that will overwrite. Which is type 1, which is type 2?

_Hint, search type 1 vs type 2 slowly changing dimensions._
+-----------------+          +-----------------+          +----------------+
|    Employee     |          |      Order      |          |      Sales     |
|-----------------|          |-----------------|          |----------------|
| EmployeeID (PK) | 1      M | OrderID (PK)    | 1      M | SalesID (PK)   |
| FirstName       |----------| CustomerID (FK) |----------| OrderID (FK)   |
| LastName        |          | EmployeeID (FK) |          | BookID (FK)    |
| Position        |          | OrderDate       |          | Quantity       |
| HireDate        |          | DateID (FK)     |          | SalePrice      |
+-----------------+          +-----------------+          +----------------+
        |                           |                           |
        |                           |                           |
        |                           |                           |
        |                           |                           |
        |                           |                           |
        |                           |                           |
        |                           |                           |
+-----------------+                 |                 +----------------+
|    Customer     |                 |                 |      Book      |
|-----------------|                 |                 |----------------|
| CustomerID (PK) | 1              M|                 | BookID (PK)    |
| FirstName       |-----------------|                 | Title          |
| LastName        |                 |                 | Author         |
| Email           |                 |                 | ISBN           |
| PhoneNumber     |                 |                 | Price          |
+-----------------+                 |                 +----------------+
        |                           |
        |                           |
        |                           |
        |                           |
        |                           |
        |                           |
        |                           |
+-------------------------+   +-------------------------+
| CustomerAddresses_Type1 |   | CustomerAddresses_Type2 |
|-------------------------|   |-------------------------|
| AddressID (PK)          |   | CustomerAddressID (PK)  |
| CustomerID (FK)         |   | CustomerID (FK)         |
| StreetAddress           |   | StreetAddress           |
| City                    |   | City                    |
| State                   |   | State                   |
| PostalCode              |   | PostalCode              |
+-------------------------+   | StartDate               |
                              | EndDate                 |
                              | IsCurrent               |
                              +-------------------------+
                                    |
                                    |
                                    |
                              +-----------------+
                              |      Date       |
                              |-----------------|
                              | DateID (PK)     |
                              | Date            |
                              | Day             |
                              | Month           |
                              | Year            |
                              +-----------------+
                                    |
                                    |
                                    |
+-----------------+                 |
| EmployeeShift   |                 |
|-----------------|                 |
| EmployeeShiftID (PK) |            |
| EmployeeID (FK) |------------------
| ShiftType       |
| StartTime       |
| EndTime         |
+-----------------+



Bonus: Are there privacy implications to this, why or why not?
## Type 1 and Type 2 Slowly Changing Dimensions

Type 1 SCD (Overwrite Changes)

Privacy Implications: This approach overwrites the existing address with new data, meaning historical addresses are not retained. This could be seen as better for privacy since old addresses are not stored, reducing the risk of historical data exposure.

Type 2 SCD (Retain Changes)
Privacy Implications: This approach retains historical addresses by creating new records for each change. While this provides a complete history and is useful for auditing and analysis, it also means that historical address data is stored. This could have privacy implications as it increases the amount of personal data stored and the potential risk if the database is compromised.

Proposed Architectures
Type 1 SCD: Overwrite Changes and is a better option from privacy prespective.


## Q3 CUSTOMER_ADDRESS 
--Type 1
## CREATE TABLE "CustomerAddresses_Type1" (
    "CustomerID" INTEGER NOT NULL,
    "AddressID" INTEGER NOT NULL PRIMARY KEY AUTOINCREMENT,
    "StreetAddress" TEXT NOT NULL,
    "City" TEXT NOT NULL,
    "State" TEXT NOT NULL,
    "PostalCode" TEXT NOT NULL,
    FOREIGN KEY ("CustomerID") REFERENCES "Customer" ("CustomerID")
);
## --  CUSTOMER_ADDRESS Type 2
CREATE TABLE "CustomerAddresses_Type2" (
    "CustomerAddressID" INTEGER NOT NULL PRIMARY KEY AUTOINCREMENT,
    "CustomerID" INTEGER NOT NULL,
    "StreetAddress" TEXT NOT NULL,
    "City" TEXT NOT NULL,
    "State" TEXT NOT NULL,
    "PostalCode" TEXT NOT NULL,
    "StartDate" TEXT NOT NULL,
    "EndDate" TEXT,
    "IsCurrent" BOOLEAN NOT NULL,
    FOREIGN KEY ("CustomerID") REFERENCES "Customer" ("CustomerID")
);


## Question 4
Review the AdventureWorks Schema [here](https://i.stack.imgur.com/LMu4W.gif)

Highlight at least two differences between it and your ERD. Would you change anything in yours?

## 1. the scope and relationship of the dataset is much larger and well organized. Contains a large number of tables (e.g., Person, SalesOrder, PurchaseOrder, Product, Employee) with complex interrelationships

2. Historical Data: Uses a detailed approach to track historical data. For example, the Person schema contains tables like PersonPhone, EmailAddress, and Address which link to the Person table, capturing a detailed history of each person's contact information.

Historical Data: Uses a detailed approach to track historical data. For example, the Person schema contains tables like PersonPhone, EmailAddress, and Address which link to the Person table, capturing a detailed history of each person's contact information.

# Criteria

[Assignment Rubric](./assignment_rubric.md)

# Submission Information

🚨 **Please review our [Assignment Submission Guide](https://github.com/UofT-DSI/onboarding/blob/main/onboarding_documents/submissions.md)** 🚨 for detailed instructions on how to format, branch, and submit your work. Following these guidelines is crucial for your submissions to be evaluated correctly.

### Submission Parameters:
* Submission Due Date: `June 1, 2024`
* The branch name for your repo should be: `model-design`
* What to submit for this assignment:
    * This markdown (design_a_logical_model.md) should be populated.
    * Two Entity-Relationship Diagrams (preferably in a pdf, jpeg, png format).
* What the pull request link should look like for this assignment: `https://github.com/<your_github_username>/sql/pull/<pr_id>`
    * Open a private window in your browser. Copy and paste the link to your pull request into the address bar. Make sure you can see your pull request properly. This helps the technical facilitator and learning support staff review your submission easily.

Checklist:
- [ ] Create a branch called `model-design`.
- [ ] Ensure that the repository is public.
- [ ] Review [the PR description guidelines](https://github.com/UofT-DSI/onboarding/blob/main/onboarding_documents/submissions.md#guidelines-for-pull-request-descriptions) and adhere to them.
- [ ] Verify that the link is accessible in a private browser window.

If you encounter any difficulties or have questions, please don't hesitate to reach out to our team via our Slack at `#cohort-3-help`. Our Technical Facilitators and Learning Support staff are here to help you navigate any challenges.
