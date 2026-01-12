# Make Integration Project

A local development project for Make.com custom apps using VS Code and Make Apps SDK.

## What is this project?

This project uses the official **Make Apps Editor for VS Code** to develop custom integrations locally. You can:

- Clone apps from Make.com to your local machine
- Develop offline with full Git version control
- Deploy changes back to Make.com
- Collaborate with your team using GitHub

## Prerequisites

- **Make.com account** (not Free tier - API access required)
- **VS Code** with [Make Apps Editor extension](https://marketplace.visualstudio.com/items?itemName=Integromat.apps-sdk)
- **Git** for version control
- **Make API Key** (generate in Make.com settings)

## Project Structure

```
make-integration/
├── base/                    # Base configuration (inherited by all modules)
│   └── base.iml.json
├── modules/                 # Action, search, and trigger modules
│   └── test-webhook/
│       ├── test-webhook.communication.iml.json
│       └── test-webhook.parameters.iml.json
├── connections/             # API connection configurations
├── webhooks/                # Webhook definitions
├── rpcs/                    # Remote Procedure Calls
├── functions/               # Custom IML functions
├── common/                  # Shared common data
│   └── common.iml.json
├── .vscode/                 # VS Code configuration
│   └── settings.json
├── CLAUDE.md               # Instructions for Claude Code
├── AGENTS.md               # Custom agent definitions
└── PROBLEM_STATEMENT.md    # Business problem description
```

## File Naming Convention

Make Apps SDK uses this naming pattern:

```
component-name.block-type.iml.json
```

Examples:
- `create-invoice.communication.iml.json` - API call definition
- `create-invoice.parameters.iml.json` - Input parameters
- `create-invoice.interface.iml.json` - Output interface
- `create-invoice.samples.iml.json` - Sample data

## Getting Started

### 1. Install VS Code Extension

Search for "Make Apps Editor" in VS Code extensions or install from:
https://marketplace.visualstudio.com/items?itemName=Integromat.apps-sdk

### 2. Generate API Key

1. Log in to Make.com
2. Go to Profile > API
3. Generate a new API key
4. Copy and save it securely

### 3. Configure VS Code

1. Open VS Code
2. Press `Cmd+Shift+P` (Mac) or `Ctrl+Shift+P` (Windows)
3. Search "Make: Configure"
4. Enter your API key and environment URL

### 4. Clone or Create App

- **Clone existing**: Right-click on app in Make sidebar > Clone
- **Create new**: Right-click on "My apps" > New App

### 5. Develop Locally

Edit `.iml.json` files in VS Code with:
- Syntax highlighting
- Auto-completion
- Error checking
- Git integration

### 6. Deploy to Make

Right-click on app > Deploy to sync changes with Make.com

## Main Use Cases

This project solves automation challenges from the problem statement:

1. **Customer Support** - Intelligent ticket sorting with AI
2. **Invoice Processing** - Veri*factu compliance (sequential processing)
3. **Data Sync** - Salesforce, Intercom, internal systems
4. **Automation Governance** - Clean, documented, maintainable workflows

## Technology Stack

- **Make.com** - Integration platform
- **IML (Integromat Markup Language)** - JSON-based configuration
- **JavaScript** - Limited custom logic within modules
- **VS Code** - Local development environment
- **Git** - Version control

## Documentation

- [PROBLEM_STATEMENT.md](./PROBLEM_STATEMENT.md) - Business problems we solve
- [CLAUDE.md](./CLAUDE.md) - Instructions for AI assistance
- [AGENTS.md](./AGENTS.md) - Specialized agent definitions
- [Make Developer Hub](https://developers.make.com/custom-apps-documentation)

## License

MIT
