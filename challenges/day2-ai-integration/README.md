# Day 2: AI Integration - Connected Agents & Advanced Tools

## 🎯 Learning Objectives

By the end of Day 2, you will:
- Build connected multi-agent systems using Azure AI Foundry
- Implement advanced tools including Bing Custom Search and OpenAPI integrations
- Create specialized agents with sophisticated tool orchestration
- Use Agent Catalog templates to accelerate development

## 📚 Key Concepts

### Connected Agents
Connected agents enable collaborative multi-agent systems where a main agent intelligently delegates tasks to specialized sub-agents without requiring custom orchestration code. This modular approach improves reliability, traceability, and extensibility for complex workflows.

### Agent Catalog Templates
Azure AI Foundry provides pre-built agent templates for common scenarios including browser automation, compliance checking, healthcare workflows, and research tasks. These templates accelerate development with proven patterns and best practices.

### Advanced Tools
- **Bing Custom Search**: Domain-specific search capabilities with configurable sources
- **OpenAPI Integration**: Standardized API connectivity with authentication and security controls

## 🏗️ Tutorial Walkthroughs

### Walkthrough 2.1: Connected Agents for Migration Planning (60 minutes)

**Summary**: Learn to build connected multi-agent systems that break down complex migration tasks across specialized agents. This walkthrough demonstrates how to create a main orchestrator agent that intelligently delegates to specialized sub-agents without custom orchestration code.

**Prerequisites**: 
- Azure AI Foundry project with deployed GPT-4 model
- Access to Azure AI Foundry portal

**Step-by-Step Guide**:

**Step 1: Create the Main Orchestrator Agent (15 minutes)**
1. Navigate to Azure AI Foundry → Your project → "Agents"
2. Click "Create agent" and configure:
   - **Name**: MigrationOrchestratorAgent
   - **Description**: "Main coordination agent for migration planning workflows"
   - **Model**: Select your deployed GPT-4 model
   - **Instructions**: 
   ```
   You are a migration planning coordinator. Your role is to:
   1. Analyze user requests and determine the type of migration task
   2. Route assessment tasks to the Infrastructure Assessment Agent
   3. Route risk analysis tasks to the Risk Analysis Agent
   4. Route planning tasks to the Migration Planning Agent
   5. Synthesize results from specialized agents into comprehensive recommendations
   
   Always provide clear reasoning for task delegation and ensure all aspects of migration planning are covered.
   ```

**Step 2: Create Specialized Connected Agents (30 minutes)**
1. Create Infrastructure Assessment Agent:
   - **Name**: InfrastructureAssessmentAgent
   - **Description**: "Specialized agent for analyzing legacy systems and mapping to Azure services"
   - **Instructions**: Focus on Azure service mapping, resource requirements, and costs

2. Create Risk Analysis Agent:
   - **Name**: RiskAnalysisAgent
   - **Description**: "Specialized agent for identifying and analyzing migration risks"
   - **Instructions**: Focus on technical, business, and operational risks with mitigation strategies

3. Create Migration Planning Agent:
   - **Name**: MigrationPlanningAgent
   - **Description**: "Specialized agent for creating detailed migration execution plans"
   - **Instructions**: Focus on phases, timelines, dependencies, and resource requirements

**Step 3: Configure Connected Agent Relationships (15 minutes)**
1. In your MigrationOrchestratorAgent, scroll to "Connected agents" section
2. Click "Add +" and configure connections:
   - **Agent**: Select InfrastructureAssessmentAgent
   - **Name**: infrastructure_assessment
   - **Description**: "Analyze infrastructure configurations and recommend Azure services mapping"
3. Repeat for other specialized agents

**Step 4: Test the Connected System**
1. Navigate to orchestrator agent → "Try in playground"
2. Test with: "I need to migrate a legacy ERP system with 15 Windows Server 2012 R2 VMs, SQL Server 2014 cluster with 2TB database, .NET Framework 4.5 applications, and 5TB file servers. 100 concurrent users, 99.9% uptime requirement, $300K budget, 8-month timeline."
3. Verify orchestrator routes tasks to appropriate agents and synthesizes results

