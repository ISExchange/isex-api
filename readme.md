# ISEX - API Documentation

## Endpoints

### GET /api

Returns a list of available endpoints.

#### Response

- `200 OK` - Returns a JSON object containing a list of available endpoints.

##### Example

Request:

```
GET /api
```

Response:

```json
{
    "endpoints": [
        "/api",
        "/api/symbol/retrieve",
        "/api/symbol/create"
    ]
}
```

### GET /api/symbol/retrieve

Returns a list of symbols or specific symbol information.

#### Query Parameters

- `api_key` (required) - The API key to use for authentication.

#### Request Body

- `symbol` (optional) - The symbol to retrieve information for.

#### Response

- `200 OK` - Returns a JSON object containing a list of symbols or specific symbol information.

##### Example

Request:

```
GET /api/symbol/retrieve?api_key=1234567890
```

Response:

```json
{
    "symbols": [
        "AAPL",
        "MSFT",
        "GOOG",
        "AMZN"
    ]
}
```

Request:

```
GET /api/symbol/retrieve?api_key=1234567890
Content-Type: application/json

{
    "symbol": "AAPL"
}
```

Response:

```json
{
    "symbol": "AAPL",
    "name": "Apple Inc.",
    "last": 148.48,
    "sector": "Technology",
    "industry": "Consumer Electronics",
    "sharesOutstanding": 16687500000,
    "marketCap": 247630000000
}
```

### GET /transactions

Returns a JSON object containing information about the transactions of the API key.

#### Query Parameters

- `api_key` (required) - The API key for the user making the request.

#### Response

- `200 OK` - Returns a JSON object containing a list of symbols or specific symbol information.

##### Example

Request:

```
GET /transactions?api_key=1234567890
```

Response:
```json
{
    "transactions": [
        {"id": 1, "time": "2023-10-24 09:30:01", "symbol": "AAPL", "side": "BUY", "price": 150.10, "volume": 500},
        {"id": 2, "time": "2023-10-24 09:30:02", "symbol": "MSFT", "side": "SELL", "price": 220.20, "volume": 300},
        {"id": 3, "time": "2023-10-24 09:30:03", "symbol": "MAMA", "side": "BUY", "price": 10.30, "volume": 1000},
    ]
}
```

### POST /api/symbol/create

A POST endpoint for creating a new symbol.

#### Query Parameters

- `api_key` (required) - The API key to use for authentication.

#### Request Body

- `symbol` (required) - The symbol to create.
- `name` (required) - The name of the symbol.
- `sector` (required) - The sector the symbol belongs to.
- `industry` (required) - The industry the symbol belongs to.
- `outstanding_shares` (required) - The number of outstanding shares for the symbol.

#### Response

- `200 OK` - Returns a JSON object containing status, and error message (if any).

##### Example

Request:

```
POST /api/symbol/create?api_key=1234567890
Content-Type: application/json

{
    "symbol": "MSFT",
    "name": "Microsoft Corporation",
    "sector": "Technology",
    "industry": "Software",
    "outstanding_shares": 1000000
}
```

Response:

```json
{
    {
    "status": {
        "status": "success"
    }
}
}
```

### POST /api/order/add
A POST endpoint for adding a new order.

#### Query Parameters

- `api_key` (required): The API key for the user making the request.

#### Request Body

- `symbol` (required) - The symbol of the stock being traded.
- `side` (required) - The side of the order representing the buyer or seller.
- `price` (required) - The price of the order.
- `volume` (required) - The volume of the order.

#### Response

- `200 OK` - Returns a JSON object containing status of the order placement.

##### Example

```
POST /api/order/add?api_key=1234567890

{
  "symbol": "AAPL",
  "side": "BUY",
  "price": 150.0,
  "volume": 100
}
```

Response:

```json
{
    {
    "status": {
        "status": "success"
    }
}
}
```

## Authentication

All endpoints require authentication using an API key. The API key must be passed as a query parameter in the request URL.

If the API key is not valid or is missing, the endpoint will return a `401 Unauthorized` or `403 Forbidden` error.

## Permissions

Some endpoints require specific permissions to access. The required permissions are specified in the `require_permission` decorator for each endpoint.

If the API key does not have the required permissions, the endpoint will return a `403 Forbidden` error.

## API Documentation

API documentation is available at `/api/docs`. The documentation is provided in YAML format.
