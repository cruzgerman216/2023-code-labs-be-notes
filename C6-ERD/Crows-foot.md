# Crows Foot ERD

**Crow's Foot ERD**, also known as a entity-relationship diagram, is a graphical representation of entities and their relationships to each other. It is used to model the structure of a database.

### Terms

**Entities:** An entity is a real-world object or concept that is represented in the database, such as a customer or a product.

**Tables:** Each entity is represented by a table in the database, and the columns of the table represent the attributes of the entity.

**Relationships:** The relationships between entities are represented by lines connecting the tables.

**Cardinality:** The cardinality of a relationship represents the number of instances of one entity that can be related to one instance of another entity. It can be represented by the following symbols:

- One to one (1:1)
- One to many (1:N)
- Many to many (M:N)

For Example, a customer can have multiple orders, so the relationship between customer and order is represented as a one-to-many (1:N) relationship.

In a crow's foot ERD, the crow's foot notation is used to indicate the cardinality of a relationship. The lines coming out of the entities indicate the number of instances that can be related to one instance of the other entity.

**In depth on Cardinality:**

1. One-to-one (1:1) relationship: A customer has only one mailing address. The relationship is represented by a line connecting the customer and address entities, with a single crow's foot on the address side of the line.

2. One-to-many (1:N) relationship: A customer can have multiple orders. The relationship is represented by a line connecting the customer and order entities, with a single crow's foot on the customer side of the line and multiple crow's feet on the order side of the line.

3. Many-to-many (M:N) relationship: A product can be in multiple orders and an order can have multiple products. The relationship is represented by a line connecting the product and order entities, with multiple crow's feet on both sides of the line.

**Bonus Terms:**

4. Inheritance: A sub-class inherits attributes and relationships from its super-class. The relationship is represented by a line connecting the super-class and sub-class entities, with an arrowhead pointing from the super-class to the sub-class.

5. Weak entities: An entity that cannot exist without the existence of another entity. The relationship is represented by a double diamond shape on the relationship line and a dashed line pointing to the owner entity.

6. Associative entities: An entity that represents the relationship between two or more entities. The relationship is represented by a diamond shape on the relationship line.

## Demonstrate a Crows Foot ERD

**Entities:**

- Customer
  - Customer_ID
  - Name
  - Email
  - Password
  - shipping_address_ID
- Item
  - Item_ID
  - Title
  - Description
  - Price
- Order
  - Order_ID
  - Customer_ID
  - Item_ID
  - shipping_address_ID
- Shipping Address
  - shipping_address_ID
  - city
  - state
  - zip_code
  - street

**Relationships:**
Customer to Order: (1:N)
Customer to Shipping Address: (1:M)
Item to Order: (M:N)
Order to Address: (1:1)

## Exercises

## READ BEFORE STARTING

**Use a cloud based service or a local IDE**<br>

You can use the following

- [lucid charts](https://www.lucidchart.com/pages/)
- [https://app.diagrams.net/](https://app.diagrams.net/)
- VS Code with extension (Draw.io Integration)

**Create a GitHub Repository/commit frequently**<br>

## ER Diagrams

**Exercise 1.1: One to One relationship: Apartment Complex**
Create two ER tables with the following:

- Apartment
  - id
  - room_number
  - active
  - renter_id
- Renter
  - id
  - first_name
  - last_name
  - email
  - license_number

Develop a 1:1 relationship. For example, a Apartment can have one renter and a renter can have one apartment.

Use a spreadsheet like google spreadsheet to create examples of what the data may look like. Create 3 apartment records and 3 renter recorders.

---

**Repeat the same process for exercises 1.2 - 1.5**

- Each entity must have at least one attribute besides id, more is encouraged.

**Exercise 1.2: Aiport**
A "Person" entity is related to a "Passport" entity. Each person can have only one passport and each passport belongs to only one person.

**Exercise 1.3: Vehicles**
A "Car" entity is related to a "License Plate" entity. Each car can have only one license plate and each license plate belongs to only one car.

**Exercise 1.4: Medical**
A "Patient" entity is related to a "Medical Record" entity. Each patient can have only one medical record and each medical record belongs to only one patient.

**Exercise 1.5: Computer Warranty**
A "Computer" entity is related to a "Warranty" entity. Each computer can have only one warranty and each warranty belongs to only one computer.

---

**Repeat the following for exercises 1.6 - 1.10**

Develop a one to many relationship.

- add at least one attribute to every entity besides id.

Use a spreadsheet like google spreadsheet to create examples of what the data may look like. Create there records of each entity.

**Exercise 1.6: Library**

Design an ER diagram for a library system that models the relationship between books and authors. A book can have multiple authors, but an author can only write one book.

**Exercise 1.7: Rent**
A customer can rent multiple cars, but a car can only be rented by one customer at a time.

**Exercise 1.8: Reservations**
A room can have multiple reservations, but a reservation can only be for one room.

**Exercise 1.9: School**
A teacher can teach multiple classes, but a class can only be taught by one teacher.

**Exercise 1.10: Medical**
A patient can have multiple visits, but a visit can only be for one patient.

---

**Repeat the following for exercises 1.10 - 1.15**
Develop a many to many relationship.

- add at least one attribute to every entity besides id.

Use a spreadsheet like google spreadsheet to create examples of what the data may look like. Create there records of each entity.

**Exercise 1.11: Grade School**
A student can enroll in multiple courses, but a course can have multiple students.

**Exercise 1.12: Work**
An employee can work on multiple projects, but a project can have multiple employees.

**Exercise 1.13: Movies**
A movie can belong to multiple genres, but a genre can have multiple movies.

**Exercise 1.14: Menu**
A menu item can have multiple ingredients, but an ingredient can be used in multiple menu items.

**Exercise 1.15: Product**

product can belong to multiple categories, but a category can have multiple products.


## Project Planning 

![project planning](../assets/images/C6/project.webp)
It's time to create your own very data for an upcoming project. Your project must have the following 
- theme 
  - library system (books, renters, staff, ect)
  - Basic Social Media (users, posts, comments, ect)
  - School (staff, students, courses, ect)
- At least three entities
- a many to many relationship 
- a one to many relationship
