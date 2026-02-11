# clawver-orders

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/nwang783/clawver-orders/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/nwang783/clawver-orders/SKILL.md)
> Category: AI & LLMs

---

## Description

Manage Clawver orders. List orders, track status, process refunds, generate download links. Use when asked about customer orders, fulfillment, refunds, or order history.

**Homepage:** https://clawver.store
**Repository:** N/A
**Version:** 1.1.0

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Manage Clawver orders. List orders, track status, process refunds, generate download links. Use when asked about customer orders, fulfillment, refunds, or order history.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run clawver-orders`)
**Workflow:** Execute skill logic with context from AiDarr's ATLAS memory

### T - Tools
Required tools (add as needed):
- HTTP requests (for API calls)
- Memory system (ATLAS for persistence)
- Context retrieval (from GOTCHA workspace)

### C - Context
Required context sources:
- User preferences from ATLAS memory
- Relevant documents from workspace
- Historical execution data

### H - Hard Prompts

```prompt
You are executing the clawver-orders workflow. Use the following context:

Description: Manage Clawver orders. List orders, track status, process refunds, generate download links. Use when asked about customer orders, fulfillment, refunds, or order history.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: clawver-orders
category: AI & LLMs
version: 1.1.0
user_invocable: True
homepage: https://clawver.store
```

---

## Original Skill Content



# Clawver Orders

Manage orders on your Clawver store—view order history, track fulfillment, process refunds, and generate download links.

## Prerequisites

- `CLAW_API_KEY` environment variable
- Active store with orders

## List Orders

### Get All Orders

```bash
curl https://api.clawver.store/v1/orders \
  -H "Authorization: Bearer $CLAW_API_KEY"
```

### Filter by Status

```bash
# Paid orders
curl "https://api.clawver.store/v1/orders?status=paid" \
  -H "Authorization: Bearer $CLAW_API_KEY"

# In-progress POD orders
curl "https://api.clawver.store/v1/orders?status=processing" \
  -H "Authorization: Bearer $CLAW_API_KEY"

# Shipped orders
curl "https://api.clawver.store/v1/orders?status=shipped" \
  -H "Authorization: Bearer $CLAW_API_KEY"

# Delivered orders
curl "https://api.clawver.store/v1/orders?status=delivered" \
  -H "Authorization: Bearer $CLAW_API_KEY"
```

**Order statuses:**

| Status | Description |
|--------|-------------|
| `pending` | Order created, payment pending |
| `paid` | Payment confirmed |
| `processing` | Being fulfilled |
| `shipped` | In transit (POD only) |
| `delivered` | Completed |
| `cancelled` | Cancelled |
| `refunded` | Fully refunded |

### Pagination

```bash
curl "https://api.clawver.store/v1/orders?limit=20&cursor=abc123" \
  -H "Authorization: Bearer $CLAW_API_KEY"
```

## Get Order Details

```bash
curl https://api.clawver.store/v1/orders/{orderId} \
  -H "Authorization: Bearer $CLAW_API_KEY"
```

## Generate Download Links

### Owner Download Link (Digital Items)

```bash
curl "https://api.clawver.store/v1/orders/{orderId}/download/{itemId}" \
  -H "Authorization: Bearer $CLAW_API_KEY"
```

Use this when customers report download issues or request a new link.

### Customer Download Link (Digital Items)

```bash
curl "https://api.clawver.store/v1/orders/{orderId}/download/{itemId}/public?token={downloadToken}"
```

Download tokens are issued per order item and can be returned in the checkout receipt (`GET /v1/checkout/{checkoutId}/receipt`).

### Customer Order Status (Public)

```bash
curl "https://api.clawver.store/v1/orders/{orderId}/public?token={orderStatusToken}"
```

### Checkout Receipt (Success Page / Support)

```bash
curl "https://api.clawver.store/v1/checkout/{checkoutId}/receipt"
```

## Process Refunds

### Full Refund

```bash
curl -X POST https://api.clawver.store/v1/orders/{orderId}/refund \
  -H "Authorization: Bearer $CLAW_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "amountInCents": 2499,
    "reason": "Customer requested refund"
  }'
```

### Partial Refund

```bash
curl -X POST https://api.clawver.store/v1/orders/{orderId}/refund \
  -H "Authorization: Bearer $CLAW_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "amountInCents": 500,
    "reason": "Partial refund for missing item"
  }'
```

**Notes:**
- `amountInCents` is required and must be a positive integer
- `reason` is required
- `amountInCents` cannot exceed remaining refundable amount
- Refunds process through Stripe (1-5 business days to customer)
- Order must have `status` of `paid` or `processing`

## POD Order Tracking

For print-on-demand orders, tracking info becomes available after shipping:

```bash
curl https://api.clawver.store/v1/orders/{orderId} \
  -H "Authorization: Bearer $CLAW_API_KEY"
```

Check `trackingUrl`, `trackingNumber`, and `carrier` fields in response.

### Webhook for Shipping Updates

```bash
curl -X POST https://api.clawver.store/v1/webhooks \
  -H "Authorization: Bearer $CLAW_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "url": "https://your-server.com/webhook",
    "events": ["order.shipped", "order.fulfilled"],
    "secret": "your-secret-min-16-chars"
  }'
```

## Order Webhooks

Receive real-time notifications:

```bash
curl -X POST https://api.clawver.store/v1/webhooks \
  -H "Authorization: Bearer $CLAW_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "url": "https://your-server.com/webhook",
    "events": ["order.created", "order.paid", "order.refunded"],
    "secret": "your-webhook-secret-16chars"
  }'
```

**Signature format:**
```
X-Claw-Signature: sha256=abc123...
```

**Verification (Node.js):**
```javascript
const crypto = require('crypto');

function verifyWebhook(body, signature, secret) {
  const expected = 'sha256=' + crypto
    .createHmac('sha256', secret)
    .update(body)
    .digest('hex');
  return crypto.timingSafeEqual(
    Buffer.from(signature),
    Buffer.from(expected)
  );
}
```

## Common Workflows

### Daily Order Check

```python
# Get paid orders
response = api.get("/v1/orders?status=paid")
orders = response["data"]["orders"]
print(f"New orders: {len(orders)}")

for order in orders:
    print(f"  - {order['id']}: ${order['totalInCents']/100:.2f}")
```

### Handle Refund Request

```python
def process_refund(order_id, amount_cents, reason):
    # Get order details
    response = api.get(f"/v1/orders/{order_id}")
    order = response["data"]["order"]
    
    # Check if refundable
    if order["status"] not in ["paid", "processing"]:
        return "Order cannot be refunded"
    
    # Process refund
    result = api.post(f"/v1/orders/{order_id}/refund", {
        "amountInCents": amount_cents,
        "reason": reason
    })
    
    return f"Refunded ${amount_cents/100:.2f}"
```

### Resend Download Link

```python
def resend_download(order_id, item_id):
    # Generate new download link
    response = api.get(f"/v1/orders/{order_id}/download/{item_id}")
    
    return response["data"]["downloadUrl"]
```

## Order Lifecycle

```
pending → paid → processing → shipped → delivered
            ↓
        cancelled / refunded
```

**Digital products:** `paid` → `delivered` (instant fulfillment)
**POD products:** `paid` → `processing` → `shipped` → `delivered`

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
