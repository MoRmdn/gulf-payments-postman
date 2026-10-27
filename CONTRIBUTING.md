# Contributing

Thanks for helping! Contributions in English or Arabic are both welcome.

## Easy ways to help

- **A request stopped working?** Open an issue with the request name and the response you got (remove any keys first).
- **A typo or unclear explanation?** Open a pull request. Better wording for beginners is always welcome.
- **Translation:** improve the Arabic files (`*.ar.md`) or the Arabic parts of request descriptions.

## Add a new gateway

Wanted: PayTabs, Tabby, Tamara, Paymob, Checkout.com, Geidea, and others.

Follow the same pattern as the existing collections so beginners feel at home:

1. **Files:** `collections/<gateway>.postman_collection.json` (Postman Collection v2.1) and `environments/<gateway>.postman_environment.json`.
2. **Auth once:** set authentication on the collection and let requests inherit it. Keys live in environment variables (`api_key`, `base_url`), never in requests.
3. **Numbered folders:** start with `1. Quick start (no browser)` if the gateway allows it, then folders that need a browser, then `Advanced`.
4. **Numbered requests** with a short description in this shape:
   - **What it does**
   - **Look at** (which response field matters)
   - **Next** (which request to send next)
   - Then `---` and the same in Arabic.
5. **Small test scripts:** check the HTTP status and the payment status with `pm.test`, and save ids with `pm.collectionVariables.set(...)`. Add a comment above anything that is not obvious.
6. **No secrets:** leave `api_key` empty and explain how to get one in `docs/get-test-keys.md`. Even public test keys that look like `sk_test_...` are blocked by GitHub's push protection, so link to the gateway's page instead of pasting them.
7. **Docs:** add the gateway to the tables in both READMEs and to `docs/test-cards.md` (and the `.ar.md` files).

## Before you open a pull request

Run your quick start folder with the Postman CLI and make sure every test passes:

```bash
postman collection run collections/<gateway>.postman_collection.json -e environments/<gateway>.postman_environment.json -i "1. Quick start (no browser)"
```

If your change needs a browser step (3-D Secure, hosted page), say in the pull request that you tested it by hand.
