# How to get test keys

**English** · [العربية](get-test-keys.ar.md)

| Gateway | Can I start right away? | What you need for your own project |
|---|---|---|
| Moyasar | No, but signup is free and quick | Your own test secret key |
| Tap Payments | Yes, copy the shared test key from Tap's docs | Your own test secret key |
| HyperPay | Yes, a shared test account is already in the environment | Test credentials from HyperPay |

## Moyasar

1. Sign up for free at [dashboard.moyasar.com](https://dashboard.moyasar.com/register/new).
2. Go to **Settings → API Keys** and find the **Test Keys** section. The Live/Test switch at the top doesn't matter here: it only changes which payments the dashboard shows.
3. Copy the test **Secret Key** (it starts with `sk_test_`). It is shown **only once**, so save it somewhere safe (a password manager).
   Lost it? Click **Regenerate Key** next to the **test** secret key. Never regenerate the live keys.
4. In Postman, open the **Moyasar (test)** environment and paste the key into `api_key`. Save.

Moyasar also gives you a **publishable key** (`pk_test_...`). It is meant for your website's payment form. The collections here use the secret key.

## Tap Payments

**To start:** open Tap's [testing keys page](https://developers.tap.company/reference/testing-keys), copy the shared **secret** test key (`sk_test_...`), and paste it into `api_key` in the **Tap (test)** environment.

> Why isn't it already in the file? GitHub's secret scanning blocks any pushed file containing a key that looks like `sk_test_...`, even a public one.

**For your own project:**

1. Create an account at [tap.company](https://www.tap.company).
2. In the dashboard, open **goSell → API Credentials**.
3. Copy your **test secret key** (`sk_test_...`) and paste it into `api_key` in the **Tap (test)** environment.

With your own key you only see your own test charges, and your dashboard shows every request.

## HyperPay

**To start:** nothing to do. The **HyperPay (test)** environment already contains the shared demo account that HyperPay uses in its [developer docs](https://hyperpay.docs.oppwa.com).

> The shared demo account only accepts **EUR**, which is why `currency` is `EUR` in the environment.

**For your own project:**

1. Contact HyperPay at [hyperpay.com](https://www.hyperpay.com) and complete merchant onboarding.
2. They send you a test **access token** and one or more **entity ids**. You often get a separate entity id for **mada**.
3. Paste them into `access_token` and `entity_id` in the **HyperPay (test)** environment, and set `currency` to `SAR`.

## Keep your keys safe

- Never commit keys to Git. Save a copy of the environment as `something.local.postman_environment.json`; that name is ignored by Git in this repo.
- From the terminal, pass keys with `--env-var "api_key=..."` instead of writing them into files.
- If a key leaks, delete it in the dashboard and create a new one.
