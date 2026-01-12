# Custom Agents for Make Integration Project

Specialized agents for developing Make.com custom apps with VS Code and Make Apps SDK.

## Available Agents

### 1. Module Builder Agent

**Purpose**: Create new Make modules following SDK conventions

**When to use**:
- Creating action, search, or trigger modules
- Converting API documentation to IML JSON
- Setting up module parameters and interface

**Outputs**:
- `module-name.communication.iml.json`
- `module-name.parameters.iml.json`
- `module-name.interface.iml.json`

---

### 2. Veri*factu Compliance Agent

**Purpose**: Implement invoice processing with Spanish tax compliance

**When to use**:
- Building sequential invoice processing
- Implementing hash chains (SHA-256)
- Generating QR codes for invoices
- Creating audit logs

**Key Requirements**:
- Sequential processing (no parallel)
- Hash formula: `Hash(N) = SHA-256(Data_N + Hash(N-1))`
- Immutable event logging

---

### 3. Connection Builder Agent

**Purpose**: Create API connections for Make modules

**When to use**:
- Setting up OAuth 2.0 authentication
- Configuring API key connections
- Managing token refresh logic

**Outputs**:
- `connection-name.base.iml.json`
- `connection-name.parameters.iml.json`
- `connection-name.scope.iml.json` (for OAuth)

---

### 4. Webhook Builder Agent

**Purpose**: Create webhook receivers for Make

**When to use**:
- Receiving external events
- Setting up webhook responses
- Handling incoming payloads

**Outputs**:
- `webhook-name.communication.iml.json`
- `webhook-name.parameters.iml.json`

---

### 5. IML Expert Agent

**Purpose**: Write correct IML expressions and JSON structures

**When to use**:
- Complex data transformations
- Conditional logic
- Array mapping
- Date formatting

**IML Functions**:
```
{{if(condition, true, false)}}
{{map(array, 'property')}}
{{formatDate(date, 'YYYY-MM-DD')}}
{{ifempty(value, default)}}
{{parseJSON(string)}}
```

---

### 6. Error Handler Agent

**Purpose**: Implement error handling in modules

**When to use**:
- API error responses
- Validation failures
- Timeout handling
- Retry logic

**Pattern**:
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

---

### 7. Data Sync Agent

**Purpose**: Build modules for cross-system data synchronization

**When to use**:
- Salesforce ↔ Intercom sync
- CRM data updates
- Tag management
- Contact deduplication

---

### 8. Security Auditor Agent

**Purpose**: Review modules for security compliance

**When to use**:
- Before production deployment
- Handling sensitive data (PII, financial)
- ISO 27001 compliance check

**Checks**:
- No hard-coded secrets
- HTTPS only
- Proper authentication
- No PII in logs
- Encrypted sensitive data

---

### 9. Documentation Agent

**Purpose**: Create clear documentation for modules

**When to use**:
- Adding help text to parameters
- Writing module descriptions
- Creating usage examples

**Fields to Document**:
- Module `label` and `description`
- Parameter `help` text
- Sample data in `samples.iml.json`

---

### 10. Migration Agent

**Purpose**: Convert existing automations to Make Apps SDK format

**When to use**:
- Moving from old Zapier workflows
- Converting web-based Make modules to local
- Upgrading legacy integrations

---

## Agent Selection Guide

| Task | Agent |
|------|-------|
| New module | Module Builder |
| Invoice processing | Veri*factu Compliance |
| API authentication | Connection Builder |
| Receive events | Webhook Builder |
| Complex expressions | IML Expert |
| Handle failures | Error Handler |
| Sync systems | Data Sync |
| Security review | Security Auditor |
| Add documentation | Documentation |
| Convert old code | Migration |

## Multi-Agent Workflows

### New Integration
1. **Connection Builder** - Set up API auth
2. **Module Builder** - Create modules
3. **Error Handler** - Add error handling
4. **Security Auditor** - Review
5. **Documentation** - Add docs

### Invoice System
1. **Veri*factu Compliance** - Design architecture
2. **Module Builder** - Create modules
3. **IML Expert** - Hash chain logic
4. **Security Auditor** - Compliance check

### Data Sync Project
1. **Data Sync** - Design sync flow
2. **Connection Builder** - Set up connections
3. **Module Builder** - Create sync modules
4. **Error Handler** - Handle conflicts

---

## How to Use

Ask Claude and mention the agent:

```
"Use the Module Builder Agent to create a Salesforce contact module"

"Use the Veri*factu Compliance Agent to review my invoice processor"

"Use the IML Expert Agent to help with date formatting"
```

Claude will use the appropriate agent's knowledge and patterns.
