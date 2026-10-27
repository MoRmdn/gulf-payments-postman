<div align="center">

# Gulf Payments Postman

**Ready-to-run Postman collections for Moyasar, Tap Payments and HyperPay, written for beginners.**

Import a file, press **Send**, watch a test payment go through. Every request is explained in English and Arabic.

[![Collections](https://github.com/MoRmdn/gulf-payments-postman/actions/workflows/collections.yml/badge.svg)](https://github.com/MoRmdn/gulf-payments-postman/actions/workflows/collections.yml)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)

**English** · [العربية](README.ar.md)

</div>

---

## Why this exists

Almost every app in Saudi Arabia and the Gulf needs online payments, and every gateway's docs look different. This repo gives you **one simple, tested path through each gateway**:

> create a payment → check it → refund it

Each request tells you what it does, which field to look at, and what to send next. Small test scripts check the response for you and pass ids to the next request automatically.

## What's inside

| Gateway | Signup needed? | Quick start (no browser) | Also covers |
|---|---|---|---|
| **Moyasar** | Yes, a free test key | STC Pay payment → OTP → refund | Card + 3-D Secure, payment links, hold → capture / void |
| **Tap Payments** | No, copy Tap's shared test key from its docs | Customer → charge → payment link | Refund after paying, hold → capture / void |
| **HyperPay** | No, shared test account included | Card payment → check → refund | Hold → capture → refund, cancel a hold, COPYandPAY checkout |

Everything runs in **test mode**. No real money moves.

## Quick start (3 steps)

1. **Download** this repo: green **Code** button → **Download ZIP** (or `git clone`).
2. Open [Postman](https://www.postman.com/downloads/) → **Import** → drag in the `collections` and `environments` folders.
3. Pick an environment in the top-right corner (for example **HyperPay (test)**), open the folder **1. Quick start (no browser)**, and press **Send** on each request in order. Check the **Test Results** tab under the response.

For **Tap** and **Moyasar**, paste a test key into the environment's `api_key` first. Tap publishes a shared one anyone can use, and Moyasar's is free. See [how to get test keys](docs/get-test-keys.md).

## Run everything from the terminal

With the [Postman CLI](https://learning.postman.com/docs/postman-cli/postman-cli-installation/):

```bash
postman collection run collections/hyperpay.postman_collection.json -e environments/hyperpay.postman_environment.json -i "1. Quick start (no browser)"
```

Swap `hyperpay` for `tap` or `moyasar`. For Tap and Moyasar, pass the key without saving it in a file:

```bash
postman collection run collections/moyasar.postman_collection.json -e environments/moyasar.postman_environment.json -i "1. Quick start (no browser)" --env-var "api_key=sk_test_YOUR_KEY"
```

## The three gateways side by side

| | Moyasar | Tap Payments | HyperPay |
|---|---|---|---|
| Test URL | `https://api.moyasar.com/v1` | `https://api.tap.company/v2` | `https://eu-test.oppwa.com` |
| Auth | Basic: secret key as username, empty password | `Bearer sk_test_...` | `Bearer <token>` + `entityId` field |
| Body format | JSON | JSON | Form fields (x-www-form-urlencoded) |
| Amount `10 SAR` | `1000` (halalas) | `10` | `"10.00"` |
| How you know it worked | `status: "paid"` | `status: "CAPTURED"` | `result.code` matches the success pattern |
| Test card that just works | `4111 1111 1111 1111` | `4508 7500 1574 1019`, exp `01/39`, CVV `100` | `4200 0000 0000 0000` |

More cards for each gateway: [docs/test-cards.md](docs/test-cards.md).

## Learn the basics

- [How online payments work](docs/how-online-payments-work.md): test vs live mode, 3-D Secure, refund vs void, payment links, and why your server must confirm every payment.
- [How to get test keys](docs/get-test-keys.md) for each gateway.
- [Test cards](docs/test-cards.md) for success, decline and insufficient funds.

## Stay safe

- **Test keys only.** Never put a live key (`sk_live_...`) in these files or in a public repo.
- Keep your own keys in Postman's environment, not in the JSON files you commit. Files named `*.local.postman_environment.json` are already in `.gitignore`.
- The HyperPay credentials in `environments/` and Tap's shared test key are **public test credentials** published in their docs. Many developers use them, so never send real personal data with them.
- Sending raw card numbers from your server is fine for learning in test mode. In a real app, use the gateway's payment page or widget unless you are PCI DSS certified.

## Contributing

Want PayTabs, Tabby, Tamara, Paymob or another gateway? Spotted a request that stopped working? See [CONTRIBUTING.md](CONTRIBUTING.md).

## Disclaimer

This is a community project. It is not affiliated with or endorsed by Moyasar, Tap Payments or HyperPay. All names and trademarks belong to their owners. Always check the official docs before going live:
[Moyasar](https://docs.moyasar.com) · [Tap](https://developers.tap.company) · [HyperPay](https://hyperpay.docs.oppwa.com)

## License

[MIT](LICENSE)

---

<div align="center">

If this saved you time, a ⭐ helps other developers find it.

</div>
