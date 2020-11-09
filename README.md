# next-stripe

## Setup

```js
// pages/api/stripe/[...nextstripe].js

import NextStripe from "next-stripe";

const options = {
  secret_key: "...",
};

export default (req, res) => NextStripe(req, res, options);
```

## Checkout

### Create Checkout session

```js
const session = await fetch("/api/stripe/checkout/sessions", {
  method: "POST",
  body: JSON.stringify({
    success_url: "https://example.com/success",
    cancel_url: "https://example.com/cancel",
    payment_method_types: ["card"],
    line_items: [{ price: "price_H5ggYwtDq4fbrJ", quantity: 2 }],
    mode: "payment",
  }),
});
```

### Retrieve a Session

```js
const session = await fetch(
  "/api/stripe/checkout/sessions/cs_test_vMHjYeaPMz8pLHM0riwxjZRn3CURX4rqYvRjLSRlEtheSstNsFvVvlol"
);
```

### List all Sessions

```js
const sessions = await fetch("/api/stripe/checkout/sessions");
```

## Payment Intents

### Create a Payment Intent

```js
const paymentIntent = await fetch("/api/stripe/payment-intents", {
  method: "POST",
  body: JSON.stringify({
    amount: 2000,
    currency: "usd",
    payment_method_types: ["card"],
  }),
});
```

### Retrieve a Payment Intent

```js
const paymentIntent = await fetch(
  "/api/stripe/payment-intents/pi_1Dij3B2eZvKYlo2C0hrKI0qO"
);
```

### Update a Payment Intent

```js
const paymentIntent = await fetch(
  "/api/stripe/payment-intents/pi_1Dij3B2eZvKYlo2C0hrKI0qO",
  {
    method: "POST",
    body: JSON.stringify({
      amount: 3000,
    }),
  }
);
```

### Confirm a Payment Intent

```js
const paymentIntent = await fetch(
  "/api/stripe/payment-intents/pi_1Dij3B2eZvKYlo2C0hrKI0qO/confirm",
  {
    method: "POST",
    body: JSON.stringify({ payment_method: "pm_card_visa" }),
  }
);
```
