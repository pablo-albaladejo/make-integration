# Custom Agents for Make Integration Project

This file defines specialized agents to help with specific tasks in this Make.com integration project.

## Available Agents

### 1. Module Builder Agent
**Purpose**: Create new Make.com modules following project conventions

**When to use**:
- Creating a new integration module
- Converting API documentation to Make module JSON
- Setting up webhooks or triggers

**Capabilities**:
- Generates module JSON structure
- Creates proper parameter definitions
- Sets up error handling
- Adds documentation
- Validates against Make.com schema

**Example invocation**:
```
Create a module for the Salesforce API that creates a new contact.
The API endpoint is POST /services/data/v52.0/sobjects/Contact
Required fields: FirstName, LastName, Email
```

---

### 2. Veri*factu Compliance Agent
**Purpose**: Implement and validate Veri*factu compliance features

**When to use**:
- Building invoice processing systems
- Implementing hash chains
- Generating QR codes
- Creating audit logs
- Validating sequential processing

**Capabilities**:
- Designs sequential processing queues
- Implements SHA-256 hash chain logic
- Generates QR code URLs
- Creates immutable event logs
- Validates compliance with Orden HAC/1177/2024

**Example invocation**:
```
Review my invoice creation module and ensure it's Veri*factu compliant.
Check the hash chain calculation and QR code generation.
```

---

### 3. API Integration Specialist
**Purpose**: Connect to external APIs and handle authentication

**When to use**:
- Integrating a new API (Salesforce, Intercom, custom APIs)
- Debugging authentication issues
- Handling OAuth flows
- Managing API rate limits
- Parsing complex API responses

**Capabilities**:
- Analyzes API documentation
- Configures authentication (OAuth, API Key, Basic)
- Handles token refresh logic
- Implements rate limiting
- Maps API responses to Make variables

**Example invocation**:
```
I need to integrate with the Intercom API. Help me set up OAuth authentication
and create a module to delete tags by name (the API only accepts IDs).
```

---

### 4. Error Handler Agent
**Purpose**: Implement robust error handling and recovery

**When to use**:
- Modules are failing silently
- Need retry logic
- Handling API errors
- Creating fallback workflows
- Monitoring and alerting

**Capabilities**:
- Analyzes failure scenarios
- Implements retry strategies with backoff
- Creates error logging
- Designs fallback workflows
- Sets up monitoring alerts

**Example invocation**:
```
My invoice processing module fails when the API is temporarily unavailable.
Add proper error handling with retry logic and alerts.
```

---

### 5. Data Transformation Agent
**Purpose**: Transform and validate data between systems

**When to use**:
- Mapping data between different APIs
- Validating input data
- Transforming response formats
- Cleaning and normalizing data
- Handling edge cases

**Capabilities**:
- Writes JavaScript transformation functions
- Creates validation logic
- Handles data type conversions
- Implements data cleaning
- Manages null/undefined values

**Example invocation**:
```
I need to sync contacts from Salesforce to Intercom. The field names are different
and I need to validate email addresses and format phone numbers.
```

---

### 6. Workflow Optimizer Agent
**Purpose**: Improve performance and efficiency of existing workflows

**When to use**:
- Workflows are slow
- Too many API calls
- High costs
- Need to reduce complexity
- Optimize for scale

**Capabilities**:
- Analyzes workflow execution
- Identifies bottlenecks
- Suggests optimization strategies
- Implements batching
- Reduces unnecessary API calls
- Adds caching where appropriate

**Example invocation**:
```
My customer sync workflow makes 100+ API calls per execution.
Help me optimize it to reduce calls and improve performance.
```

---

### 7. Documentation Agent
**Purpose**: Create comprehensive documentation for modules and workflows

**When to use**:
- Documenting new modules
- Creating user guides
- Writing API references
- Explaining complex logic
- Onboarding new team members

**Capabilities**:
- Generates module documentation
- Creates user guides
- Writes inline comments
- Produces flow diagrams (text-based)
- Explains technical concepts in simple terms

**Example invocation**:
```
Document the invoice processing workflow including all modules,
error handling, and Veri*factu compliance requirements.
```

---

### 8. Security Auditor Agent
**Purpose**: Ensure integrations meet security and compliance standards

**When to use**:
- Before deploying to production
- Handling sensitive data (PII, financial)
- ISO 27001 compliance review
- Security vulnerability assessment
- Access control validation

**Capabilities**:
- Reviews modules for security issues
- Validates authentication methods
- Checks for data leakage
- Ensures encryption of sensitive data
- Validates compliance with ISO 27001
- Audits logging practices

**Example invocation**:
```
Audit my customer data sync module for security issues.
We're ISO 27001 certified and handle sensitive tax information.
```

