# Domain Model

## Goal

Define the core business concepts for the Amazon-Lite MVP before implementation.

The first version is a modular monolith with one PostgreSQL database. Order placement must happen inside one database transaction so inventory reduction and order creation succeed or fail together.

## Modules

### Product

Represents an item that can be browsed and purchased.

Responsibilities:

- Store product identity, name, description, category, and price.
- Support customer browsing and product detail views.
- Support admin create and update operations.

Important rules:

- A product must have a name.
- A product must have a non-negative price.
- A product can exist even when inventory is zero.

### Inventory

Represents sellable stock for a product.

Responsibilities:

- Track available quantity for each product.
- Allow admins to add or adjust stock.
- Reserve or decrement stock during order placement.

Important rules:

- Inventory quantity cannot be negative.
- A customer cannot place an order for more quantity than is available.
  - Inventory changes during order placement must be protected by the database transaction.

### Order

Represents a customer's purchase request.

Responsibilities:

- Store the customer identifier supplied by the request.
- Store order status and total amount.
- Group one or more order items.
- Allow customers to view previously placed orders.

Important rules:

- An order must contain at least one order item.
- An order total is derived from its order items.
- Order creation and inventory reduction happen in the same transaction.

### OrderItem

Represents one product and quantity inside an order.

Responsibilities:

- Store product identity at the time of purchase.
- Store unit price at the time of purchase.
- Store requested quantity.

Important rules:

- Quantity must be greater than zero.
- Unit price should be copied from the product during checkout so historical orders do not change when product prices are updated later.

## Initial Entity Relationships

- Product has one Inventory record.
- Order has many OrderItems.
- OrderItem references one Product.

## MVP Transaction Boundary

Placing an order is the main consistency boundary.

Within one transaction:

1. Load the requested products and inventory rows.
2. Verify each requested quantity is available.
3. Decrease inventory quantities.
4. Create the order.
5. Create order items with copied unit prices.
6. Commit.

If any step fails, the transaction rolls back.

## Out Of Scope For MVP

- Authentication and authorization
- Cart
- Payment
- Shipping
- Notifications
- Kafka events
- Redis cache
- Kubernetes deployment
