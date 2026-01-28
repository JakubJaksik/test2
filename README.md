# Binance Spot API Documentation (Test)

Test repository simulating external API documentation.
Used to test vector search for code impact analysis.
new line

---

## POST /api/v3/order

Create a new order.

### Authentication
Requires API key in header: `X-MBX-APIKEY`
Requires signature parameter (HMAC SHA256)

### Parameters:
- `symbol` (string, required): Trading pair (e.g., "BTCUSDT")
- `side` (string, required): "BUY" or "SELL"
- `type` (string, required): "LIMIT", "MARKET", "STOP_LOSS", "STOP_LOSS_LIMIT", "TAKE_PROFIT", "TAKE_PROFIT_LIMIT", "LIMIT_MAKER"
- `quantity` (decimal, required): Order quantity
- `price` (decimal, required for LIMIT orders): Order price
- `timeInForce` (string, required for LIMIT orders): "GTC" (Good Till Cancel), "IOC" (Immediate or Cancel), "FOK" (Fill or Kill)
- `timestamp` (long, required): Request timestamp in milliseconds
- `signature` (string, required): HMAC SHA256 signature

### Response:
```json
{
  "symbol": "BTCUSDT",
  "orderId": 123456,
  "clientOrderId": "myOrder1",
  "transactTime": 1499827319559,
  "price": "50000.00",
  "origQty": "0.01",
  "executedQty": "0.01",
  "status": "FILLED",
  "timeInForce": "GTC",
  "type": "LIMIT",
  "side": "BUY"
}
```

---

## GET /api/v3/account

Get current account information including balances.

### Authentication
Requires API key in header: `X-MBX-APIKEY`
Requires signature parameter

### Parameters:
- `timestamp` (long, required): Request timestamp
- `signature` (string, required): HMAC SHA256 signature

### Response:
```json
{
  "makerCommission": 15,
  "takerCommission": 15,
  "buyerCommission": 0,
  "sellerCommission": 0,
  "canTrade": true,
  "canWithdraw": true,
  "canDeposit": true,
  "updateTime": 123456789,
  "balances": [
    {
      "asset": "BTC",
      "free": "4.00000000",
      "locked": "0.00000000"
    },
    {
      "asset": "USDT",
      "free": "10000.00000000",
      "locked": "0.00000000"
    }
  ]
}
```

---

## GET /api/v3/order

Query order status.

### Authentication
Requires API key and signature

### Parameters:
- `symbol` (string, required): Trading pair
- `orderId` (long, required): Order ID
- `timestamp` (long, required): Request timestamp
- `signature` (string, required): HMAC SHA256 signature

### Response:
```json
{
  "symbol": "BTCUSDT",
  "orderId": 123456,
  "clientOrderId": "myOrder1",
  "price": "50000.00",
  "origQty": "0.01",
  "executedQty": "0.01",
  "status": "FILLED",
  "timeInForce": "GTC",
  "type": "LIMIT",
  "side": "BUY",
  "time": 1499827319559,
  "updateTime": 1499827319559
}
```

---

## Rate Limits

- 1200 requests per minute
- Weight system: each endpoint has a weight
- POST /api/v3/order: weight 1
- GET /api/v3/account: weight 10
- GET /api/v3/order: weight 2
