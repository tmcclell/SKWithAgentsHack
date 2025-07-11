# 🚀 Quick Start Guide

## Prerequisites

Before starting the hackathon, ensure you have:

### Required Software
- **Visual Studio Code** or **Visual Studio 2022**
- **.NET 8.0 SDK** or later
- **Azure CLI** (latest version)
- **Azure Functions Core Tools v4**
- **Git** for version control
- **Node.js** (for performance testing)

### Azure Resources Required
- **Azure Subscription** with sufficient credits
- **Contributor** or **Owner** role in the subscription
- **Azure OpenAI** access (request if needed)
- **Azure AI Studio** access

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

## 📅 Your 4-Day Journey

### Day 1: Foundation (3-4 hours)
**Focus**: Azure AI services setup via portal
- Set up Azure OpenAI and Cognitive Search through portal
- Configure Key Vault and managed identity via portal
- Test AI integration through Azure AI Studio

**Start Here**: `challenges/day1-foundation/README.md`

### Day 2: AI Integration (4-5 hours)
**Focus**: Advanced AI configuration via portal
- Configure multi-agent systems in Azure AI Studio
- Build intelligent workflows through portal
- Implement function calling via portal interface

**Start Here**: `challenges/day2-ai-integration/README.md`

### Day 3: Migration Automation (5-6 hours)
**Focus**: Automation via portal tools
- Create Logic Apps workflows through portal
- Build ARM template deployments via portal
- Implement monitoring through portal dashboards

**Start Here**: `challenges/day3-migration-automation/README.md`

### Day 4: Production Ready (3-4 hours)
**Focus**: Monitoring and governance via portal
- Set up comprehensive monitoring through portal
- Implement governance via Azure Policy portal
- Deploy production-ready solution

**Start Here**: `challenges/day4-monitoring-production/README.md`

## 🎯 Success Metrics

By the end of each day, you should have:

**Day 1**: ✅ Working Azure service connections and structured logging
**Day 2**: ✅ AI-powered migration planning and decision engine
**Day 3**: ✅ Automated infrastructure deployment and migration workflows
**Day 4**: ✅ Production-ready solution with monitoring and security

## 💡 Pro Tips

### Cost Management
- Use Azure Free Tier resources when possible
- Clean up resources after each day if not needed
- Set up cost alerts to monitor spending

### Learning Approach
- Read the entire day's README before starting
- Complete challenges in order (they build on each other)
- Experiment beyond the basic requirements
- Document your learnings and insights

### Getting Help
- Check the troubleshooting sections in each README
- Use Azure documentation for detailed service information
- Leverage GitHub Discussions for community support
- Create GitHub Issues for technical problems

## 🔧 Essential Commands

### Azure CLI Essentials
```bash
# List all resource groups
az group list --output table

# View resource deployment status in portal
Portal → Resource groups → "rg-migration-hackathon" → Check deployment status

# Clean up resources via portal  
Portal → Resource groups → "rg-migration-hackathon" → Delete resource group
```

### Portal Navigation Essentials
- **Resource Groups**: Organize and manage related resources
- **Search Bar**: Quick access to any Azure service or resource
- **Favorites**: Pin frequently used services to sidebar
- **Cloud Shell**: Built-in terminal (if needed for advanced scenarios)
- **Resource Graph Explorer**: Query across all resources

### Workspace Management
- Save portal configurations as custom dashboards
- Use resource group tags for organization
- Set up cost alerts and budgets
- Configure access controls (RBAC)

## 🎉 Ready to Begin!

You're all set! Navigate to `challenges/day1-foundation/README.md` and start your portal-based AI migration automation journey.

**Remember**: This hackathon focuses on using Azure Portal for all configuration and setup. The goal is to understand the portal workflows and build practical skills without writing code.

Good luck! 🚀

---

**Need immediate help?** Check `CONTRIBUTING.md` for detailed guidelines and troubleshooting tips.