---

### 9. Test Automation Agent
**Purpose**: Create and run tests for modules and workflows

**When to use**:
- Testing new modules
- Regression testing after changes
- Validating error handling
- Load testing
- Compliance testing

**Capabilities**:
- Generates test cases
- Creates test data
- Validates expected outputs
- Tests error scenarios
- Performs compliance validation
- Documents test results

**Example invocation**:
```
Create test cases for the invoice creation module.
Include happy path, error scenarios, and Veri*factu compliance validation.
```

---

### 10. Migration Agent
**Purpose**: Migrate automations from Zapier or other platforms to Make

**When to use**:
- Moving from Zapier to Make
- Consolidating automations
- Upgrading from simple to complex workflows
- Refactoring legacy automations

**Capabilities**:
- Analyzes existing Zapier/automation logic
- Translates to Make.com modules
- Identifies improvement opportunities
- Creates migration plan
- Maintains feature parity
- Improves error handling during migration

**Example invocation**:
```
Migrate this Zapier workflow to Make. It currently syncs Salesforce leads
to Intercom when they're marked as qualified. Improve error handling.
```

---

## How to Use These Agents

### Method 1: Direct Invocation
When working with Claude Code, mention the agent name in your request:

```
Hey Claude, use the Module Builder Agent to create a new Salesforce contact module.
```

### Method 2: Implicit Use
Claude will automatically select the appropriate agent based on your request:

```
I need to integrate with the Intercom API and handle OAuth.
```
(Claude will use the API Integration Specialist agent)

### Method 3: Multiple Agents
For complex tasks, Claude can use multiple agents in sequence:

```
Create a new invoice module (Module Builder), ensure it's Veri*factu compliant
(Compliance Agent), and add comprehensive error handling (Error Handler Agent).
```

## Agent Selection Guidelines

| Task Type | Recommended Agent | Alternative Agent |
|-----------|------------------|-------------------|
| Create new module | Module Builder | API Integration Specialist |
| Fix authentication | API Integration Specialist | Security Auditor |
| Handle errors | Error Handler | Workflow Optimizer |
| Transform data | Data Transformation | API Integration Specialist |
| Invoice compliance | Veri*factu Compliance | Security Auditor |
| Improve performance | Workflow Optimizer | Data Transformation |
| Write docs | Documentation | - |
| Security review | Security Auditor | Veri*factu Compliance |
| Write tests | Test Automation | Error Handler |
| Migrate workflow | Migration | Module Builder |

## Common Agent Workflows

### New Integration (Multi-Agent Workflow)
1. **API Integration Specialist** - Analyze API and set up authentication
2. **Module Builder** - Create module structure
3. **Data Transformation** - Handle data mapping
4. **Error Handler** - Add error handling
5. **Security Auditor** - Review security
6. **Documentation** - Document the integration
7. **Test Automation** - Create tests

### Invoice Processing (Compliance-First Workflow)
1. **Veri*factu Compliance** - Design compliant architecture
2. **Module Builder** - Create invoice modules
3. **Error Handler** - Add robust error handling
4. **Security Auditor** - Validate security and compliance
5. **Test Automation** - Test all compliance requirements
6. **Documentation** - Document compliance features

### Optimization Project (Performance Workflow)
1. **Workflow Optimizer** - Analyze and identify bottlenecks
2. **Data Transformation** - Optimize data processing
3. **API Integration Specialist** - Reduce API calls
4. **Error Handler** - Ensure reliability isn't compromised
5. **Test Automation** - Validate improvements
6. **Documentation** - Update documentation

## Agent Configuration

Each agent follows these principles:

### All Agents Must:
- Follow project conventions (see CLAUDE.md)
- Use proper JSON structure for modules
- Implement error handling
- Add clear documentation
- Consider security implications
- Validate against Make.com limitations

### All Agents Should:
- Ask clarifying questions when requirements are unclear
- Provide examples and explanations
- Suggest best practices
- Warn about potential issues
- Reference relevant documentation

### All Agents Should NOT:
- Assume you have unlimited API rate limits
- Ignore security considerations
- Create overly complex solutions
- Hard-code sensitive values
- Skip error handling
- Forget platform limitations (Make.com runtime constraints)

## Feedback and Improvements

As you use these agents, they'll learn your preferences and patterns. Key areas for improvement:

1. **Module Templates** - Agents learn your preferred module structure
2. **Error Patterns** - Common errors in your environment
3. **API Quirks** - Specific behavior of your integrated APIs
4. **Performance Needs** - Your performance requirements and constraints
5. **Security Policies** - Your organization's security standards

---

**Note**: These agents are conceptual helpers. Claude Code will use these definitions to provide more targeted and effective assistance for your specific tasks.
