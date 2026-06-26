# Data Model

This document will evolve into the PostgreSQL database design for the modular monolith.

## Tables

### products

Stores products available for browsing and ordering.

Candidate columns:

- id
- name
- description
- category
- price
- created_at
- updated_at

### inventory

Stores available stock for each product.

Candidate columns:

- id
- product_id
- available_quantity
- created_at
- updated_at

### orders

Stores customer orders.

Candidate columns:

- id
- customer_id
- status
- total_amount
- created_at
- updated_at

### order_items

Stores the products purchased within an order.

Candidate columns:

- id
- order_id
- product_id
- quantity
- unit_price
- line_total

## Design Questions To Review

- Should product price use `numeric(12,2)`?
- Should inventory be one-to-one with product in the MVP?
- Which order statuses are needed for the first release?
- Which indexes are needed for product browsing and order lookup?
- Which locking strategy should order placement use to prevent overselling?
