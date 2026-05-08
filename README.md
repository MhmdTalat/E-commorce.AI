# E-Commerce Database Schema

## Overview

This project contains the database schema design for a scalable e-commerce platform. The database is designed using relational database principles and supports complete e-commerce workflows including:

- User authentication and authorization
- Product catalog management
- Shopping cart functionality
- Order processing
- Payment tracking
- Product reviews and ratings
- Loyalty and rewards systems
- Vendor/store management
- Wishlist and favorites
- Inventory and product variants

The schema follows normalized relational database design practices using:

- Primary Keys (PK)
- Foreign Keys (FK)
- Junction Tables
- One-to-Many Relationships
- Many-to-Many Relationships

View the database schema diagram: [Mermaid Diagram](https://mermaid.ai/d/f91bb88c-02a9-435d-92e9-419156d64200)

---

# Database Architecture

The database is divided into several core domains:

| Domain             | Responsibility                         |
| ------------------ | -------------------------------------- |
| User Management    | Authentication, profiles, roles        |
| Product Catalog    | Products, categories, brands, variants |
| Shopping System    | Cart, checkout, order items            |
| Transaction System | Payments and transactions              |
| Engagement System  | Reviews, favorites                     |
| Loyalty System     | Rewards and loyalty points             |

---

# Entity Descriptions

# USERS

## Purpose

Stores all registered users in the system.

## Main Responsibilities

- Authentication
- User profile management
- Order ownership
- Reviews and ratings
- Payment ownership

## Important Columns

| Column       | Description           |
| ------------ | --------------------- |
| Id           | Primary key           |
| FullName     | User full name        |
| Email        | Login email           |
| PasswordHash | Encrypted password    |
| RoleId       | Linked role           |
| CreatedAt    | Account creation date |

## Relationships

| Relationship        | Type        |
| ------------------- | ----------- |
| User → Role         | Many-to-One |
| User → Orders       | One-to-Many |
| User → Reviews      | One-to-Many |
| User → Transactions | One-to-Many |
| User → Favorites    | One-to-Many |
| User → Addresses    | One-to-Many |

---

# ROLES

## Purpose

Defines authorization and permission levels.

## Example Roles

- Admin
- Customer
- Vendor
- Moderator

## Important Columns

| Column | Description |
| ------ | ----------- |
| Id     | Primary key |
| Name   | Role name   |

## Relationships

| Relationship | Type        |
| ------------ | ----------- |
| Role → Users | One-to-Many |

---

# PRODUCTS

## Purpose

Stores all products available in the platform.

## Important Columns

| Column      | Description        |
| ----------- | ------------------ |
| Id          | Product identifier |
| CategoryId  | Linked category    |
| VendorId    | Linked vendor      |
| Name        | Product name       |
| Description | Product details    |
| Price       | Product price      |
| Discount    | Discount value     |
| MainImage   | Product image      |
| Stock       | Available quantity |

## Relationships

| Relationship         | Type        |
| -------------------- | ----------- |
| Product → Category   | Many-to-One |
| Product → Vendor     | Many-to-One |
| Product → Reviews    | One-to-Many |
| Product → CartItems  | One-to-Many |
| Product → OrderItems | One-to-Many |
| Product → Sizes      | One-to-Many |
| Product → Variants   | One-to-Many |

---

# CATEGORIES

## Purpose

Organizes products into logical groups.

## Important Columns

| Column | Description         |
| ------ | ------------------- |
| Id     | Category identifier |
| Name   | Category name       |

## Relationships

| Relationship        | Type        |
| ------------------- | ----------- |
| Category → Products | One-to-Many |

---

# VENDORS

## Purpose

Stores supplier/vendor information.

## Important Columns

| Column      | Description       |
| ----------- | ----------------- |
| Id          | Vendor identifier |
| UserId      | Associated user   |
| Name        | Vendor name       |
| Email       | Vendor email      |
| Phone       | Vendor phone      |
| Description | Vendor details    |

## Relationships

| Relationship      | Type        |
| ----------------- | ----------- |
| Vendor → Products | One-to-Many |

---

# PRODUCT_VARIANTS

## Purpose

Handles product variations such as:

- Color
- Material
- Style

## Important Columns

| Column      | Description        |
| ----------- | ------------------ |
| Id          | Variant identifier |
| ProductId   | Parent product     |
| VariantType | Variation type     |
| Value       | Variant value      |
| Stock       | Variant stock      |

---

# PRODUCT_SIZES

## Purpose

Stores product sizes and inventory.

## Important Columns

| Column    | Description        |
| --------- | ------------------ |
| Id        | Size identifier    |
| ProductId | Linked product     |
| SizeName  | Size label         |
| Stock     | Available quantity |

---

# PRODUCT_BRANDS

## Purpose

Stores product brand information.

## Important Columns

| Column | Description      |
| ------ | ---------------- |
| Id     | Brand identifier |
| Name   | Brand name       |

---

# CART_ITEMS

## Purpose

Stores items added to user shopping carts.

## Important Columns

| Column    | Description          |
| --------- | -------------------- |
| Id        | Cart item identifier |
| CartId    | Parent cart          |
| ProductId | Selected product     |
| SizeId    | Selected size        |
| Quantity  | Product quantity     |

## Relationships

| Relationship        | Type        |
| ------------------- | ----------- |
| Cart → CartItems    | One-to-Many |
| Product → CartItems | One-to-Many |

---

# ORDERS

## Purpose

Represents completed purchases.

## Important Columns

| Column        | Description      |
| ------------- | ---------------- |
| Id            | Order identifier |
| UserId        | Purchasing user  |
| TotalPrice    | Order total      |
| Status        | Order status     |
| PaymentMethod | Payment type     |
| CreatedAt     | Order date       |

## Relationships

| Relationship       | Type        |
| ------------------ | ----------- |
| User → Orders      | One-to-Many |
| Order → OrderItems | One-to-Many |

## Order Status Examples

- Pending
- Paid
- Shipped
- Delivered
- Cancelled
- Refunded

---

# ORDER_ITEMS

## Purpose

Stores products inside orders.

## Important Columns

| Column    | Description           |
| --------- | --------------------- |
| Id        | Order item identifier |
| OrderId   | Parent order          |
| ProductId | Ordered product       |
| Quantity  | Purchased quantity    |
| Price     | Purchase price        |

## Relationships

| Relationship         | Type        |
| -------------------- | ----------- |
| Order → OrderItems   | One-to-Many |
| Product → OrderItems | One-to-Many |

---

# REVIEWS

## Purpose

Allows customers to review and rate products.

## Important Columns

| Column    | Description       |
| --------- | ----------------- |
| Id        | Review identifier |
| UserId    | Reviewer          |
| ProductId | Reviewed product  |
| Rating    | Product rating    |
| Comment   | Review text       |
| CreatedAt | Review date       |

## Relationships

| Relationship      | Type        |
| ----------------- | ----------- |
| User → Reviews    | One-to-Many |
| Product → Reviews | One-to-Many |

---

# USER_FAVORITES

## Purpose

Stores wishlist/favorite products for users.

## Relationships

| Relationship   | Type         |
| -------------- | ------------ |
| User ↔ Product | Many-to-Many |

---

# USER_ADDRESSES

## Purpose

Stores shipping and billing addresses.

## Important Columns

| Column     | Description        |
| ---------- | ------------------ |
| Id         | Address identifier |
| UserId     | Owner user         |
| Country    | Country            |
| City       | City               |
| Street     | Street address     |
| PostalCode | ZIP/postal code    |

---

# USER_TRANSACTIONS

## Purpose

Tracks financial operations and payments.

## Important Columns

| Column         | Description            |
| -------------- | ---------------------- |
| Id             | Transaction identifier |
| UserId         | Associated user        |
| Amount         | Transaction amount     |
| Type           | Transaction type       |
| TransactionRef | External reference     |

---

# LOYALTY_ACCOUNTS

## Purpose

Stores loyalty points and membership levels.

## Important Columns

| Column | Description                |
| ------ | -------------------------- |
| Id     | Loyalty account identifier |
| UserId | Account owner              |
| Points | Current balance            |
| Level  | Loyalty level              |

---

# Relationship Summary

## One-to-Many Relationships

| Parent   | Child        |
| -------- | ------------ |
| Role     | Users        |
| User     | Orders       |
| User     | Reviews      |
| User     | Transactions |
| User     | Addresses    |
| Vendor   | Products     |
| Category | Products     |
| Product  | Reviews      |
| Product  | Sizes        |
| Product  | Variants     |
| Order    | OrderItems   |

---

## Many-to-Many Relationships

| Entity A | Entity B  | Junction Table |
| -------- | --------- | -------------- |
| Users    | Favorites | User_Favorites |
| Products | Tags      | Product_Tags   |
| Orders   | Products  | Order_Items    |

---

# Purchase Workflow

1. User registers/login
2. User browses products
3. User adds products to cart
4. User selects size/variant
5. Checkout creates order
6. Order items are generated
7. Payment transaction is recorded
8. Inventory updates occur
9. Loyalty points may be awarded
10. User submits reviews

---

# Database Design Strengths

## Normalization

The schema avoids duplication by separating:

- Orders from order items
- Products from variants
- Users from addresses
- Products from categories

## Scalability

Supports:

- Marketplace architecture
- Multi-vendor systems
- Recommendation systems
- Loyalty programs
- Analytics and reporting

## Maintainability

Uses:

- Consistent PK/FK structure
- Clear relationships
- Modular entity design

---

# Recommended Improvements

## Security

- Encrypt sensitive payment data
- Add password salting
- Add audit logging
- Use secure authentication tokens

## Performance

- Add indexes on foreign keys
- Optimize search queries
- Add caching layer

## Advanced Features

- Soft delete support
- Coupon management
- Shipment tracking
- Product image galleries
- Inventory reservation system

---

# Suggested Indexes

| Table       | Suggested Index      |
| ----------- | -------------------- |
| USERS       | Email                |
| PRODUCTS    | CategoryId, VendorId |
| ORDERS      | UserId, CreatedAt    |
| ORDER_ITEMS | OrderId, ProductId   |
| REVIEWS     | ProductId            |
| CART_ITEMS  | CartId               |

---

# Conclusion

This schema provides a strong relational foundation for a modern e-commerce platform. It supports:

- User management
- Product inventory
- Order processing
- Financial transactions
- Customer engagement
- Marketplace scalability
- Reporting and analytics

The design follows best practices in relational database modeling and can scale into a production-grade enterprise system with additional optimization and security enhancements.
