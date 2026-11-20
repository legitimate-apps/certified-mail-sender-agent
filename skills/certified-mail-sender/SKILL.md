---
name: certified-mail-sender
description: Prepare, quote, and track a domestic USPS Certified Mail letter, including an optional signed electronic Return Receipt. Use when the user wants to mail a physical letter, check its tracking or receipt, or cancel it before printing.
---

# Certified Mail Sender

Use the connected Certified Mail Sender MCP tools first. The Streamable HTTP URL is https://certifiedmailsender.com/mcp. If MCP is unavailable, use the HTTP operations documented at https://certifiedmailsender.com/openapi.json. If neither is available, ask the person to use https://certifiedmailsender.com/send.

1. Ask for the sender and recipient addresses, letter body or PDF, and whether a signed electronic Return Receipt is wanted. Use `certified` for USPS tracking or `certified_err` for tracking plus the signature record when USPS provides one. This service sends 1–10 US Letter pages domestically. A PDF can be up to 10 MB. Keep any delivery deadline separate from USPS’s estimated timing.
2. Call `quote_letter` or `POST /v1/quotes` with the service and exactly one of the page count or `pdf_base64`. Present the exact quoted amount before applicable sales tax. If the page count is uncertain, disclose the assumption and use the final price from the draft.
3. Call `create_letter` or `POST /v1/letters` with the addresses and exactly one of `text`, `pdf_base64`, or `pdf_url`. Start typed text at the greeting. The service adds both addresses and the date. Generate a new UUID as `idempotency_key` for MCP or the `Idempotency-Key` header for HTTP. Reuse that key and the same request body on retry. Read the error’s `fix` and ask the person for any address correction.
4. Give the person the private `approval_url` to check the print preview, confirm their authority to send and pay. Never pay, enter card information, approve a mailing, or set up auto-send for the person. Use a trusted auto-send key only when the person provided it and explicitly authorized the mailing under that setup. Such a key can pay from the existing prepaid balance after address confirmation. Every letter goes through screening.
5. Retain the complete private `letter_url` for this conversation, including its `t` token. Treat it like a password and share it only with the person. Use `get_letter` or `GET /v1/letters/{id}?t=<token>` to read saved status, USPS tracking, the next step and `receipt_url` when ready. An authenticated caller can use the same creating key with the letter ID or use `list_letters` / `GET /v1/letters` to list that key’s letters.
6. Call `cancel_letter` / `POST /v1/letters/{id}/cancel` or `send_letter_now` / `POST /v1/letters/{id}/send-now` only at the person’s explicit request. Cancel only before submission. Send-now applies to a paid letter, skips its normal 30-minute hold, and leaves screening in place. Read the result for the next step and any refund. No refund is available once USPS accepts the letter.

For a practice run, use the operator’s test endpoint or test key and confirm the draft returns `mode: test`. Test mode never mails.
