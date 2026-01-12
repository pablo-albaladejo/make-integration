# Claude Instructions for Make Integration Project

Instructions for Claude Code when working on this Make.com custom apps project.

## Project Context

This project uses **Make Apps SDK with VS Code** for local development of Make.com custom apps. The main challenges are:

1. Customer Support Automation
2. Invoice Processing (Veri*factu compliance)
3. Data Synchronization
4. Automation Governance

## Development Environment

### Tools
- **VS Code** with Make Apps Editor extension
- **Make Apps SDK** for local development
- **Git** for version control
- **Make.com API** for deployment

### Workflow
```
Local (VS Code) → Git Commit → Deploy to Make.com
```

## File Structure

```
make-integration/
├── base/                    # Base configuration
├── modules/                 # Action and trigger modules
├── connections/             # API connections
├── webhooks/                # Webhook definitions
├── rpcs/                    # Remote Procedure Calls
├── functions/               # Custom IML functions
└── common/                  # Shared data
```

## File Naming Convention

All Make component files follow this pattern:

```
component-name.block-type.iml.json
```

### Block Types
- `communication` - API calls (URL, method, headers, body)
- `parameters` - Input fields users fill in
- `interface` - Output structure
- `samples` - Example data for testing
- `scope` - OAuth scopes (for connections)
- `mappable` - Mappable parameters
- `static` - Static parameters

### Examples
```
create-invoice.communication.iml.json
create-invoice.parameters.iml.json
create-invoice.interface.iml.json
```

## IML JSON Structure

### Module Communication Block
```json
{
  "url": "/api/endpoint",
  "method": "POST",
  "headers": {
    "Content-Type": "application/json"
  },
  "body": {
    "field": "{{parameters.fieldName}}"
  },
  "response": {
    "output": "{{body}}"
  }
}
```

### Module Parameters Block
```json
[
  {
    "name": "fieldName",
    "type": "text",
    "label": "Field Label",
    "required": true,
    "help": "Help text for users"
  }
]
```

### Base Configuration
```json
{
  "baseUrl": "https://api.example.com",
  "headers": {
    "Authorization": "Bearer {{connection.apiKey}}"
  }
}
```

### Common Data
```json
{
  "timeout": 300000,
  "version": "1.0.0"
}
```

## IML Expressions

Use double curly braces for dynamic values:

```
{{parameters.name}}       - Input parameter
{{connection.apiKey}}     - Connection value
{{body.result}}           - Response body
{{headers.contentType}}   - Response header
{{now}}                   - Current timestamp
{{common.timeout}}        - Common data value
```

## Parameter Types

Available types for parameters:
- `text` - String input
- `number` - Numeric input
- `boolean` - True/false checkbox
- `date` - Date picker
- `select` - Dropdown list
- `email` - Email with validation
- `url` - URL with validation
- `array` - List of items
- `collection` - Object with nested fields
- `buffer` - Binary data
- `filename` - File name
- `file` - File upload

## Critical Requirements

### Security (ISO 27001)
- ✅ Use HTTPS only
- ✅ Store secrets in connections, not common data
- ✅ Never log sensitive data
- ❌ Don't hard-code API keys
- ❌ Don't expose PII in errors

### Veri*factu Compliance
- ✅ Sequential processing (use queues)
- ✅ SHA-256 hash chains
- ✅ QR code generation
- ✅ Immutable audit logs
- ❌ Never process invoices in parallel

### Error Handling
```json
{
  "response": {
    "error": {
      "type": "{{statusCode}}",
      "message": "{{body.error.message}}"
    }
  }
}
```

## Common Tasks

### Create New Module

1. Create folder: `modules/my-module/`
2. Add communication: `my-module.communication.iml.json`
3. Add parameters: `my-module.parameters.iml.json`
4. Add interface: `my-module.interface.iml.json`
5. Test in Make.com

### Create New Connection

1. Create folder: `connections/my-service/`
2. Add base: `my-service.base.iml.json`
3. Add parameters: `my-service.parameters.iml.json`
4. For OAuth: add `my-service.scope.iml.json`

### Create New Webhook

1. Create folder: `webhooks/my-webhook/`
2. Add communication: `my-webhook.communication.iml.json`
3. Add parameters: `my-webhook.parameters.iml.json`

## Testing

1. Deploy to Make.com test environment
2. Create a scenario with your module
3. Run with test data
4. Check execution logs
5. Fix issues locally
6. Redeploy

## Git Workflow

### Commits
```bash
feat: add invoice processor module
fix: correct hash calculation
docs: update parameter descriptions
```

### Branches
```
feature/invoice-processing
fix/intercom-tags
docs/api-reference
```

## Useful IML Patterns

### Conditional Value
```json
"value": "{{if(parameters.flag, 'yes', 'no')}}"
```

### Array Mapping
```json
"items": "{{map(body.items, 'item.id')}}"
```

### Date Formatting
```json
"date": "{{formatDate(now, 'YYYY-MM-DD')}}"
```

### Default Value
```json
"name": "{{ifempty(parameters.name, 'default')}}"
```

## References

- [Make Developer Hub](https://developers.make.com/custom-apps-documentation)
- [Make Apps Editor Extension](https://marketplace.visualstudio.com/items?itemName=Integromat.apps-sdk)
- [IML Reference](https://developers.make.com/custom-apps-documentation/iml)

---

**Remember**: All code is IML JSON. JavaScript is only for limited transformations within modules.
