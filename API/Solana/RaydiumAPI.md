![Raydium API Logo](../../Images/logo.png)

# Raydium API Documentation

## API Endpoints

### Buy Tokens
<details>
<summary>POST /buy</summary>

**Description:** Buy tokens on Raydium with SOL as the base currency.

**Request Body:**
```json
{
  "private_key": "<string>",
  "public_key": "<string>",
  "mint": "<string>",
  "amount": <number>,
  "useJito": <boolean> (optional, default: false)
}
```

**Example Request:**
```bash
curl -X POST http://api.smalltimedevs.com/solana/raydium-api/buy \
-H "Content-Type: application/json" \
-d '{
  "private_key": "your-private-key",
  "public_key": "your-public-key",
  "mint": "your-mint-address",
  "amount": 1.5,
  "useJito": true
}'
```

**Responses:**
- Success:
  ```json
  {
    "success": true,
    "message": "Transaction confirmed",
    "tokensPurchased": <number>,
    "txid": "<string>"
  }
  ```
- Failure:
  ```json
  {
    "success": false,
    "message": "<error_message>",
    "error": "<details_if_any>"
  }
  ```

</details>

### Sell Tokens
<details>
<summary>POST /sell</summary>

**Description:** Sell tokens for SOL on Raydium.

**Request Body:**
```json
{
  "private_key": "<string>",
  "public_key": "<string>",
  "mint": "<string>",
  "amount": <number>,
  "useJito": <boolean> (optional, default: false)
}
```

**Example Request:**
```bash
curl -X POST http://api.smalltimedevs.com/solana/raydium-api/sell \
-H "Content-Type: application/json" \
-d '{
  "private_key": "your-private-key",
  "public_key": "your-public-key",
  "mint": "your-mint-address",
  "amount": 100,
  "useJito": true
}'
```

**Responses:**
- Success:
  ```json
  {
    "success": true,
    "message": "Transaction confirmed",
    "solReceived": <number>,
    "txid": "<string>"
  }
  ```
- Failure:
  ```json
  {
    "success": false,
    "message": "<error_message>"
  }
  ```

</details>

### Market Maker Buy Tokens
<details>
<summary>POST /mmbuy</summary>

**Description:** Perform a buy operation for market makers, supporting delegate wallets.

**Request Body:**
```json
{
  "depositPubkey": "<string>",
  "depositPrivateKey": "<string>",
  "delegatePubkey": "<string>",
  "delegatePrivateKey": "<string>",
  "mint": "<string>",
  "amount": <number>,
  "useJito": <boolean> (optional, default: false)
}
```

**Example Request:**
```bash
curl -X POST http://api.smalltimedevs.com/solana/raydium-api/mmbuy \
-H "Content-Type: application/json" \
-d '{
  "depositPubkey": "your-deposit-pubkey",
  "depositPrivateKey": "your-deposit-privkey",
  "delegatePubkey": "your-delegate-pubkey",
  "delegatePrivateKey": "your-delegate-privkey",
  "mint": "your-mint-address",
  "amount": 1.0,
  "useJito": false
}'
```

**Responses:**
- Success:
  ```json
  {
    "success": true,
    "message": "Transaction confirmed",
    "tokensPurchased": <number>,
    "txid": "<string>"
  }
  ```
- Failure:
  ```json
  {
    "success": false,
    "message": "<error_message>"
  }
  ```

</details>

### Market Maker Sell Tokens
<details>
<summary>POST /mmsell</summary>

**Description:** Perform a sell operation for market makers, supporting delegate wallets.

**Request Body:**
```json
{
  "depositPubkey": "<string>",
  "depositPrivateKey": "<string>",
  "delegatePubkey": "<string>",
  "delegatePrivateKey": "<string>",
  "mint": "<string>",
  "amount": <number>,
  "useJito": <boolean> (optional, default: false)
}
```

**Example Request:**
```bash
curl -X POST http://api.smalltimedevs.com/solana/raydium-api/mmsell \
-H "Content-Type: application/json" \
-d '{
  "depositPubkey": "your-deposit-pubkey",
  "depositPrivateKey": "your-deposit-privkey",
  "delegatePubkey": "your-delegate-pubkey",
  "delegatePrivateKey": "your-delegate-privkey",
  "mint": "your-mint-address",
  "amount": 50,
  "useJito": false
}'
```

**Responses:**
- Success:
  ```json
  {
    "success": true,
    "message": "Transaction confirmed",
    "solReceived": <number>,
    "txid": "<string>"
  }
  ```
- Failure:
  ```json
  {
    "success": false,
    "message": "<error_message>"
  }
  ```

</details>

---

## Fee Structure

The following fees are associated with using this Raydium API:

- **General Fees:**
  - Priority Fee: `0.0002 SOL` (default).
  - Jito Tip Fee: `0.000001 SOL`.

- **Buy/Sell Fees:**
  - Standard Raydium Fee: `0.001 SOL`.
  - Market Maker Fee: `0.0001 SOL`.

- **High Congestion Fees:**
  - Priority Fee: `0.00008 SOL`, incrementing by `0.00002 SOL` per retry.
  - Jito Tip Fee: `0.000001 SOL`, incrementing by `0.0000005 SOL` per retry.

---

## Usage Notes

1. **Testing Environment:**
   Ensure you have a Solana wallet with sufficient SOL balance for testing.

2. **Jito Transactions:**
   Set the `useJito` flag to `true` for prioritized transactions.

3. **Market Maker Operations:**
   Use delegate wallets for advanced trading scenarios.

---

## Navigation

- **[Home](../../README.md)**: Navigate to the base README file.
- **[Applications](../../Applications/README.md)**: View documentation for Applications.
- **[APIs](../README.md)**: View documentation for APIs.

