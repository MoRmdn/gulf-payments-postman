# Test cards

**English** · [العربية](test-cards.ar.md)

These cards only work in **test mode**. They are published by each gateway. Always check the official page for the latest list.

## Moyasar

Use any name with at least two words, any future expiry date, and any 3-digit CVC (4 digits for Amex). Cards not on Moyasar's list always fail.

| Brand | Card number | Result |
|---|---|---|
| Visa | `4111 1111 1111 1111` | Paid |
| mada | `4201 3201 1111 1010` | Paid |
| Mastercard | `5421 0801 0100 0000` | Paid |
| Amex | `3400 0000 0900 000` | Paid |
| Visa | `4123 1200 0109 0000` | Failed: insufficient funds |
| mada | `4201 3200 0031 1101` | Failed: insufficient funds |
| Mastercard | `5457 2100 0100 0092` | Failed: insufficient funds |
| mada | `4201 3212 3441 1220` | Failed: declined |
| Visa | `4111 1157 8422 8433` | Failed: 3-D Secure rejected by the bank |

**STC Pay**

| Mobile number | OTP code | Result |
|---|---|---|
| Any number starting with `05` (e.g. `0512345678`) | `123456` | Paid |
| Same | `111111` | Failed: insufficient balance |
| `0515555555` | (no code) | Failed: number not registered with STC Pay |

Full list: [Moyasar test cards](https://docs.moyasar.com/guides/card-payments/test-cards).

## Tap Payments

On Tap's payment page, use CVV **`100`**. The **expiry date decides the result**:

| Expiry | Result |
|---|---|
| `01/39` | Approved |
| `05/22` | Declined |
| `04/27` | Expired card |
| `08/28` | Timed out |

| Brand | Card number | 3-D Secure |
|---|---|---|
| Visa | `4508 7500 1574 1019` | Yes |
| Visa | `4012 0000 3333 0026` | No |
| Mastercard | `5123 4500 0000 0008` | Yes |
| Mastercard | `5111 1111 1111 1118` | No |
| mada | `4464 0400 0000 0007` | Yes |
| mada | `5588 4800 0000 0003` | No |
| Amex | `3714 4963 5398 431` (CVV `1000`) | No |

KNET (Kuwait): `8888 8800 0000 0001`, expiry `09/30`, PIN `1234`.

Full list: [Tap testing cards](https://developers.tap.company/reference/testing-cards).

## HyperPay

Any future expiry date and any 3-digit CVV.

| Brand | Card number | 3-D Secure |
|---|---|---|
| Visa | `4200 0000 0000 0000` | No (used in the quick start) |
| Mastercard | `5454 5454 5454 5454` | No (used in the "hold" folders) |
| Visa | `4711 1000 0000 0000` | Yes |
| Mastercard | `5212 3456 7890 1234` | Yes |

For **mada** test cards, ask HyperPay or check their docs, because mada usually needs its own entity id.

Full list: [HyperPay test parameters](https://hyperpay.docs.oppwa.com/reference/parameters) and [3-D Secure testing guide](https://hyperpay.docs.oppwa.com/tutorials/threeDSecure/TestingGuide).
