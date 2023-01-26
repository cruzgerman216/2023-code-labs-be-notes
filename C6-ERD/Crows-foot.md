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
