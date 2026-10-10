---
name: taptax
description: 'UK self-employed tax with TapTax: tax owed so far, receipts and expenses, mileage, invoices, the transaction review queue, PAYE tax codes, and Making Tax Digital quarterly updates and deadlines for sole traders and landlords.'
---

# TapTax

TapTax is Making Tax Digital (MTD) software for UK sole traders and landlords.
It keeps their income, expenses, mileage and invoices, estimates their tax, and files their quarterly updates to HMRC.
Use these tools when someone asks about their own UK self-employed or property tax, their TapTax records, or MTD.

## Facts to work with

- Money is in pounds sterling. Amounts are VAT-inclusive unless a tool says otherwise.
- UK tax years run 6 April to 5 April and are written like `2026-27`.
- MTD quarterly updates are cumulative: each one covers 6 April to the end of the quarter (5 July, 5 October, 5 January, 5 April) and is due on the 7th of the month after.
- Estimates are not tax advice. Say so when someone is about to rely on a figure.

## Signing in

`estimate_self_employed_tax`, `check_tax_code`, `check_mtd_status`, `get_mtd_deadlines` and every calculator and document tool below work for anyone, with no TapTax account.
The tools for the person's own records (tax position, transactions, mileage, invoices, the quarterly update) act on their account; the first one used prompts them to connect TapTax, on taptax.co.uk.

## Calculators and documents

More than 30 calculators work without an account and give the same figures as taptax.co.uk/tax-calculator: pay (`calculate_take_home_pay` and the salary converters), company and contractor pay (`compare_salary_and_dividends`, `compare_limited_company_and_sole_trader`, `calculate_contractor_day_rate`), property and investments (`calculate_capital_gains_tax`, `calculate_stamp_duty`, `calculate_rental_income_tax`), VAT, CIS, mileage and penalties.
Each result has a `summary` to lead with and a `moreDetail` link to the page.
`prepare_business_document` returns a link that opens TapTax's free generator with an invoice, quote or receipt filled in; the person downloads the PDF there.

## Filing to HMRC

Filing never happens from the chat.
`prepare_quarterly_update` gathers the cumulative figures and shows a card whose button opens TapTax on the submit page for that period, where the person checks the figures and files.
HMRC needs fraud-prevention details about the device the person files from, which a chat cannot supply.
Never tell someone a return is filed unless `get_tax_position` lists that quarter as filed.

## Changing records

- When reading a receipt, confirm any unclear amount, date or supplier before `add_transaction`.
- Pick the expense category from the HMRC self-employment boxes the tool lists; ask when two could fit.
- `send_invoice` emails nothing by itself: it shows the invoice in a card, and the person sends it with the card's Send button. Never say an invoice was sent unless the card says so or `list_invoices` shows it sent.
- `update_transaction` is how review-queue items get a business or personal decision; work through `list_transactions` with `needsReview` one item at a time.
- Mileage logging is a Pro feature, and the free plan includes three invoices. When a tool refuses because of a plan limit, say so plainly and point to taptax.co.uk.

## Good answers

- Lead with the number the person asked for, then the few figures that explain it.
- Name the tax year and the period a figure covers.
- When transactions still need reviewing, say how many and that they are counted as business until decided.
