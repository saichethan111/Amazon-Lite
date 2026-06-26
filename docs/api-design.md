# API Design

## Scope

The MVP exposes REST APIs for product browsing, product administration, inventory administration, order placement, and order lookup.

Authentication, cart, payment, shipping, notifications, Kafka, Redis, and Kubernetes are out of scope for this release.

## Customer APIs

### List Products

`GET /api/products`

Query parameters:

- `search`
- `category`

Response includes:

List of
- product id
- name
- description
- category
- price
- available quantity

### Get Product Details

`GET /api/products/{productId}`

Response includes:

Product's
- product id
- name
- description
- category
- price
- available quantity

### Place Order

`POST /api/orders`

Request body:

```json
{
  "customerId": "customer-1",
  "items": [
    {
      "productId": 1,
      "quantity": 2
    }
  ]
}
```

Response includes:

- order id
- order status
- total amount
- order items

### View Order

`GET /api/orders/{orderId}`

Response includes:

- order id
- customer id
- status
- total amount
- order items
- created time

## Admin APIs

### Create Product

`POST /api/admin/products`

Creates a product.

### Update Product

`PUT /api/admin/products/{productId}`

Updates product details such as name, description, category, or price.

### Add Inventory

`POST /api/admin/products/{productId}/inventory`

Adds or adjusts inventory for a product.

## Search Behavior (Out of scope)

Product search should support partial matching by name and category.

If an exact product is not found, the API can return related products from the same category when possible. This should stay simple in the MVP and can later evolve into better search ranking.
