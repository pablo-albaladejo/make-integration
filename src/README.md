# Source Code Directory

This directory contains the main implementation files for Make integrations.

## Structure

### `/modules`
Contains action and trigger modules. Each module is defined in JSON format with optional JavaScript for custom logic.

**Types of modules:**
- **Actions**: Do something (create invoice, send email, update record)
- **Triggers**: Start a workflow when something happens (new customer, invoice created)
- **Searches**: Find data (search customer by email)

### `/connections`
Connection configurations for different APIs and services.

Each connection defines:
- Authentication method (API key, OAuth, Basic Auth)
- Base URL
- Common headers
- Token refresh logic

### `/webhooks`
Webhook receivers that trigger workflows when external events occur.

### `/common`
Shared utilities and helper functions used across multiple modules:
- Data transformation functions
- Validation helpers
- Error handling utilities
- Common API wrappers

## File Naming Convention

- Use lowercase with hyphens: `create-invoice.json`
- Group related files: `invoice-create.json`, `invoice-update.json`, `invoice-delete.json`
- Keep names descriptive but short

## Module Structure Example

```json
{
  "name": "createInvoice",
  "label": "Create Invoice",
  "description": "Creates a new invoice with Veri*factu compliance",
  "type": "action",
  "connection": "myapp",
  "parameters": [
    {
      "name": "customerEmail",
      "type": "email",
      "label": "Customer Email",
      "required": true
    },
    {
      "name": "amount",
      "type": "number",
      "label": "Amount",
      "required": true
    }
  ],
  "execute": {
    "url": "/api/invoices",
    "method": "POST",
    "body": {
      "customer": "{{parameters.customerEmail}}",
      "amount": "{{parameters.amount}}"
    }
  }
}
```

## Getting Started

1. Study the examples in `/examples`
2. Copy an example module to `/modules`
3. Modify it for your needs
4. Test it in Make.com
5. Document your changes
