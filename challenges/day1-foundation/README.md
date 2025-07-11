# Day 1: Azure AI Foundry - Model Deployment & Agent Creation

## 🎯 Learning Objectives

By the end of Day 1, you will:
- Deploy AI models using Azure AI Foundry.
- Review Catalog of agents
- Build and configure a single AI agents for migration automation
- Test agent in Playground.
- Review thread logs for decision insight.
- Set up responsible AI content filters
- Give the agent knowledge to ground it's context.
- Add an email action that will allow the agent to send an email.

## 📚 Key Concepts Lecture

### Azure AI Foundry Overview

**Azure AI Foundry**: Next-generation AI development platform for enterprise AI solutions
- Unified experience for AI model deployment, management, and agent creation
- Enterprise-grade AI with built-in governance, security, and responsible AI controls
- Seamless integration with Azure AI services and OpenAI models
- Comprehensive model catalog with pre-trained models and deployment capabilities

### Model Deployment and Management

**Model Catalog and Deployment**: Accessing and configuring AI models for migration tasks
- GPT-4 and other foundation models for intelligent migration analysis
- Flexible deployment options with rate limiting and scaling controls
- Model versioning and lifecycle management for production environments
- Testing and validation through integrated playground environments

### AI Agent Creation and Configuration

**Migration Agent Architecture**: Building specialized AI agents for automation
- Agent personas with role-specific instructions and migration expertise
- Tool integration capabilities for external service connectivity
- Knowledge grounding through vector stores and RAG (Retrieval-Augmented Generation)
- Action orchestration for automated workflows and email notifications

### Responsible AI Implementation

**Content Safety and Governance**: Ensuring ethical and secure AI operations
- Content filtering policies to prevent harmful or inappropriate responses
- Monitoring and logging for audit trails and compliance requirements
- Responsible AI guardrails for production deployment
- Transparency features for decision tracking and explainability

## 🏗️ Challenges

### Challenge 1.1: Azure AI Foundry Model Deployment (45 minutes)

**Goal**: Deploy and configure AI models using Azure AI Foundry through Azure Portal

#### Step-by-Step Tasks:

**1.1.1 Create Azure AI Foundry Resource (15 minutes)**

