# Claude Instructions for Make Integration Project

This file contains specific instructions for Claude Code when working on this Make.com integration project.

## Project Context

This is a Make.com (formerly Integromat) integration project focused on solving automation challenges for growing businesses. The main challenges include:

1. **Customer Support Automation** - Reduce response times through intelligent ticket sorting
2. **Invoice Processing** - Implement Veri*factu compliance with sequential processing
3. **Data Synchronization** - Keep Salesforce, Intercom, and internal systems in sync
4. **Automation Governance** - Clean up and standardize existing automations

## Technology Constraints

### What You CAN Use
- **JSON** - Primary language for module definitions
- **JavaScript** - For custom logic within modules (limited scope)
- **REST APIs** - For external integrations
- **Make.com platform** - No-code/low-code automation
- **Webhooks** - For real-time event handling

### What You CANNOT Use
- Python, Ruby, PHP, or other backend languages (Make doesn't support them)
- Custom servers or hosting (unless as external endpoints)
- Direct database access (must go through APIs)
- Complex npm packages (limited JavaScript runtime)

## File Structure Conventions

### Module Files (`src/modules/`)
- Use kebab-case: `create-invoice.json`, `send-notification.json`
- Each module must have: `name`, `label`, `description`, `type`, `connection`, `parameters`, `execute`
- Group related modules with prefixes: `invoice-create.json`, `invoice-update.json`, `invoice-delete.json`

### Connection Files (`src/connections/`)
- One file per service: `salesforce-connection.json`, `intercom-connection.json`
- Must include authentication configuration
- Never commit API keys or secrets (use environment variables)

### Common Functions (`src/common/`)
- Reusable JavaScript functions
- Data transformation utilities
- Validation helpers

## Code Style Guidelines

### JSON Modules
```json
{
  "name": "camelCaseModuleName",
  "label": "Human Readable Label",
  "description": "Clear description of what this module does",
  "type": "action",
  "connection": "service-name",
  "parameters": [
    {
      "name": "paramName",
      "type": "text|email|number|boolean|date|select",
      "label": "User-Friendly Label",
      "required": true|false,
      "help": "Optional help text",
      "default": "optional default value"
    }
  ],
  "execute": {
    "url": "/api/endpoint",
    "method": "GET|POST|PUT|DELETE|PATCH",
    "headers": {
      "Content-Type": "application/json"
    },
    "body": {
      "field": "{{parameters.paramName}}"
    },
    "response": {
      "output": {
        "id": "{{body.id}}",
        "status": "{{body.status}}"
      },
      "error": {
        "message": "{{body.error.message}}"
      }
    }
  }
}
```

### JavaScript in Modules
- Keep it simple and functional
- Avoid complex dependencies
- Use arrow functions when possible
- Always return a value

```javascript
// Good
return items.map(item => ({ id: item.id, name: item.name.toUpperCase() }))

// Bad (too complex for Make runtime)
const processItems = async () => {
  const results = await Promise.all(items.map(async item => {
    // Complex async logic
  }))
  return results
}
```

## Critical Requirements

### Security (ISO 27001 Compliance)
When working with sensitive data:
- ✅ Use HTTPS endpoints only
- ✅ Encrypt sensitive parameters
- ✅ Implement proper authentication
- ✅ Log all data access (audit trail)
- ✅ Never expose PII in logs
- ❌ Don't use public Google Sheets for data transfer
- ❌ Don't hard-code credentials
- ❌ Don't store sensitive data in variables without encryption

### Veri*factu Compliance
When working with invoice modules:
- ✅ Ensure sequential processing (use queues)
- ✅ Generate SHA-256 hash chains
- ✅ Create QR codes for each invoice
- ✅ Log all events immutably
- ✅ Prevent race conditions
- ❌ Don't process invoices in parallel
- ❌ Don't skip hash validation
- ❌ Don't allow manual invoice ordering

### Error Handling
All modules must handle errors gracefully:
- Provide clear error messages
- Include error codes when available
- Suggest remediation steps
- Log errors for monitoring
- Implement retry logic for transient failures

Example:
```json
{
  "response": {
    "error": {
      "type": "{{statusCode}}",
      "message": "Failed to create invoice: {{body.error.message}}",
      "detail": "{{body.error.detail}}",
      "remediation": "Check that all required fields are provided and the customer exists"
    }
  }
}
```

## Common Tasks

### Task: Create a New Module
1. Copy `examples/simple-module.json` to `src/modules/your-module.json`
2. Update `name`, `label`, `description`
3. Define `parameters` based on what inputs are needed
4. Configure the `execute` block with API details
5. Map the `response` output
6. Test with Make.com platform
7. Document in module comments

### Task: Add API Connection
1. Create `src/connections/service-name.json`
2. Define authentication method (OAuth, API Key, Basic)
3. Set base URL and common headers
4. Test authentication flow
5. Document required credentials

### Task: Implement Sequential Processing
For Veri*factu compliance or any sequential workflow:
1. Create a queue system (external or using Make's built-in queue)
2. Ensure single-threaded processing
3. Implement hash chain calculation
4. Add error recovery (what happens if one item fails?)
5. Log all processing steps

### Task: Debug an Integration
1. Check Make.com execution logs
2. Verify API credentials are valid
3. Test API endpoints directly (Postman, curl)
4. Check parameter mapping ({{parameters.x}})
5. Verify response structure matches expectations
6. Add console logging if available

## When Asking Claude for Help

### DO Provide:
- The specific module or file you're working on
- The error message or unexpected behavior
- What you've already tried
- The Make.com execution log (if available)
- The API documentation you're integrating with

### Example Good Question:
"I'm working on `src/modules/create-invoice.json` and getting a 401 error. The API docs say to use Bearer token authentication. I've set up the connection with `Authorization: Bearer {{connection.token}}` but it's still failing. Here's the error log: [paste log]. What am I missing?"

### Example Bad Question:
"My module doesn't work. Fix it."

## Testing Strategy

1. **Unit Test**: Test each module independently in Make.com
2. **Integration Test**: Test the full workflow end-to-end
3. **Error Test**: Deliberately cause errors and verify handling
4. **Load Test**: For critical paths, verify performance with volume
5. **Compliance Test**: For Veri*factu, verify hash chains and QR codes

## Documentation Requirements

Every module must include:
- Clear `description` field
- Help text for non-obvious parameters
- Comments explaining complex logic
- Example usage in comments or separate file

## Performance Considerations

- Minimize API calls (batch when possible)
- Use pagination for large datasets
- Implement caching where appropriate
- Consider rate limits (add delays if needed)
- Monitor execution time (Make has timeout limits)

## Git Workflow

### Commit Messages
Use conventional commits:
- `feat: add invoice creation module`
- `fix: correct hash calculation in Veri*factu`
- `docs: update API connection instructions`
- `refactor: simplify ticket classification logic`
- `test: add validation for QR code generation`

### Branch Naming
- `feature/invoice-processing`
- `fix/intercom-tag-deletion`
- `docs/api-reference`

## Useful References

- [Make.com Modules Documentation](https://www.make.com/en/help/modules)
- [Make.com API Reference](https://www.make.com/en/api-documentation)
- Project files:
  - `PROBLEM_STATEMENT.md` - Understand the business problems
  - `docs/GETTING_STARTED.md` - Quick start guide
  - `examples/` - Working examples
  - `src/README.md` - Source code structure

## Common Pitfalls to Avoid

1. **Forgetting Make.com Limitations**: Remember you're in a limited JavaScript runtime, not Node.js
2. **Ignoring Rate Limits**: APIs have limits; implement backoff strategies
3. **Hardcoding Values**: Use parameters and connection variables
4. **Poor Error Messages**: Users need actionable error information
5. **No Validation**: Validate inputs before making API calls
6. **Overcomplicating**: Start simple, add complexity only when needed

## When to Use Custom Code vs. Make Modules

### Use Make Modules When:
- The logic is straightforward (CRUD operations)
- Built-in error handling is sufficient
- Performance is not critical
- Rapid prototyping is needed

### Use Custom Code (external endpoints) When:
- Complex business logic is required
- Need access to specific libraries
- Performance is critical
- Advanced error handling is needed
- Veri*factu hash chain calculations (precision matters)

## Project-Specific Notes

### Veri*factu Implementation
- Hash function: SHA-256
- Chain formula: `Hash(N) = SHA-256(Data_N + Hash(N-1))`
- QR Code: Must include URL to AEAT verification
- Sequential processing: CRITICAL - no parallel invoice creation

### Intercom Integration
- Tag deletion requires ID, not name (need mapping step)
- Use cache for tag name-to-ID mapping
- Refresh cache daily

### Trustpilot Integration
- OAuth 2.0 with token refresh
- Build custom middleware for authentication
- Invite links must be generated immediately after positive interaction

### Salesforce Sync
- Use Salesforce REST API v52+
- Implement field mapping for custom fields
- Handle API version updates

---

**Remember**: This project prioritizes reliability and compliance over speed. A slow, correct automation is better than a fast, broken one.
