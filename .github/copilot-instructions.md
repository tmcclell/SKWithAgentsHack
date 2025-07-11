# GitHub Copilot Instructions for SKWithAgentsHack

## Project Overview
This is a **4-day progressive hackathon** teaching AI-powered migration automation using Azure AI Foundry, Semantic Kernel, and multi-agent systems. The project transforms manual migration processes into intelligent, automated workflows.

## Core Architecture Patterns

### Multi-Agent System Design
- **Connected Agents**: Main orchestrator delegates to specialized sub-agents (Infrastructure Assessment, Risk Analysis, Migration Planning, Cost Analysis)
- **Agent Catalog Templates**: Use pre-built templates from Azure AI Foundry for common scenarios
- **Tool Integration**: Agents use Bing Custom Search, OpenAPI, Logic Apps, and custom functions

### Migration Domain Context
- **Target Scenarios**: Enterprise applications, databases, infrastructure, PLC controllers
- **Key Artifacts**: Software analysis reports, migration steps, validation checklists, customer communication templates
- **Sample Data**: Located in `challenges/day1-foundation/docs/` - reference these for realistic migration scenarios

## Technology Stack & Integration Points

### Azure AI Foundry (Days 1-2)
- **Agent Creation**: Portal-based configuration with system messages and tool integration
- **Vector Stores**: RAG-enabled knowledge bases for migration documentation
- **Content Filters**: Responsible AI policies for enterprise deployment
- **Logic Apps**: Email automation and workflow orchestration

### Semantic Kernel (Days 3-4)
- **Plugin Architecture**: Extensible AI capabilities with function calling
- **Group Chat Orchestration**: Multi-agent coordination with round-robin management
- **Memory Management**: Context handling across long-running processes
- **Azure AI Search**: Intelligent search with vector embeddings

### GitHub Copilot & MCP (Day 3)
- **Agent Mode**: Conversational AI for complex development tasks
- **MCP Integration**: Client-server architecture for AI model communication
- **Visual Studio Professional**: Primary development environment

## Development Workflow

### Project Structure
```
challenges/
├── day1-foundation/        # Azure AI Foundry basics
│   └── docs/              # Migration domain knowledge
├── day2-ai-integration/    # Connected agents & advanced tools
├── day3-githubCopilot/     # Copilot & MCP integration
├── day3-semantic kernel/   # (Empty placeholder)
└── day4-semantic kernel/   # Semantic Kernel orchestration
```

### Key Commands & Setup
- **Azure Login**: `az login && az account set --subscription "YOUR_SUBSCRIPTION_ID"`
- **Resource Group**: `az group create --name "rg-ai-foundry-hack" --location "eastus2"`
- **Prerequisites**: .NET 8.0 SDK, Azure CLI, Azure Functions Core Tools v4

## Project-Specific Conventions

### Agent Configuration Patterns
- **System Messages**: Always include specific role definitions and Azure best practices
- **Tool Integration**: Use descriptive action names (e.g., `send_migration_email`)
- **Error Handling**: Implement retry logic and graceful degradation

### Migration Domain Expertise
- **PLC Controllers**: Reference firmware versions, hardware models, custom code analysis
- **Enterprise Systems**: Include dependency mapping, compatibility checks, backup strategies
- **Risk Assessment**: Always consider downtime, data loss, and rollback scenarios

### Documentation Standards
- **Step-by-Step Guides**: Include time estimates (e.g., "45 minutes")
- **Prerequisites**: List required Azure resources and access levels
- **Testing Scenarios**: Provide realistic migration examples for validation

## When Working on This Codebase

1. **Understand the Learning Progression**: Each day builds on previous concepts
2. **Focus on Azure Portal Workflows**: Most configuration is portal-based, not code-based
3. **Reference Migration Scenarios**: Use the docs/ folder for realistic examples
4. **Consider Multi-Agent Orchestration**: Think about task delegation and agent specialization
5. **Maintain Enterprise Focus**: All solutions should be production-ready with proper monitoring

## Common Patterns to Follow

- **Agent Instructions**: Always include numbered role definitions and specific deliverables
- **Tool Descriptions**: Use clear action names and parameter descriptions
- **Error Scenarios**: Document retry logic and fallback strategies
- **Integration Points**: Clearly define API endpoints and authentication methods