**Azure AI Foundry Navigation Steps**:
1. Open [Azure AI Foundry](https://ai.azure.com) in your browser
2. Sign in with your Azure account credentials
3. Click "Create new" or "Get started" button
4. In the project creation wizard:
   - Choose **Azure AI Foundry resource**, Click Next
   - **Project name**: "migration-automation-project"
   - Click "Advanced options"
     - **Subscription**: Select your subscription
     - **Resource Group**: Create new → "rg-ai-foundry-hack"
     - **Location**: Select your region.
   - Click "Create"
5. Wait for deployment to complete (~5-7 minutes)

**1.1.2 Deploy AI Models in Azure AI Foundry (20 minutes)**

**Deploy GPT-4 Model**:
1. In your Azure AI Foundry project → Navigate to "Models + endpoints"
2. Click "Deploy a model" → "Deploy base model"
3. Browse model catalog → Search for "GPT-4"
4. Select "gpt-4" → Click "Confirm"
5. Configure deployment settings:
   - **Deployment name**: gpt-4-migration-agent
   - **Model version**: Latest available
   - **Deployment type**: Global Standard
   - **Tokens per minute rate limit**: 150K (adjust based on your needs)
6. Click "Deploy" and wait for completion (~2-3 minutes)

**Test Model Deployments**:
1. Navigate to "Models + endpoints" → Select "gpt-4-migration-agent"
2. Click "Open in playground" button
3. In the chat interface, try this prompt: 
   ```
   You are a migration planning agent. Analyze this server config: 
   Windows Server 2019, 16GB RAM, SQL Server 2017. 
   What migration considerations should I be aware of?
   ```
4. Verify the model provides a meaningful, detailed response

**1.1.3 Create AI Agent for Migration Planning (10 minutes)**

**Agent Creation Steps**:
1. In Azure AI Foundry → Navigate to "AI Services" → "Agents"
2. Choose Catalog and browse agents available
3. Return to My Agents
4. Configure agent settings:
   - **Agent name**: MigrationPlannerAgent
   - **Description**: "AI agent specialized in analyzing legacy systems and creating migration plans"
   - **Base model**: Select your deployed model.
   - **Instructions (System message)**: 
   ```
   You are an expert migration planning agent. Your role is to:
   1. Analyze legacy system configurations
   2. Identify potential migration challenges
   3. Recommend optimal Azure target architectures
   4. Create step-by-step migration plans
   5. Suggest risk mitigation strategies
   Always provide specific, actionable recommendations based on Azure best practices.
   ```

**Test Agent Functionality**:
1. Choose → Try in playground → Paste the following in the user query
   ```
   Analyze this environment for Azure migration:
   - 5 Windows Server 2016 VMs
   - SQL Server 2014 database (500GB)
   - .NET Framework 4.7 applications
   - On-premises Active Directory
   What's your migration recommendation?
   ```
   Choose → Add and run
2. Verify agent provides structured migration analysis
3. Create secret for OpenAI:
   - **Name**: OpenAI-ApiKey
   - **Value**: (Get from OpenAI resource → "Keys and Endpoint")

### Challenge 1.2: Responsible AI and Content Safety (30 minutes)

**Goal**: Configure responsible AI policies and content safety measures

#### Step-by-Step Tasks:

**1.2.1 Configure Content Filters (15 minutes)**

**Portal Content Filter Setup**:
1. In Azure AI Foundry → "Guardrails + Controls → "Content filters"
2. Click "Create content filter"
3. Configure filter policy:
   - **Name**: MigrationContentFilter → Next
   - Modify blocking thresold or accept defaults → Next
   - Apply filter to deployments → Leave unselected → Next
4. Review content filter configurations - choose **Create Filter**

**Test Content Safety**:
1. In Azure AI Studio → Navigate to your agent
2. Test with potentially harmful content to verify filtering
3. Verify appropriate responses and blocked content

**1.2.2 Configure AI Monitoring and Logging (15 minutes)**

**Enable Monitoring**:
1. Azure Portal → Your AI Foundry resource → "Monitoring"
2. Click "Create new"
3. **Name**: MigrationAppInsight → Create

### Challenge 1.3: Assistant Vector Stores (45 minutes)

**Goal**: Create and configure vector stores for RAG-enabled migration knowledge using Azure AI Foundry

#### Step-by-Step Tasks:

**1.3.1 Create Vector Store for Migration Documentation (25 minutes)**

**Create Vector Store via Azure AI Foundry**:
1. Navigate to Azure AI Foundry → Your project
2. Go to "Agents"
3. Under Knowledge - Click "+ Add"
4. Choose Files
5. Configure vector store:
   - **Vector store**: Create a new vector store
   - **Name**: migration-knowledge-store
   - **Add files**: Upload local
6. Click "Select local files". 
7. Upload the 4 files in day1-foundtion/docs.
8. Click **Upload and save**. 
9. Wait for processing to complete.
10. Open the agent and test the responses using query requests such as "search my files for validation checklist"

```

### Challenge 1.4: Create Logic App for AI Agent Integration (45 minutes)

**Goal**: Build a Logic App that integrates with your AI assistant to send automated emails

#### Step-by-Step Tasks:

**1.4.3 Configure Logic App Tool in AI Foundry as AI Agent Tool (10 minutes)**

1. Navigate to Azure AI Foundry → Your project
2. Go to "AI Services" → "Agents" → Select your MigrationPlannerAgent
3. In the agent configuration, scroll to "Actions" section
4. Click "Add" → Select "Azure Logic Apps"
5. Choose the action "**Send Email using Outlook**".
6. Configure logic app action:
   - **Action name**: `send_migration_email`
   - **Action Description**: `Send email notifications with migration analysis results to specified recipients`
   - Check resource group and location are correct.
   - Choose **Connect** and "allow access" for Office 365 Outlook to connect.
   - Choose **Next**
   - Acknowledge additional pricing notice, choose **Next**
   - Accept default schema and choose **Create**

**Update Agent Instructions**:
1. Modify agent system message to include email functionality:
   ```
   You are an expert Azure migration consultant. After completing migration analysis, 
   offer to send email notifications using the send_migration_email tool.
   
   When using the email tool:
   - Always ask for recipient email address
   - Provide clear migration status (Ready, Needs Review, High Risk)
   - Include specific recommendations
   - Summarize environment details
   
   Your analysis should cover:
   1. Server compatibility assessment
   2. Migration complexity evaluation
   3. Recommended Azure target architecture
   4. Risk mitigation strategies
   5. Estimated timeline and downtime
   ```

**Test Complete Integration**:
1. In the agent playground, test with:
   ```
   Search my files for validation checklist
   
   Send validation checklist to: admin@company.com
   ```

2. Verify the agent:
   - Provides detailed migration analysis
   - Asks for confirmation before sending email
   - Successfully calls the Logic App tool
   - Sends formatted email with recommendations

**Advanced Integration Features**:

**Add Conditional Email Logic**:
1. In Logic App designer, add "Condition" action after HTTP trigger
2. Configure condition: `migrationStatus` contains "High Risk"
3. Create separate email templates for different risk levels
4. Add Teams notification for high-risk migrations

**Error Handling**:
1. Add "Configure run after" on email action
2. Handle failed email scenarios
3. Return appropriate error messages to agent
4. Add retry logic for transient failures

## 🚀 Next Steps

After completing Day 1 challenges, you'll be ready to move to Day 2 where we'll integrate AI services and build intelligent decision-making capabilities.


