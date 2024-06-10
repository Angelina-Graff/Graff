# E-commerce Project

## Diagramme relationnel d'entités

### Entités et leurs propriétés

- **User**
  - id: int
  - username: string
  - password: string
  - email: string
  - created_at: datetime
  - updated_at: datetime

- **Customer**
  - id: int
  - user_id: int (FK)
  - first_name: string
  - last_name: string
  - phone: string
  - created_at: datetime
  - updated_at: datetime

- **CustomerAddress**
  - id: int
  - customer_id: int (FK)
  - address_line1: string
  - address_line2: string
  - city: string
  - state: string
  - postal_code: string
  - country: string
  - created_at: datetime
  - updated_at: datetime

- **Category**
  - id: int
  - name: string
  - description: string
  - created_at: datetime
  - updated_at: datetime

- **Product**
  - id: int
  - category_id: int (FK)
  - name: string
  - description: string
  - price: decimal
  - stock_quantity: int
  - created_at: datetime
  - updated_at: datetime

- **Review**
  - id: int
  - product_id: int (FK)
  - customer_id: int (FK)
  - rating: int
  - comment: text
  - created_at: datetime
  - updated_at: datetime

- **Order**
  - id: int
  - customer_id: int (FK)
  - order_date: datetime
  - status: string
  - total_amount: decimal
  - created_at: datetime
  - updated_at: datetime

- **OrderLine**
  - id: int
  - order_id: int (FK)
  - product_id: int (FK)
  - quantity: int
  - price: decimal
  - created_at: datetime
  - updated_at: datetime

- **Payment**
  - id: int
  - order_id: int (FK)
  - payment_date: datetime
  - amount: decimal
  - payment_method: string
  - status: string
  - created_at: datetime
  - updated_at: datetime

### Relations entre les entités

- Un **User** peut avoir un **Customer** (relation 1:1)
- Un **Customer** peut avoir plusieurs **CustomerAddresses** (relation 1:N)
- Un **Category** peut avoir plusieurs **Products** (relation 1:N)
- Un **Product** peut avoir plusieurs **Reviews** (relation 1:N)
- Un **Customer** peut passer plusieurs **Orders** (relation 1:N)
- Un **Order** peut avoir plusieurs **OrderLines** (relation 1:N)
- Un **OrderLine** est lié à un **Product** (relation N:1)
- Un **Order** peut avoir plusieurs **Payments** (relation 1:N)

### Diagramme relationnel d'entités (ERD) en Mermaid

```mermaid
erDiagram
    USER {
        int id
        string username
        string password
        string email
        datetime created_at
        datetime updated_at
    }
    CUSTOMER {
        int id
        int user_id
        string first_name
        string last_name
        string phone
        datetime created_at
        datetime updated_at
    }
    CUSTOMERADDRESS {
        int id
        int customer_id
        string address_line1
        string address_line2
        string city
        string state
        string postal_code
        string country
        datetime created_at
        datetime updated_at
    }
    CATEGORY {
        int id
        string name
        string description
        datetime created_at
        datetime updated_at
    }
    PRODUCT {
        int id
        int category_id
        string name
        string description
        decimal price
        int stock_quantity
        datetime created_at
        datetime updated_at
    }
    REVIEW {
        int id
        int product_id
        int customer_id
        int rating
        text comment
        datetime created_at
        datetime updated_at
    }
    ORDER {
        int id
        int customer_id
        datetime order_date
        string status
        decimal total_amount
        datetime created_at
        datetime updated_at
    }
    ORDERLINE {
        int id
        int order_id
        int product_id
        int quantity
        decimal price
        datetime created_at
        datetime updated_at
    }
    PAYMENT {
        int id
        int order_id
        datetime payment_date
        decimal amount
        string payment_method
        string status
        datetime created_at
        datetime updated_at
    }
    USER ||--|{ CUSTOMER : has
    CUSTOMER ||--|{ CUSTOMERADDRESS : has
    CATEGORY ||--|{ PRODUCT : contains
    PRODUCT ||--|{ REVIEW : receives
    CUSTOMER ||--|{ ORDER : places
    ORDER ||--|{ ORDERLINE : includes
    ORDERLINE ||--|{ PRODUCT : contains
    ORDER ||--|{ PAYMENT : processes
