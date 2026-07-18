Tags: [[_Software_Engineering]]
#SoftwareEngineering 

# Introduction
Aggregate is a group of entities ([[Software Engineering - Architecture concepts - Entity|link]])/value objects ([[Software Engineering - Architecture concepts - Value object|link]]) treated as one consistency boundary.

When we want to modify aggregate's entities, we do this by interacting with the aggregate which enforces some rules, instead of modifying an entity directly.
# The main ideas
- An aggregate has one Aggregate Root.
- External code can only directly access the root 
	- We can't modify entities that belong to the aggregate
	- The root enforces business rules and invariants
	- So when we want to modify an aggregate's entity, we do this by interacting with the root which enforces some rules to make sure that we don't do something wrong
- Usually, one database transaction should modify only one aggregate.
# Example
For example, consider an e-commerce system.

Business rules:
- An order must have at least one item before being confirmed.
- The total price must equal the sum of items.
- An item quantity cannot be negative.
- After an order is shipped, items cannot be modified.

`Order` is a good aggregate root because these rules involve multiple objects:
```
Order (aggregate root)
 ├── OrderItem
 ├── OrderStatus
```

```python
from dataclasses import dataclass
from enum import Enum


class OrderStatus(Enum):
    DRAFT = "draft"
    CONFIRMED = "confirmed"
    SHIPPED = "shipped"


@dataclass(frozen=True)
class ProductId:
    value: str


class OrderItem:
    def __init__(self, product_id: ProductId,
                 quantity: int,
                 price_per_item: float):

        if quantity <= 0:
            raise ValueError("Quantity must be positive")

        self.product_id = product_id
        self.quantity = quantity
        self.price_per_item = price_per_item

    @property
    def total_price(self):
        return self.quantity * self.price_per_item


class Order:
    def __init__(self, order_id: str):
        self.order_id = order_id
        self._items: list[OrderItem] = []
        self.status = OrderStatus.DRAFT

    @property
    def items(self):
        # Return read-only copy (we can't add new items into it)
        return tuple(self._items)

    @property
    def total_price(self):
        return sum(i.total_price for i in self._items)

    def add_item(
        ...
    ):
        # add item to self._items
        ...
        
    def update_item_quantity(...)
	    # Change quantity of a specific item
	    ...

    def confirm(self):
        # Change status of an order to confirmed
        ...
        self.status = OrderStatus.CONFIRMED

    def ship(self):
        # Change status of an order to shipped
        ...
        self.status = OrderStatus.SHIPPED
```

Usage:
```python
order = Order("order-1")

order.add_item(ProductId("laptop"), 1, 1000)
order.add_item(ProductId("mouse"), 2, 50)

print(order.total_price)  # 1100

order.confirm()
order.ship()
```

Notice that external code cannot do:
```python
# can't do this because order.items is a tuple (read-only)
order.items.append(...)
```

or
```python
item.quantity = -10
```

All modifications need to go through `Order`, which enforces the business rules. For example, we modify `OrderItem` using functions from `Order`, e.g. `add_item`, `update_item_quantity`, not by interacting with `OrderItem` directly.
# Aggregate Root
The main entity controlling access to an aggregate. When we want to modify aggregate's entities, we do this through the root.