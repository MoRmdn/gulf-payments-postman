# How online payments work

**English** · [العربية](how-online-payments-work.ar.md)

A short, plain-language guide to the ideas behind every request in this repo.

## Test mode vs live mode

Every gateway gives you two sets of keys:

- **Test keys** (`sk_test_...`) talk to a sandbox. Payments look real, but no money moves. Use them while you learn and build.
- **Live keys** (`sk_live_...`) move real money. Only use them on your production server, and never share or commit them.

All the collections here use test mode.

## The life of a payment

```
                  ┌──► paid / CAPTURED ──► refunded
initiated ────────┤
 (waiting for     └──► failed / DECLINED
  the customer)
```

1. **Your server creates the payment.** The status is `initiated`: the gateway is waiting for the customer.
2. **The customer confirms**, for example with a 3-D Secure page or an STC Pay SMS code.
3. **The payment becomes `paid`** (Tap calls it `CAPTURED`), or it **fails**.
4. Later you can **refund** all or part of it.

## Pay now vs hold first

| | Pay now | Hold first (authorize) |
|---|---|---|
| What happens | The money is taken right away | The money is reserved on the card |
| Next step | Nothing, or a refund later | **Capture** to take it, or **void** to release it |
| Used by | Most online shops | Hotels, car rentals, orders checked by hand |
| Moyasar | `manual: false` | `manual: true` → `/capture` or `/void` |
| Tap | `POST /charges` | `POST /authorize` → charge with the auth id, or `/void` |
| HyperPay | `paymentType=DB` | `paymentType=PA` → `CP` (capture) or `RV` (reversal) |

## Refund vs void

- **Refund**: the money was already taken, and you send it back. It can take a few days to reach the customer.
- **Void / reversal**: you cancel **before** the money is taken. The customer is never charged.

## 3-D Secure: why some steps need a browser

Most cards in Saudi Arabia, including **mada**, require **3-D Secure**: the customer's bank shows a page (often an SMS code) to prove the card owner is paying. That page must open in a browser, so the API answers with a link (`transaction_url`). The customer opens it, confirms, and comes back to your site.

In the collections, these steps are in folders marked **"opens a browser"**.

## Payment page vs sending card numbers yourself

There are two ways to collect card details:

1. **Hosted payment page or widget** (Tap `transaction.url`, HyperPay COPYandPAY, the Moyasar payment form). The customer types the card on the gateway's page. Card numbers never touch your server. **This is what real apps should use.**
2. **Server-to-server**: your server sends the card number in the API request. The HyperPay quick start does this because it is the easiest way to learn. In production, this requires **PCI DSS** certification, which is expensive and strict.

## Payment links (invoices)

Moyasar and Tap can create an **invoice** with its own payment page. You send the link by WhatsApp, SMS or email, and the customer pays without you building a website. This is great for small businesses and freelancers.

## Always confirm on your server

When the customer returns from the payment page, the browser lands on your `redirect` or `callback` URL. **Do not trust that alone**, because anyone can open that URL. Your server must:

1. Read the payment from the gateway by its id (the "Fetch" / "Retrieve" / "Query" requests), and
2. Check the status **and the amount** before you ship anything.

Gateways can also call your server directly when a payment changes. These calls are named **webhooks** (Moyasar `callback_url`, Tap `post.url`).

## Amounts

Each gateway writes 10 SAR differently. Mistakes here are very common.

| Moyasar | Tap | HyperPay |
|---|---|---|
| `1000` (in halalas, 100 halalas = 1 SAR) | `10` | `"10.00"` (text, always 2 decimals) |

## Small glossary

| Word | Meaning |
|---|---|
| **Gateway** | The service your app talks to (Moyasar, Tap, HyperPay). |
| **Acquirer** | The bank that receives the money for the merchant. |
| **mada** | Saudi Arabia's national debit card network. |
| **STC Pay** | A Saudi mobile wallet. Payments are confirmed with an SMS code (OTP). |
| **OTP** | One-time password, the short code sent by SMS. |
| **3-D Secure (3DS)** | The bank's extra check that the card owner is paying. |
| **PCI DSS** | The security standard for anyone who stores or handles card numbers. |
| **Webhook** | A request the gateway sends to your server when something changes. |
| **Idempotency** | Sending the same request twice has the same effect as once, which prevents double charges. |
