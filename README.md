# Mint — interactive payment sandbox

Run `python3 -m http.server 3000 --bind 0.0.0.0` in this directory.

A responsive, dependency-free interface with overview, contacts, send money, editable plans, review, simulated authorization, receipts, requests and searchable/filterable history. Google Fonts are optional; local fallbacks work without them.

## Try it
- Send the prefilled ₹7,500 to Priya. Toggle Break into payments, recalculate or edit installments. Totals must match and each installment must respect your planning ceiling.
- Change the ceiling through Settings (₹500–₹5,000).
- Review and choose a successful, declined or cancelled mock provider outcome.
- Successful payments show Pending → Processing → Success. Declines and cancellations show Pending → Failed/Cancelled.
- History includes newly simulated transactions. Download a clearly watermarked text receipt or share its text.
- Try an amount over ₹10,000: the whole-payment mock limit blocks it, regardless of installment size.

## Security boundaries — important
This is a UX prototype, **not production payment infrastructure**. No real funds, official PSP integration, bank identity verification, PINs, OTPs, or credential screens. Runtime state is in memory and resets on refresh. Request money creates only a demonstration confirmation; no request is dispatched. Plans are budgeting breakdowns, not individually submitted transactions or scheduled mandates.

The single simulated authorization is a capability of this fictional provider, not a claim that real UPI supports one authorization across arbitrary payments. No authentication secrets are collected, persisted, or logged. The busy lock prevents repeated clicks during a mock authorization; it is not production-grade server idempotency. Client-side validation is for UX only and is not a security boundary.

## Required before any live launch
- Integrate an official regulated payment-provider API/SDK. Redirect/delegate authentication exclusively to that provider. Never capture PINs, OTPs, bank credentials or biometrics.
- Create authoritative server-side payment intents with integer minor units, strict schemas, verified payees, validated amount/plan totals and provider capability checks. Enforce aggregate and per-transaction rules, KYC requirements, risk policy and bank/NPCI/PSP limits without using splitting to avoid them.
- Use authenticated sessions with secure cookies, CSRF protection, restrictive CORS/CSP, TLS, encrypted sensitive storage, managed keys and least-privilege access. Do not deploy this development HTTP server for production.
- Persist idempotency keys and enforce uniqueness atomically across requests, restarts, retries and webhooks. Use a durable state machine and transactional ledger, not browser balances.
- Verify provider signatures and payment details server-side; reject replayed webhooks and reconcile final provider state before confirming success. Never trust a client success signal.
- Apply server rate limits, velocity controls, abuse monitoring and fraud detection. Scrub logs and telemetry; establish audit trails, retention controls and incident response.
- Support scheduled plans only through provider-approved mandates, explicit consent, cancellation controls and any additional per-payment authorizations required. Honor provider fees and limits and disclose these before authorization.
- Perform security review, accessibility testing, end-to-end integration testing and regulatory review prior to live money movement.