**Documentation Reference**: [Connected Agents Documentation](https://learn.microsoft.com/en-us/azure/ai-foundry/agents/how-to/connected-agents?pivots=portal)

### Walkthrough 2.2: Agent Catalog Templates (30 minutes)

**Summary**: Explore and customize pre-built agent templates from the Azure AI Foundry Agent Catalog to accelerate development with proven patterns and best practices for common scenarios.

**Prerequisites**: 
- Azure AI Foundry project access
- Understanding of agent configuration

**Step-by-Step Guide**:

**Step 1: Explore Agent Catalog (10 minutes)**
1. Navigate to Azure AI Foundry → Your project → "Agents"
2. Click "Catalog" at the top of the screen
3. Browse available templates:
   - **Browser Automation Agent**: For web-based tasks
   - **Contract Analysis Agent**: Document processing and analysis
   - **Customer Service Agent**: Multi-agent support system
   - **Healthcare Agent Orchestrator**: Multi-disciplinary workflows
   - **Research Flow Agent**: Complex research workflows

**Step 2: Deploy and Customize Template (20 minutes)**
1. Select "Contract Analysis Agent" template
2. Click "Open in GitHub" to review the template structure
3. Create new agent based on template:
   - **Name**: MigrationContractAnalysisAgent
   - **Description**: "Analyze migration contracts and service agreements"
   - **Instructions**: Adapt template for migration-specific contract analysis:
   ```
   You are a migration contract analysis specialist. Your role is to:
   1. Review migration service agreements and contracts
   2. Extract key terms, conditions, and obligations
   3. Identify potential risks and liabilities
   4. Compare contract versions and highlight differences
   5. Generate compliance reports and recommendations
   
   Focus on migration-specific terms like SLAs, data handling, security requirements, and liability provisions.
   ```

**Step 3: Configure Tools and Test**
1. Add File Search tool for contract document analysis
2. Configure OpenAPI tool for compliance database integration
3. Test with sample migration contract or service agreement

**Documentation Reference**: [Agent Catalog Documentation](https://learn.microsoft.com/en-us/azure/ai-foundry/agents/concepts/agent-catalog)

### Walkthrough 2.3: Bing Custom Search Integration (30 minutes)

**Summary**: Configure Bing Custom Search for domain-specific migration knowledge retrieval, allowing agents to search within configurable sets of public web domains relevant to your migration scenarios.

**Prerequisites**: 
- Azure AI Foundry project
- Grounding with Bing Custom Search resource

**Step-by-Step Guide**:

**Step 1: Create Bing Custom Search Resource (10 minutes)**
1. Navigate to Azure Portal → "Create resource"
2. Search for "Grounding with Bing Custom Search"
3. Configure:
   - **Resource name**: migration-custom-search
   - **Resource group**: Same as your AI Foundry project
   - **Location**: Same as your AI Foundry project
   - **Pricing tier**: Standard

**Step 2: Configure Search Domains (10 minutes)**
1. Navigate to your Bing Custom Search resource
2. Select "Resource Management" → "Configurations"
3. Click "Create a new configuration"
4. Configure migration-specific search domains:
   - **Configuration name**: migration-knowledge-search
   - **Allowed domains**:
     - `https://docs.microsoft.com/azure/migrate/`
     - `https://azure.microsoft.com/migration/`
     - `https://docs.microsoft.com/azure/architecture/`
     - `https://azure.microsoft.com/case-studies/`
   - **Include subpages**: Yes
   - **Ranking**: Default

**Step 3: Integrate with Agent (10 minutes)**
1. Navigate to Azure AI Foundry → Your project → "Agents"
2. Select your MigrationOrchestratorAgent
3. Scroll to "Knowledge" section → "Add"
4. Select "Grounding with Bing Custom Search"
5. Configure:
   - **Connection**: Select your Bing Custom Search resource
   - **Configuration**: migration-knowledge-search
6. Test integration with query: "Search for the latest Azure migration best practices and tools for enterprise workloads, focusing on database migration strategies."

**Documentation Reference**: [Bing Custom Search Documentation](https://learn.microsoft.com/en-us/azure/ai-foundry/agents/how-to/tools/bing-custom-search)

### Walkthrough 2.4: OpenAPI Tool Integration (45 minutes)
###TODO

**Summary**: Enhance an existing Azure AI Foundry agent by adding OpenAPI tool integration to connect with external APIs. This walkthrough demonstrates how to extend your InfrastructureAssessmentAgent from Walkthrough 2.1 with external API capabilities using standardized OpenAPI 3.0 specifications.

**Prerequisites**: 
- Azure AI Foundry project with completed quickstart setup
- InfrastructureAssessmentAgent from Walkthrough 2.1 (or any existing agent)
- OpenAPI 3.0 specification with required `operationId` for each function

**Step-by-Step Guide**:

**Step 1: Prepare OpenAPI Specification (15 minutes)**
1. Create a simple migration cost calculator API specification:
   ```yaml
   openapi: 3.0.0
   info:
     title: Migration Cost Calculator API
     version: 1.0.0
     description: API for calculating Azure migration costs and recommendations
   
   servers:
     - url: https://jsonplaceholder.typicode.com
   
   paths:
     /posts:
       post:
         operationId: calculate_migration_cost
         summary: Calculate migration cost estimate
         description: Simulates cost calculation for infrastructure migration
         requestBody:
           required: true
           content:
             application/json:
               schema:
                 type: object
                 properties:
                   title:
                     type: string
                     description: Migration scenario name
                   body:
                     type: string
                     description: Infrastructure details for cost calculation
                   userId:
                     type: integer
                     description: User identifier
         responses:
           '201':
             description: Cost calculation completed
             content:
               application/json:
                 schema:
                   type: object
                   properties:
                     id: {type: integer}
                     title: {type: string}
                     body: {type: string}
                     userId: {type: integer}
   ```
   
   > **Note**: This example uses JSONPlaceholder (a free testing API) to demonstrate the integration. In a real scenario, you would use your actual migration API with proper authentication.

**Step 2: Add OpenAPI Tool to Existing Agent (15 minutes)**
1. Navigate to [Azure AI Foundry portal](https://ai.azure.com/) and select your AI Project
2. Go to "Agents" section and select your **InfrastructureAssessmentAgent** from Walkthrough 2.1
3. Click "Edit" to modify the existing agent
4. Scroll down to the "Tools" section
5. Click "Add" → "OpenAPI Specified Tool"
6. Configure the OpenAPI tool:
   - **OpenAPI spec**: Upload or paste your YAML specification from Step 1
   - **Connection**: Leave blank for anonymous APIs (like JSONPlaceholder)
   - **Tool name**: `cost_calculator`
   - **Description**: "Calculate migration costs and provide estimates"
7. Click "Add tool" to save

**Step 3: Update Agent Instructions (10 minutes)**
1. In the same agent editing view, update the "Instructions" field to include the new capability:
   ```
   You are an infrastructure assessment specialist focused on analyzing legacy systems and mapping them to Azure services. Your capabilities include:
   
   1. Analyze infrastructure configurations and recommend Azure service mappings
   2. Assess resource requirements and performance considerations
   3. Calculate migration costs using the cost calculator tool
   4. Provide detailed technical recommendations with cost implications
   
   When analyzing infrastructure:
   - Always consider both technical feasibility and cost optimization
   - Use the cost calculator tool to provide realistic budget estimates
   - Include specific Azure service recommendations with SKU suggestions
   - Consider compliance, security, and performance requirements
   
   When using the cost calculator, format the infrastructure details clearly in the request body.
   ```

2. Click "Save" to update the agent

**Step 4: Test Enhanced Agent with OpenAPI Tool (5 minutes)**
1. Click "Try in playground" from your updated agent
2. Test the enhanced functionality with a comprehensive query:
   ```
   Analyze this infrastructure and provide a cost estimate:
   
   Infrastructure:
   - 3 Windows Server 2019 VMs (8 cores, 16GB RAM each)
   - 1 SQL Server 2017 database (4 cores, 32GB RAM, 1TB storage)
   - Load balancer and network configuration
   - Requirements: High availability, backup strategy, monitoring
   
   Please assess the infrastructure and calculate migration costs for this scenario.
   ```

3. Observe how the agent:
   - Provides infrastructure analysis (existing capability)
   - Calls the OpenAPI tool to calculate costs (new capability)
   - Synthesizes both results into comprehensive recommendations

4. Verify the agent successfully uses both its original assessment capabilities and the new cost calculation tool

**Alternative Authentication Methods (Optional)**
For APIs requiring authentication, you can set up:

1. **API Key Authentication**:
   - Go to Settings → Connected resources → + New connection
   - Select "Custom keys" and configure your API key
   - Reference the connection in your OpenAPI tool configuration

2. **Managed Identity Authentication**:
   - Enable system-assigned managed identity on your Azure AI Service
   - Grant permissions to your target API resource
   - Configure your OpenAPI spec for managed identity authentication

**Documentation Reference**: [OpenAPI Tool Documentation](https://learn.microsoft.com/en-us/azure/ai-foundry/agents/how-to/tools/openapi-spec)

### Walkthrough 2.5: Azure Function Calling with PowerShell Scripts (45 minutes)

**Summary**: Create Azure Functions that execute PowerShell scripts for infrastructure management and automation, then integrate them as callable tools for AI agents. This walkthrough demonstrates how to build serverless functions that can be invoked by agents to perform real infrastructure operations.

**Prerequisites**: 
- Azure AI Foundry project with agents configured
- Azure subscription with Functions service enabled
- Visual Studio Code with Azure Functions extension
- PowerShell execution policy configured

**Step-by-Step Guide**:

**Step 1: Create Azure Function App (10 minutes)**
1. Navigate to Azure Portal → "Create a resource" → "Function App"
2. Configure the Function App:
   - **Function App name**: `migration-powershell-functions`
   - **Runtime stack**: PowerShell Core
   - **Version**: 7.4
   - **Region**: Same as your AI Foundry project
   - **Operating System**: Windows
   - **Plan type**: Consumption (Serverless)
3. Click "Review + create" → "Create"
4. Wait for deployment to complete

**Step 2: Create PowerShell Function for Infrastructure Assessment (15 minutes)**
1. Open Visual Studio Enterprise
2. Install Azure Functions extension if not already installed
3. Create new Azure Functions project:
   - Go to File → New → Project
   - Select "Azure Functions" template under Visual C# → Cloud
   - Choose PowerShell as runtime
   - Select HTTP trigger template
   - Function name: `Get-InfrastructureStatus`
4. Replace the default function code with migration-specific PowerShell:

```powershell
using namespace System.Net

param($Request, $TriggerMetadata)

# Parse input parameters
$ServerName = $Request.Query.ServerName
$CheckType = $Request.Query.CheckType

if (-not $ServerName) {
    Push-OutputBinding -Name Response -Value ([HttpResponseContext]@{
        StatusCode = [HttpStatusCode]::BadRequest
        Body = "ServerName parameter is required"
    })
    return
}

# Migration infrastructure assessment logic
$assessmentResult = @{
    ServerName = $ServerName
    Timestamp = Get-Date -Format "yyyy-MM-dd HH:mm:ss"
    CheckType = $CheckType
}

switch ($CheckType) {
    "connectivity" {
        # Simulate connectivity check
        $assessmentResult.Status = "Online"
        $assessmentResult.ResponseTime = "12ms"
        $assessmentResult.Details = "Server is reachable and responding"
    }
    "resources" {
        # Simulate resource assessment
        $assessmentResult.CPU = "65%"
        $assessmentResult.Memory = "8.2GB/16GB"
        $assessmentResult.Disk = "250GB/500GB"
        $assessmentResult.Details = "Resources within normal parameters"
    }
    "compatibility" {
        # Simulate compatibility check
        $assessmentResult.OSVersion = "Windows Server 2019"
        $assessmentResult.NetFramework = "4.8"
        $assessmentResult.AzureCompatible = $true
        $assessmentResult.Details = "Compatible with Azure migration"
    }
    default {
        # General health check
        $assessmentResult.OverallHealth = "Good"
        $assessmentResult.MigrationReady = $true
        $assessmentResult.Details = "Server ready for migration assessment"
    }
}

# Return structured response
Push-OutputBinding -Name Response -Value ([HttpResponseContext]@{
    StatusCode = [HttpStatusCode]::OK
    Body = ($assessmentResult | ConvertTo-Json -Depth 10)
    Headers = @{
        "Content-Type" = "application/json"
    }
})
```

**Step 3: Deploy Function to Azure (10 minutes)**
1. In Visual Studio Enterprise, right-click on your Azure Functions project in Solution Explorer
2. Select "Publish..." from the context menu
3. Choose "Azure" as the publish target → "Azure Function App (Windows)"
4. Select your subscription and the function app created in Step 1
5. Click "Publish" to start deployment
6. Wait for deployment to complete (status shown in Output window)
7. Test the function:
   - Go to Azure Portal → Your Function App → Functions → `Get-InfrastructureStatus`
   - Click "Code + Test" tab in the function view
   - Click "Test/Run" button at the top
   - Add query parameters: `ServerName=PROD-SQL01&CheckType=resources`
   - Click "Run" and verify JSON response

**Step 4: Create OpenAPI Specification for the Function (5 minutes)**
Create an OpenAPI spec that describes your PowerShell function:

```yaml
openapi: 3.0.0
info:
   title: "Migration PowerShell Functions API"
   version: "1.0.0"
   description: "Azure Functions executing PowerShell scripts for infrastructure management and migration assessment"

servers:
   - url: "https://migration-powershell-functions.azurewebsites.net"

security:
   - functionKey: []

paths:
   "/api/Get-InfrastructureStatus":
      get:
         operationId: "assess_infrastructure_status"
         summary: "Assess server infrastructure status"
         description: "Execute PowerShell script to check server connectivity, resources, or Azure migration compatibility"
         parameters:
            - name: "ServerName"
               in: "query"
               required: true
               schema:
                  type: "string"
               description: "Name or IP address of the server to assess"
            - name: "CheckType"
               in: "query"
               required: false
               schema:
                  type: "string"
                  enum: ["connectivity", "resources", "compatibility", "general"]
                  default: "general"
               description: "Type of infrastructure check to perform"
         responses:
            "200":
               description: "Infrastructure assessment completed successfully"
               content:
                  "application/json":
                     schema:
                        type: "object"
                        properties:
                           ServerName:
                              type: "string"
                              description: "Name of the assessed server"
                           Timestamp:
                              type: "string"
                              format: "date-time"
                              description: "When the assessment was performed"
                           CheckType:
                              type: "string"
                              description: "Type of check that was performed"
                           Status:
                              type: "string"
                              description: "Overall status of the server"
                           Details:
                              type: "string"
                              description: "Detailed assessment information"
                           # Additional properties based on CheckType
                           ResponseTime:
                              type: "string"
                              description: "Server response time (connectivity check)"
                           CPU:
                              type: "string"
                              description: "CPU utilization percentage (resources check)"
                           Memory:
                              type: "string"
                              description: "Memory usage information (resources check)"
                           Disk:
                              type: "string"
                              description: "Disk space information (resources check)"
                           OSVersion:
                              type: "string"
                              description: "Operating system version (compatibility check)"
                           NetFramework:
                              type: "string"
                              description: ".NET Framework version (compatibility check)"
                           AzureCompatible:
                              type: "boolean"
                              description: "Azure migration compatibility status"
                           OverallHealth:
                              type: "string"
                              description: "Overall server health status (general check)"
                           MigrationReady:
                              type: "boolean"
                              description: "Migration readiness status (general check)"
                        required:
                           - ServerName
                           - Timestamp
                           - CheckType
                           - Status
                           - Details
            "400":
               description: "Bad request - missing or invalid parameters"
               content:
                  "application/json":
                     schema:
                        type: "object"
                        properties:
                           error:
                              type: "string"
                              description: "Error message describing the issue"
            "500":
               description: "Internal server error during PowerShell execution"
               content:
                  "application/json":
                     schema:
                        type: "object"
                        properties:
                           error:
                              type: "string"
                              description: "Error message from the server"

components:
   securitySchemes:
      functionKey:
         type: "apiKey"
         in: "header"
         name: "x-functions-key"
         description: "Azure Functions host key for authentication"
```


**Step 5: Integrate Function with AI Agent (5 minutes)**
1. Navigate to Azure AI Foundry → Your project → "Agents"
2. Select your **InfrastructureAssessmentAgent** or create a new agent
3. In the agent configuration, scroll to "Tools" section
4. Click "Add" → "OpenAPI Specified Tool"
5. Configure the PowerShell Function tool:
   - **OpenAPI spec**: Paste the YAML specification from Step 4
   - **Connection**: Leave blank (use Function App's public endpoint)
   - **Tool name**: `infrastructure_assessor`
   - **Description**: "Execute PowerShell scripts to assess server infrastructure"
6. Update agent instructions to include the new capability:

```
You are an infrastructure assessment specialist. You can:

1. Analyze infrastructure configurations and recommend Azure service mappings
2. Execute real-time PowerShell-based infrastructure assessments using the infrastructure_assessor tool
3. Provide detailed technical recommendations based on live server data

When assessing infrastructure:
- Use the infrastructure_assessor tool to get real-time server status
- Specify appropriate CheckType based on assessment needs:
  - connectivity: Check if server is reachable
  - resources: Get CPU, memory, and disk usage
  - compatibility: Verify Azure migration compatibility
  - general: Overall health assessment

Always provide actionable recommendations based on the PowerShell assessment results.
```

**Step 6: Test Complete Integration**
1. In the agent playground, test the PowerShell integration:
   ```
   Please assess the infrastructure status of server PROD-SQL01. 
   I need to know about its resource utilization and Azure migration compatibility.
   ```

2. Verify the agent:
   - Calls the PowerShell function via the infrastructure_assessor tool
   - Receives structured JSON response with server details
   - Provides intelligent analysis based on the PowerShell results
   - Offers migration recommendations using real server data

**Advanced PowerShell Scenarios (Optional)**
You can extend this pattern for other migration tasks:

- **Database Assessment**: PowerShell scripts to check SQL Server compatibility
- **Application Discovery**: Scripts to inventory installed applications
- **Network Configuration**: Scripts to assess network requirements
- **Security Compliance**: Scripts to check security policies and configurations

**Security Considerations**:
- Configure Function App authentication for production use
- Use Azure Key Vault for storing sensitive credentials
- Implement proper error handling and logging
- Restrict Function App network access as needed

**Documentation Reference**: [Function Calling with Azure Functions](https://learn.microsoft.com/en-us/azure/ai-foundry/agents/how-to/tools/function-calling?pivots=csharp)

## 📝 Deliverables

After completing Day 2 tutorial walkthroughs, you should have:

- [ ] **Connected Multi-Agent System**: Main orchestrator with specialized connected agents for migration planning
- [ ] **Agent Catalog Implementation**: Customized agent template adapted for migration contract analysis
- [ ] **Custom Search Configuration**: Domain-specific Bing Custom Search for migration knowledge retrieval
- [ ] **OpenAPI Tool Integration**: External API connectivity with secure authentication
- [ ] **Azure Function PowerShell Integration**: Serverless functions executing PowerShell scripts as agent tools

## 🚀 Next Steps

After completing Day 2 tutorials, you'll move to Day 3 where you'll implement migration automation using AI Search, Semantic Kernel, and orchestration patterns.

## 📚 Additional Resources

### Microsoft Learn Documentation
- [Connected Agents How-to Guide](https://learn.microsoft.com/en-us/azure/ai-foundry/agents/how-to/connected-agents?pivots=portal)
- [Agent Catalog Overview](https://learn.microsoft.com/en-us/azure/ai-foundry/agents/concepts/agent-catalog)
- [Bing Custom Search Integration](https://learn.microsoft.com/en-us/azure/ai-foundry/agents/how-to/tools/bing-custom-search)
- [OpenAPI Tool Integration](https://learn.microsoft.com/en-us/azure/ai-foundry/agents/how-to/tools/openapi-spec)
- [Function Calling with Azure Functions](https://learn.microsoft.com/en-us/azure/ai-foundry/agents/how-to/tools/function-calling?pivots=csharp)

### GitHub Resources
- [Agent Catalog Templates](https://github.com/Azure/ai-foundry-agent-catalog)
- [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)

## ❓ Troubleshooting

### Common Issues and Solutions

**Connected Agents Not Routing Correctly**:
- Verify agent descriptions are clear and specific
- Check that connected agent names are descriptive
- Ensure main agent instructions include routing logic
- Test with simple, focused queries first

**Bing Custom Search No Results**:
- Verify domains are publicly accessible and indexed by Bing
- Check configuration includes subpages if needed
- Confirm search terms match indexed content
- Review domain spelling and URL format

**OpenAPI Tool Authentication Failures**:
- Verify API key is correct and not expired
- Check security scheme configuration matches API requirements
- Ensure connection is properly configured in Azure AI Foundry
- Test API endpoint independently first

### Getting Help

1. **Review Documentation**: Check the Microsoft Learn links above for detailed guidance
2. **Check Prerequisites**: Ensure all required resources are properly deployed
3. **Test Incrementally**: Start with simple configurations before adding complexity
4. **Monitor Logs**: Use Azure AI Foundry monitoring to track agent performance
5. **Community Support**: Visit Microsoft Tech Community for additional assistance

## 🔧 Tips for Success

### Best Practices
- **Start Simple**: Begin with basic agent configurations before adding advanced features
- **Test Thoroughly**: Validate each component before integrating with others
- **Document Configuration**: Keep track of connection strings, API keys, and configurations
- **Monitor Performance**: Use Azure AI Foundry monitoring to track agent effectiveness
- **Iterate Based on Results**: Refine instructions and configurations based on testing

### Performance Optimization
- **Clear Instructions**: Write specific, actionable instructions for each agent
- **Efficient Routing**: Design clear routing logic for connected agents
- **Appropriate Tools**: Match tools to specific use cases and requirements
- **Resource Management**: Monitor token usage and API costs
- **Error Handling**: Implement proper error handling and fallback mechanisms
