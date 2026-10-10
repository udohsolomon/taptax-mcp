<p align="center"><img src="assets/logo.svg" width="72" alt="TapTax"></p>

# TapTax MCP server

TapTax is Making Tax Digital (MTD) software for UK sole traders and landlords.
This repository holds the public connection details for the TapTax MCP server, plus ready-made plugins for Claude Code and Cursor.
The server itself is hosted by TapTax; there is nothing to install or run.

- **Server URL:** `https://api.taptax.co.uk/mcp` (Streamable HTTP)
- **Registry name:** `uk.co.taptax/taptax` on the [Official MCP Registry](https://registry.modelcontextprotocol.io/v0/servers?search=uk.co.taptax/taptax)
- **Auth:** none for the 37 public tools; OAuth 2.1 (PKCE, client ID metadata documents or dynamic client registration) for the 11 tools that act on your own TapTax account
- **Docs:** [taptax.co.uk/integrations/claude](https://taptax.co.uk/integrations/claude) and [taptax.co.uk/integrations/chatgpt](https://taptax.co.uk/integrations/chatgpt)

Ask in plain English: how much tax you owe so far this year, which transactions still need reviewing, log this receipt, invoice a client, or get your quarterly update ready.
The 37 public tools work with no account: the tax estimate, PAYE tax code checker, MTD eligibility and deadlines, and every calculator at [taptax.co.uk/tax-calculator](https://taptax.co.uk/tax-calculator).

## Connect

### Claude

Add **TapTax** from the [Claude connector directory](https://claude.ai/directory/connectors/taptax), or add a custom connector with the server URL above.

### Claude Code

Install the plugin from this repository:

```
/plugin marketplace add udohsolomon/taptax-mcp
/plugin install taptax@taptax
```

Or add just the server:

```bash
claude mcp add --transport http taptax https://api.taptax.co.uk/mcp
```

Then run `/mcp`, choose **taptax** and **Authenticate** to use your own records.

### Cursor

Install the TapTax plugin from the Cursor Marketplace, or add the server to `~/.cursor/mcp.json`:

```json
{
  "mcpServers": {
    "taptax": { "url": "https://api.taptax.co.uk/mcp" }
  }
}
```

### VS Code

```bash
code --add-mcp '{"name":"taptax","type":"http","url":"https://api.taptax.co.uk/mcp"}'
```

### Any other MCP client

Point it at `https://api.taptax.co.uk/mcp` over Streamable HTTP.
The account tools answer an unauthenticated call with HTTP 401 and a `WWW-Authenticate` header naming the protected resource metadata, so clients that support MCP authorization start the sign-in themselves.

## Tools

### Public (no account)

| Tool | What it does |
| --- | --- |
| `estimate_self_employed_tax` | Estimate self-employed tax |
| `check_tax_code` | Check a PAYE tax code |
| `check_mtd_status` | Check if Making Tax Digital applies |
| `get_mtd_deadlines` | Making Tax Digital deadlines |
| `calculate_take_home_pay` | Calculate take-home pay |
| `calculate_gross_salary_for_take_home` | Work out the salary for a take-home figure |
| `calculate_salary_sacrifice` | Calculate salary sacrifice savings |
| `calculate_pro_rata_salary` | Calculate a pro rata salary |
| `convert_hourly_rate_to_salary` | Convert an hourly rate to a salary |
| `convert_salary_to_hourly_rate` | Convert a salary to an hourly rate |
| `calculate_student_loan_repayment` | Calculate student loan repayments |
| `calculate_child_benefit_charge` | Calculate the High Income Child Benefit Charge |
| `calculate_tax_on_multiple_incomes` | Calculate tax on several incomes |
| `calculate_pension_tax_relief` | Calculate pension tax relief |
| `calculate_dividend_tax` | Calculate dividend tax |
| `compare_salary_and_dividends` | Compare salary and dividends |
| `compare_limited_company_and_sole_trader` | Compare a limited company and sole trader |
| `calculate_corporation_tax` | Calculate corporation tax |
| `calculate_contractor_day_rate` | Calculate contractor day rate income |
| `compare_inside_and_outside_ir35` | Compare inside and outside IR35 |
| `calculate_cis_deduction` | Calculate a CIS deduction |
| `plan_quarterly_tax_set_aside` | Plan how much tax to set aside |
| `calculate_mileage_allowance` | Calculate the mileage allowance |
| `estimate_self_assessment_penalties` | Estimate Self Assessment penalties |
| `calculate_vat` | Add or remove VAT |
| `check_vat_registration` | Check VAT registration and the Flat Rate Scheme |
| `check_vat_reverse_charge` | Check the construction VAT reverse charge |
| `calculate_markup` | Calculate a price from a markup |
| `calculate_profit_margin` | Calculate a profit margin |
| `calculate_invoice_due_date` | Calculate an invoice due date |
| `calculate_late_payment_interest` | Calculate late payment interest on an invoice |
| `calculate_capital_gains_tax` | Calculate Capital Gains Tax |
| `calculate_rental_income_tax` | Calculate tax on rental income |
| `calculate_savings_interest_tax` | Calculate tax on savings interest |
| `calculate_stamp_duty` | Calculate Stamp Duty |
| `prepare_business_document` | Prepare an invoice, quote or receipt to download |
| `generate_invoice_numbers` | Generate invoice numbers |

### Your TapTax account

| Tool | What it does | Access |
| --- | --- | --- |
| `get_tax_position` | Get my tax position | read |
| `list_transactions` | List my transactions | read |
| `get_mileage_summary` | Get my mileage | read |
| `add_transaction` | Add income or an expense | read and change |
| `update_transaction` | Update or review a transaction | read and change |
| `log_mileage_trip` | Log a business trip | read and change |
| `list_invoices` | List my invoices | read |
| `create_invoice` | Create an invoice | read and change |
| `send_invoice` | Show an invoice ready to send | read and change |
| `mark_invoice_paid` | Mark an invoice paid | read and change |
| `prepare_quarterly_update` | Prepare my quarterly update | read |

You sign in on taptax.co.uk and choose read-only or read-and-change access, and you can disconnect at any time in TapTax Settings > Connected apps.

## What TapTax never does from a chat

- **File to HMRC.** HMRC's fraud-prevention rules need details of the device you file from, so `prepare_quarterly_update` shows the figures with a button that opens TapTax on the right period, and the last tap is yours.
- **Email an invoice by itself.** `send_invoice` shows the invoice in a card, and it is emailed only when you press Send on that card.
- **Move money or reveal bank or HMRC logins.**

Estimates are not tax advice.

## What is in this repository

| Path | Purpose |
| --- | --- |
| `server.json` | The Official MCP Registry entry |
| `.claude-plugin/` | Claude Code plugin manifest and marketplace |
| `.cursor-plugin/plugin.json` | Cursor plugin manifest |
| `.mcp.json`, `mcp.json` | The remote server for Claude Code and Cursor |
| `skills/taptax/SKILL.md` | Guidance the assistant loads with the plugin |
| `glama.json` | Glama ownership claim |

## Support and privacy

- Support: [support@taptax.co.uk](mailto:support@taptax.co.uk)
- Privacy policy: [taptax.co.uk/privacy](https://taptax.co.uk/privacy)
- Terms: [taptax.co.uk/terms](https://taptax.co.uk/terms)

TapTax is a trading name of HomePortfolio HQ Ltd.
