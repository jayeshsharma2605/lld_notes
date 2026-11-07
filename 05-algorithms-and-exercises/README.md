# 05 — Algorithms and Design Exercises

## 1. Splitwise: simplify debts

Represent each person's net balance:
- Positive: the person should receive money.
- Negative: the person owes money.

For each expense, update payer and participants according to the split. To settle, repeatedly match one debtor with one creditor.

### Greedy settlement flow
```mermaid
flowchart TD
 A[Compute net balances] --> B[Separate debtors and creditors]
 B --> C[Pick one debtor and one creditor]
 C --> D[Transfer min of amount owed and amount due]
 D --> E[Update both balances]
 E --> F{All balances zero?}
 F -->|No| C
 F -->|Yes| G[Settlement plan complete]
```

This simple greedy approach produces a valid settlement plan and is easy to explain. It does not always prove the globally minimum number of transactions for every variant. If minimum transaction count is required, discuss search/backtracking and its exponential worst-case complexity.

Use integer minor units (for example, paise) and define rounding rules for percentage splits.

## 2. Shopping cart coupons

Model a coupon as a policy with eligibility and discount calculation:
- Fixed amount off
- Percentage off
- Category-specific
- Minimum cart value
- Maximum discount
- First-order/customer-specific

Avoid hard-coding every coupon in a large conditional block.

```mermaid
sequenceDiagram
 participant C as Cart
 participant E as CouponEngine
 participant P as CouponPolicy
 C->>E: apply(coupon, cart)
 E->>P: isEligible(cart)
 P-->>E: eligible
 E->>P: calculateDiscount(cart)
 P-->>E: discount
 E-->>C: final total
```

Important decisions: Can coupons stack? Which order is applied? Is discount applied before tax or after tax? Can discount exceed item total? Define these rules explicitly.

## 3. Inventory Management System

Core objects: `Product`, `SKU`, `Warehouse`, `StockLevel`, `Reservation`, `PurchaseOrder`, `StockMovement`.

Keep on-hand, reserved and available quantities distinct:

`available = onHand - reserved`

When an order is placed, reserve stock atomically. On shipment, reduce on-hand and release reservation. On cancellation, release reservation without shipping.

```mermaid
flowchart TD
 A[Order requested] --> B[Check available stock]
 B --> C{Enough stock?}
 C -->|No| D[Reject / backorder]
 C -->|Yes| E[Reserve quantity atomically]
 E --> F[Payment / order confirmation]
 F --> G{Order fulfilled?}
 G -->|Yes| H[Ship: reduce on-hand and reserved]
 G -->|No| I[Cancel: release reserved]
```

For concurrent orders, use a database conditional update or transaction. A read-then-write in application memory is not enough.

## 4. Cache design

A cache stores frequently used data closer to the caller to reduce latency and load on the source.

### Common operations
`get(key)`, `put(key,value)`, `remove(key)`.

### Eviction policies
- LRU: evict least recently used.
- LFU: evict least frequently used.
- FIFO: evict oldest inserted item.
- TTL: expire entries after a configured time.

A common LRU implementation combines a hash map and doubly linked list:
- Hash map gives O(1) lookup of a node.
- List gives O(1) move-to-front and remove-tail.
- Overall get/put are O(1) average.

### LRU flow
```mermaid
flowchart TD
 A[get(key)] --> B{Key in map?}
 B -->|No| C[Return cache miss]
 B -->|Yes| D[Move node to list head]
 D --> E[Return value]
 F[put(key,value)] --> G{Key exists?}
 G -->|Yes| H[Update and move to head]
 G -->|No| I[Insert at head and map]
 I --> J{Capacity exceeded?}
 J -->|Yes| K[Remove tail and map entry]
 J -->|No| L[Done]
 K --> L
```

Decide whether cache operations must be thread-safe. Also discuss stale data, invalidation, cache stampede and what happens on cache failure.

## 5. Payment processing exercise

A robust payment flow should distinguish request acceptance from final settlement.

```mermaid
stateDiagram-v2
 [*] --> Created
 Created --> Pending
 Pending --> Authorized
 Pending --> Failed
 Authorized --> Captured
 Authorized --> Voided
 Captured --> RefundPending
 RefundPending --> Refunded
 Failed --> [*]
 Refunded --> [*]
```

Use idempotency keys for client retries. Store provider transaction IDs. Verify webhook signatures. Treat provider callbacks as at-least-once delivery and make handlers idempotent. Do not assume a timeout means the provider did not process the payment.

## 6. Exercise prompts

1. Add multi-currency support to Splitwise. Where should conversion rates be captured?
2. Add coupon stacking. How do you make order deterministic?
3. Add multiple warehouses. How do you select a fulfilment location?
4. Add TTL to an LRU cache. When is an entry considered expired?
5. Two customers order the last item. Which layer enforces correctness?
