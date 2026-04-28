# Mental Map

-- Customer Order Flow (Instagram / WhatsApp Store)

1. customer sends message →
   we store in customer table
   (full_name, phone, social_handle)

2. customer source tracked →
   customer_source =
   instagram / whatsapp / website / offline

3. business adds product →
   we store in products table
   (name, product_type, category)

4. then map sellable item to product_variants →
   store:
     - size
     - color
     - item_condition
     - price
     - stock_qty
     - sku

5. system checks stock →
   product_variants.stock_qty > 0

6. customer confirms purchase →
   create orders record

7. add ordered products →
   create order_items rows

8. reduce stock →
   product_variants.stock_qty - qty

9. order is now placed



# FAQs

## What products are being sold?

Use:
- products.name
- categories.name

## Are they thrifted items or handmade items?

Use:

products.product_type

Values:
- THRIFT
- HANDMADE

## How many pieces are available?

Use:

product_variants.stock_qty

## Which customer placed which order?

Use relationship:

customers.id = orders.customer_id

## What all items were part of one order?

Use:

orders.id = order_items.order_id

Then join:

order_items.variant_id → product_variants.id

## Was the order paid for?

Use:

payments.payment_status

Examples:
- PENDING
- PAID

## Has the order been shipped or delivered?

Use:

shipments.shipping_status

Examples:
- PENDING
- SHIPPED
- DELIVERED

## Can one customer place multiple orders?

Yes.

Relationship:

customers 1:N orders

## Can one order contain multiple products?

Yes.

Relationship:

orders 1:N order_items

## How do we store product-specific details like size, category, color, condition, or price?

Category:

products.category_id

Size / Color / Condition / Price:

product_variants.size
product_variants.color
product_variants.item_condition
product_variants.price
