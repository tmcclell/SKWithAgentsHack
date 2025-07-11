# 🚀 Quick Start Guide

## Prerequisites

Before starting the hackathon, ensure you have:

### Required Software
- **Visual Studio Code** or **Visual Studio 2022**
- **.NET 8.0 SDK** or later
- **Azure CLI** (latest version)
- **Azure Functions Core Tools v4**
- **Git** for version control
- **Node.js** (for MCP integration)

### Azure Resources Required
- **Azure Subscription** with sufficient credits
- **Contributor** or **Owner** role in the subscription
- **Azure OpenAI** access (request if needed)
- **Azure AI Foundry** access

### Knowledge Prerequisites
- **C# Programming**: Intermediate level
- **Azure Fundamentals**: Basic understanding of Azure services
- **REST APIs**: Understanding of HTTP methods and JSON
- **Git**: Basic version control knowledge

## Day-by-Day Setup

### Day 1 Setup: Azure AI Foundry
```bash
# 1. Login to Azure
az login

# 2. Set your subscription
az account set --subscription "YOUR_SUBSCRIPTION_ID"

# 3. Create resource group
az group create --name "rg-ai-foundry-hack" --location "eastus2"

# 4. Follow Day 1 challenges for portal-based setup
```

**What you'll create today:**
- Azure AI Foundry Hub and Project
- Deployed GPT-4 and embedding models
- AI agents for migration planning
- Vector stores with RAG capabilities
- Logic Apps for email automation

## 📅 Your 4-Day Journey

### Day 1: Foundation - Azure AI Foundry (3-4 hours)
**Focus**: Model deployment & agent creation via portal
- Deploy AI models using Azure AI Foundry
- Create and configure AI agents for migration automation
- Set up responsible AI content filters
- Configure vector stores for RAG-enabled knowledge
- Add Logic App email actions for agent integration

**Start Here**: `challenges/day1-foundation/README.md`

### Day 2: AI Integration - Connected Agents (4-5 hours)
**Focus**: Multi-agent systems & advanced tools
- Build connected multi-agent systems
- Implement Bing Custom Search and OpenAPI integrations
- Create specialized agents with tool orchestration
- Use Agent Catalog templates for accelerated development

**Start Here**: `challenges/day2-ai-integration/README.md`

### Day 3: GitHub Copilot & MCP Integration (5-6 hours)
**Focus**: AI-assisted development workflows
- Install and configure GitHub Copilot in Visual Studio
- Learn Model Context Protocol (MCP) architecture
- Set up MCP with Azure and GitHub integration
- Build enhanced development workflows

**Start Here**: `challenges/day3-githubCopilot/README.md`

### Day 4: Semantic Kernel - AI Orchestration (4-5 hours)
**Focus**: Advanced AI orchestration with C#
- Configure Azure AI Search with semantic capabilities
- Implement Semantic Kernel for AI orchestration
- Build group chat orchestration with connected agents
- Create progressive automation workflows

**Start Here**: `challenges/day4-semantic kernel/README.md`

## 🎯 Success Metrics

By the end of each day, you should have:

**Day 1**: ✅ Working Azure AI Foundry agents with deployed models and email integration
**Day 2**: ✅ Connected multi-agent systems with advanced tool integration
**Day 3**: ✅ GitHub Copilot integration with MCP-enhanced development workflows
**Day 4**: ✅ Production-ready Semantic Kernel orchestration with AI Search

## 💡 Pro Tips

### Cost Management
- Use Azure Free Tier resources when possible
- Monitor Azure OpenAI token usage and set limits
- Clean up resources after each day if not needed
- Set up cost alerts to monitor spending

### Learning Approach
- Read the entire day's README before starting
- Complete challenges in order (they build on each other)
- Test each agent thoroughly before moving to next challenge
- Document your learnings and agent configurations

### Migration Domain Focus
- Reference the sample PLC controller data in `challenges/day1-foundation/docs/`
- Practice with realistic enterprise migration scenarios
- Focus on risk assessment and validation workflows
- Consider downtime and rollback strategies

### Getting Help
- Check the troubleshooting sections in each README
- Use Azure AI Foundry documentation for agent best practices
- Leverage GitHub Discussions for community support
- Create GitHub Issues for technical problems

## 🔧 Essential Commands

### Azure CLI Essentials
```bash
# List all resource groups
az group list --output table

# Check Azure AI Foundry resources
az cognitiveservices account list --output table

# View deployment status
az deployment group list --resource-group "rg-ai-foundry-hack" --output table

# Clean up resources
az group delete --name "rg-ai-foundry-hack" --yes --no-wait
```

### Azure Portal Navigation
- **Azure AI Foundry**: https://ai.azure.com - Main platform for agent creation
- **Resource Groups**: Organize and manage related resources
- **Search Bar**: Quick access to any Azure service or resource
- **Favorites**: Pin Azure AI Foundry and related services
- **Cloud Shell**: Built-in terminal for Azure CLI commands

### Key Resource Naming Conventions
- **Resource Group**: `rg-ai-foundry-hack`
- **AI Foundry Project**: `migration-automation-project`
- **GPT-4 Deployment**: `gpt-4-migration-agent`
- **Vector Store**: `migration-knowledge-store`
- **Logic App**: `send-migration-email`

## 🎉 Ready to Begin!

You're all set! Navigate to `challenges/day1-foundation/README.md` and start your AI-powered migration automation journey.

**Remember**: This hackathon focuses on building practical AI agent solutions for real-world migration scenarios. Each day builds on the previous, creating a comprehensive automation platform.

Good luck! 🚀

---

**Need immediate help?** Check the individual challenge READMEs for detailed troubleshooting and step-by-step guidance.
