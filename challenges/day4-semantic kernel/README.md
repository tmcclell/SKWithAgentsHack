# Day 3: Migration Automation with AI Search & Semantic Kernel

## 🎯 Learning Objectives

By the end of Day 3, you will:
- Configure Azure AI Search using Azure Portal with sample documents
- Implement Semantic Kernel for AI orchestration in C# applications
- Connect to existing Azure AI Foundry agents using Semantic Kernel
- Build group chat orchestration with connected agents
- Create progressive automation workflows that build upon each other

## 📚 Key Concepts

### AI Search Integration
- **Azure AI Search Overview**: Intelligent search service for migration data
  - Semantic search capabilities with vector embeddings
  - Portal-based configuration for rapid prototyping
  - Integration with Azure AI services for content enrichment
  - Scalable indexing and querying for migration documentation

### Semantic Kernel Architecture
- **SK Framework Overview**: Microsoft's enterprise AI orchestration platform
  - Plugin-based architecture for extensible AI capabilities
  - Built-in connectors for Azure OpenAI and Azure AI Foundry
  - Memory management and conversation context handling
  - Cross-platform support (.NET, Python, Java)

### Group Chat Orchestration
- **Multi-Agent Coordination**: Orchestrating multiple AI agents
  - Round-robin conversation management
  - Agent specialization and role-based interactions
  - Dynamic workflow routing and decision making
  - State management across distributed conversations

## 🏗️ Tutorial Walkthroughs

### Walkthrough 3.1: AI Search Using Azure Portal (45 minutes)

**Summary**: Create an Azure AI Search service and index using the Azure Portal with sample migration documents. This walkthrough demonstrates the portal-based approach to setting up intelligent search for migration knowledge bases.

**Prerequisites**: 
- Azure subscription with contributor access
- Azure AI Foundry project (optional, for agent integration)

**Step-by-Step Guide**:

**Step 1: Create Azure AI Search Service via Portal (10 minutes)**
1. Navigate to [Azure Portal](https://portal.azure.com)
2. Click "Create a resource" → Search for "Azure AI Search"
3. Configure the service:
   - **Service name**: `migration-search-demo`
   - **Resource group**: Use existing or create new
   - **Location**: East US 2
   - **Pricing tier**: Free (for demo) or Basic
4. Click "Review + Create" → "Create"
5. Wait for deployment to complete

**Step 2: Create Search Index with Sample Data (20 minutes)**
1. Navigate to your Azure AI Search service in the portal
2. Click "Add index" → "Using sample data"
3. Select "Sample Migration Documents" or create custom sample:
   - **Data source**: Choose "Upload JSON documents"
   - **Index name**: `migration-knowledge-base`
   - **Key field**: `id`

4. Create sample migration documents (save as `sample-migration-docs.json`):
   ```json
   [
     {
       "id": "doc1",
       "title": "Azure VM Migration Guide",
       "content": "Complete guide for migrating on-premises virtual machines to Azure. This includes pre-migration assessment using Azure Migrate, sizing recommendations based on performance data, and step-by-step migration process. Key considerations include network configuration, storage requirements, and security group settings.",
       "category": "Compute",
       "migrationPhase": "Assessment",
       "complexity": "Medium",
       "estimatedHours": 24
     },
     {
       "id": "doc2",
       "title": "SQL Server Database Migration",
       "content": "Best practices for migrating SQL Server databases to Azure SQL Database or Azure SQL Managed Instance. Covers database compatibility assessment, performance optimization strategies, security considerations, and minimal downtime migration techniques using Azure Database Migration Service.",
       "category": "Database",
       "migrationPhase": "Migration",
       "complexity": "High",
       "estimatedHours": 40
     },
     {
       "id": "doc3",
       "title": "Azure App Service Migration",
       "content": "Migrating web applications to Azure App Service. Includes code analysis, configuration management, custom domain setup, SSL certificate configuration, and scaling strategies. Covers both .NET and Java applications with Docker container support.",
       "category": "WebApp",
       "migrationPhase": "Deployment",
       "complexity": "Low",
       "estimatedHours": 16
     }
   ]
   ```

5. Upload the JSON file using the portal's import wizard
6. Configure index fields:
   - **id**: Key field, retrievable
   - **title**: Searchable, retrievable
   - **content**: Searchable, retrievable
   - **category**: Searchable, filterable, facetable
   - **migrationPhase**: Filterable, facetable
   - **complexity**: Filterable, facetable
   - **estimatedHours**: Filterable, sortable

**Step 3: Test Search Functionality (15 minutes)**
1. Navigate to "Search explorer" in your Azure AI Search service
2. Test basic search queries:
   - Search: `"SQL Server"` (should return database migration doc)
   - Search: `"virtual machine"` (should return VM migration doc)
   - Search: `category:Database` (filtered search)
   - Search: `migrationPhase:Assessment` (phase-specific search)

3. Test semantic search (if available in your tier):
   - Enable semantic search in Index configuration
   - Test natural language queries: `"How to migrate databases with minimal downtime?"`

4. Verify search results include:
   - Document titles and content excerpts
   - Relevance scoring
   - Faceted navigation results

**Documentation Reference**: [Azure AI Search Portal Guide](https://learn.microsoft.com/en-us/azure/search/search-get-started-portal)

// ...existing code...

### Walkthrough 3.2: Semantic Kernel Setup and Azure AI Agent Connection (45 minutes)

**Summary**: Build a comprehensive Semantic Kernel application that connects to your existing Azure AI Foundry agents and demonstrates advanced orchestration patterns. This progressive tutorial builds upon each key topic, allowing you to master Semantic Kernel fundamentals before advancing to complex scenarios like group chat orchestration and multi-tool integration.

**Prerequisites**: 
- Completed Day 1: Azure AI Foundry setup with deployed agents
- Completed Day 2: OpenAPI tools, Bing Custom Search, and file search configurations
- .NET 8.0 SDK installed
- Visual Studio or VS Code with C# extension

**Learning Path**: This walkthrough is designed as a progressive experience where each step builds upon the previous one. Complete each section fully and test your implementation before proceeding to the next step.

**Step-by-Step Guide**:

**Step 1: Foundation - Initialize Semantic Kernel (10 minutes)**

**Objective**: Learn to properly initialize the Semantic Kernel framework and understand its core architecture.

1. **Create New Console Application**:
```bash
dotnet new console -n MigrationOrchestrator
cd MigrationOrchestrator
dotnet add package Microsoft.SemanticKernel
dotnet add package Microsoft.SemanticKernel.Agents.AzureAI
dotnet add package Microsoft.Extensions.Configuration
dotnet add package Microsoft.Extensions.Configuration.Json
```

2. **Configure Application Settings**:
Create `appsettings.json`:
```json
{
  "AzureOpenAI": {
    "Endpoint": "https://your-openai-resource.openai.azure.com/",
    "ApiKey": "your-openai-key",
    "DeploymentName": "gpt-4-migration-agent"
  }
}
```

3. **Initialize Basic Kernel**:
Create `Program.cs`:
```csharp
using Microsoft.Extensions.Configuration;
using Microsoft.SemanticKernel;

class Program
{
    static async Task Main(string[] args)
    {
        Console.WriteLine("🚀 Step 1: Initializing Semantic Kernel...");
        
        // Load configuration
        var configuration = new ConfigurationBuilder()
            .AddJsonFile("appsettings.json")
            .Build();

        // Initialize Semantic Kernel
        var kernel = CreateKernel(configuration);
        
        Console.WriteLine("✅ Semantic Kernel initialized successfully!");
        Console.WriteLine("🎯 Key Learning: The kernel is your main orchestration hub for AI operations");
        
        // Test basic functionality
        await TestBasicKernel(kernel);
    }

    private static Kernel CreateKernel(IConfiguration configuration)
    {
        var builder = Kernel.CreateBuilder();
        
        builder.AddAzureOpenAIChatCompletion(
            configuration["AzureOpenAI:DeploymentName"]!,
            configuration["AzureOpenAI:Endpoint"]!,
            configuration["AzureOpenAI:ApiKey"]!);

        return builder.Build();
    }
    
    private static async Task TestBasicKernel(Kernel kernel)
    {
        Console.WriteLine("\n💬 Testing basic kernel functionality...");
        
        var result = await kernel.InvokePromptAsync("What are the key steps in Azure migration planning?");
        
        Console.WriteLine($"Response: {result}");
        Console.WriteLine("\n🎉 Step 1 Complete! Build and run to verify before proceeding to Step 2.");
    }
}
```dot

**Build and Test**: Run `dotnet run` to verify the kernel initializes correctly before proceeding.

**Step 2: Azure AI Agent Connection (10 minutes)**

**Objective**: Connect to your existing Azure AI Foundry agent from Day 1 and understand agent lifecycle management.

1. **Add Azure AI Agent Configuration**:
Update `appsettings.json`:
```json
{
  "AzureOpenAI": {
    "Endpoint": "https://your-openai-resource.openai.azure.com/",
    "ApiKey": "your-openai-key",
    "DeploymentName": "gpt-4-migration-agent"
  },
  "AzureAI": {
    "Endpoint": "https://your-ai-foundry-project.cognitiveservices.azure.com/",
    "ApiKey": "your-api-key",
    "AgentId": "your-migration-agent-id-from-day1"
  }
}
```

2. **Update Program.cs to Include Agent Connection**:
```csharp
using Microsoft.Extensions.Configuration;
using Microsoft.SemanticKernel;
using Microsoft.SemanticKernel.Agents.AzureAI;

// Update Main method
static async Task Main(string[] args)
{
    Console.WriteLine("🚀 Step 2: Connecting to Azure AI Agent...");
    
    var configuration = new ConfigurationBuilder()
        .AddJsonFile("appsettings.json")
        .Build();

    var kernel = CreateKernel(configuration);
    
    // Connect to existing Azure AI Agent from Day 1
    var azureAIAgent = await CreateAzureAIAgent(configuration);
    
    Console.WriteLine($"✅ Connected to agent: {azureAIAgent.Id}");
    Console.WriteLine("🎯 Key Learning: Azure AI Agents provide specialized, pre-trained capabilities");
    
    await TestAgentConnection(azureAIAgent);
}

private static async Task<AzureAIAgent> CreateAzureAIAgent(IConfiguration configuration)
{
    var agent = await AzureAIAgent.RetrieveAsync(
        kernelArguments: new KernelArguments(),
        apiKey: configuration["AzureAI:ApiKey"]!,
        endpoint: new Uri(configuration["AzureAI:Endpoint"]!),
        agentId: configuration["AzureAI:AgentId"]!);

    return agent;
}

private static async Task TestAgentConnection(AzureAIAgent agent)
{
    Console.WriteLine("\n💬 Testing agent connection...");
    
    var thread = await agent.NewThreadAsync();
    var response = await agent.InvokeAsync(thread, "Provide a brief overview of your migration capabilities");
    
    Console.WriteLine($"Agent Response: {response.FirstOrDefault()?.Content}");
    Console.WriteLine("\n🎉 Step 2 Complete! Build and run to verify agent connection before proceeding.");
}
```

**Build and Test**: Run `dotnet run` to verify the agent connection works before proceeding.

**Step 3: Streaming Responses (10 minutes)**

**Objective**: Implement real-time streaming responses for better user experience during long-running operations.

1. **Add Streaming Functionality**:
Update your `Main` method and add streaming support:
```csharp
// Update Main method to include streaming
static async Task Main(string[] args)
{
    Console.WriteLine("🚀 Step 3: Implementing Streaming Responses...");
    
    var configuration = new ConfigurationBuilder()
        .AddJsonFile("appsettings.json")
        .Build();

    var kernel = CreateKernel(configuration);
    var azureAIAgent = await CreateAzureAIAgent(configuration);
    
    Console.WriteLine("🎯 Key Learning: Streaming provides real-time feedback for complex operations");
    
    // Demonstrate streaming response
    await DemonstrateStreamingResponse(azureAIAgent);
}

private static async Task DemonstrateStreamingResponse(AzureAIAgent agent)
{
    Console.WriteLine("\n💬 Starting streaming conversation with migration agent...");
    Console.WriteLine("Query: Analyze this environment for Azure migration: 3 Windows Server 2019 VMs, SQL Server 2017 database (200GB), legacy .NET Framework applications\n");
    Console.WriteLine("Response (streaming):");
    
    var thread = await agent.NewThreadAsync();
    
    await foreach (var message in agent.InvokeStreamingAsync(
        thread, 
        "Analyze this environment for Azure migration: 3 Windows Server 2019 VMs, SQL Server 2017 database (200GB), legacy .NET Framework applications"))
    {
        Console.Write(message.Content);
    }
    
    Console.WriteLine("\n\n✅ Streaming response completed.");
    Console.WriteLine("🎉 Step 3 Complete! Build and run to see streaming in action before proceeding.");
}
```

**Build and Test**: Run `dotnet run` to see streaming responses in action before proceeding.
**Step 4: Tool Integration - OpenAPI Integration (5 minutes)**

**Objective**: Integrate the OpenAPI tools created in Day 2 to extend agent capabilities with external services.

1. **Add OpenAPI Package and Integration**:
```bash
dotnet add package Microsoft.SemanticKernel.Plugins.OpenApi
```

2. **Update Program.cs to Include OpenAPI Integration**:
```csharp
// Add this method to your Program class
private static async Task<Kernel> AddOpenApiIntegration(Kernel kernel, IConfiguration configuration)
{
    Console.WriteLine("🔌 Adding OpenAPI integration from Day 2...");
    
    // Use the cost calculator API from Day 2
    var openApiSpec = """
    {
      "openapi": "3.0.1",
      "info": {
        "title": "Migration Cost Calculator",
        "version": "1.0"
      },
      "servers": [
        {"url": "https://jsonplaceholder.typicode.com"}
      ],
      "paths": {
        "/posts": {
          "post": {
            "operationId": "calculate_migration_cost",
            "summary": "Calculate migration cost estimate",
            "requestBody": {
              "required": true,
              "content": {
                "application/json": {
                  "schema": {
                    "type": "object",
                    "properties": {
                      "title": {"type": "string"},
                      "body": {"type": "string"},
                      "userId": {"type": "integer"}
                    }
                  }
                }
              }
            }
          }
        }
      }
    }
    """;

    await kernel.ImportPluginFromOpenApiAsync(
        "CostCalculator",
        new StringReader(openApiSpec));

    Console.WriteLine("✅ OpenAPI Cost Calculator plugin loaded");
    Console.WriteLine("🎯 Key Learning: OpenAPI integration extends AI capabilities with external services");
    return kernel;
}
```

**Build and Test**: Update your Main method to call `AddOpenApiIntegration(kernel, configuration)` and verify the plugin loads successfully.

**Step 5: Tool Integration - Azure AI Search Integration (5 minutes)**

**Objective**: Connect to the Azure AI Search service created in Walkthrough 3.1 for intelligent knowledge retrieval.

1. **Add Azure AI Search Integration**:
```csharp
using Microsoft.SemanticKernel.Plugins.Core;

// Add this method to your Program class  
private static Kernel AddAzureSearchIntegration(Kernel kernel, IConfiguration configuration)
{
    Console.WriteLine("🔍 Adding Azure AI Search integration...");
    
    kernel.ImportPluginFromType<AzureSearchPlugin>();
    Console.WriteLine("✅ Azure AI Search plugin loaded");
    Console.WriteLine("🎯 Key Learning: AI Search provides intelligent document retrieval capabilities");
    return kernel;
}

// Create AzureSearchPlugin class
public class AzureSearchPlugin
{
    [KernelFunction, Description("Search migration knowledge base using Azure AI Search")]
    public async Task<string> SearchMigrationDocs(
        [Description("The search query")] string query)
    {
        // This would integrate with your Azure AI Search service from Walkthrough 3.1
        // For demo purposes, return simulated results
        return $"Found migration documentation for '{query}': Best practices include assessment, planning, and phased migration approach with rollback procedures.";
    }
}
```

**Build and Test**: Update your Main method to call `AddAzureSearchIntegration(kernel, configuration)` and verify the search plugin works.

**Step 6: Tool Integration - File Search and Bing Grounding (5 minutes)**

**Objective**: Add file search capabilities and Bing Custom Search for comprehensive information retrieval.

1. **Add File Search and Bing Integration**:
```csharp
// Add these methods to your Program class
private static Kernel AddFileSearchIntegration(Kernel kernel)
{
    Console.WriteLine("📁 Adding File Search integration...");
    kernel.ImportPluginFromType<FileSearchPlugin>();
    Console.WriteLine("✅ File Search plugin loaded");
    return kernel;
}

private static Kernel AddBingSearchIntegration(Kernel kernel, IConfiguration configuration)
{
    Console.WriteLine("🌐 Adding Bing Custom Search integration...");
    kernel.ImportPluginFromType<BingSearchPlugin>();
    Console.WriteLine("✅ Bing Custom Search plugin loaded");
    Console.WriteLine("🎯 Key Learning: Multiple search sources provide comprehensive knowledge coverage");
    return kernel;
}

public class FileSearchPlugin
{
    [KernelFunction, Description("Search migration knowledge base files")]
    public async Task<string> SearchKnowledgeBase(
        [Description("The search term")] string searchTerm)
    {
        // This would integrate with your vector store from Day 1
        return $"Knowledge base results for '{searchTerm}': Found 3 relevant documents about Azure migration best practices and common pitfalls.";
    }
}

public class BingSearchPlugin
{
    [KernelFunction, Description("Search for current migration documentation and best practices using Bing")]
    public async Task<string> SearchMigrationDocs(
        [Description("The search query")] string query)
    {
        // This would integrate with your Bing Custom Search configuration from Day 2
        return $"Bing search results for '{query}': Latest Microsoft documentation on Azure migration tools and strategies.";
    }
}
```

**Build and Test**: Update your Main method to include these integrations and verify all tools load correctly.

**Step 7: Group Chat Orchestration (10 minutes)**

**Objective**: Implement multi-agent group chat orchestration to simulate collaborative planning between specialized agents.

1. **Add Group Chat Dependencies**:
```csharp
using Microsoft.SemanticKernel.Agents;
using Microsoft.SemanticKernel.Agents.Chat;
using Microsoft.SemanticKernel.ChatCompletion;
```

2. **Create Specialized Agents for Group Chat**:
```csharp
// Add this method to your Program class
private static async Task DemonstrateGroupChat(IConfiguration configuration)
{
    Console.WriteLine("\n🤖 Step 7: Initializing Group Chat with Migration Specialists...");
    Console.WriteLine("🎯 Key Learning: Group chat enables collaborative AI problem-solving");
    
    var kernel = CreateKernel(configuration);
    
    // Create Assessment Agent
    var assessmentAgent = new ChatCompletionAgent()
    {
        Name = "AssessmentSpecialist",
        Instructions = """
            You are an infrastructure assessment specialist. Your role is to:
            1. Analyze current infrastructure configurations
            2. Identify dependencies and constraints  
            3. Assess migration readiness and complexity
            4. Provide technical feasibility analysis
            Keep responses concise but detailed. Focus on technical accuracy.
            """,
        Kernel = kernel,
        Arguments = new KernelArguments(new OpenAIPromptExecutionSettings() { MaxTokens = 800 })
    };

    // Create Planning Agent
    var planningAgent = new ChatCompletionAgent()
    {
        Name = "PlanningSpecialist", 
        Instructions = """
            You are a migration planning specialist. Your role is to:
            1. Create detailed migration plans based on assessments
            2. Define migration phases and timelines
            3. Identify required resources and dependencies
            4. Establish rollback and contingency plans
            Build upon the assessment specialist's analysis. Be practical and specific.
            """,
        Kernel = kernel,
        Arguments = new KernelArguments(new OpenAIPromptExecutionSettings() { MaxTokens = 800 })
    };

    // Create Cost Analysis Agent
    var costAgent = new ChatCompletionAgent()
    {
        Name = "CostAnalyst",
        Instructions = """
            You are a cost analysis specialist. Your role is to:
            1. Calculate migration costs and TCO analysis
            2. Compare different Azure service options
            3. Identify cost optimization opportunities
            4. Provide budget recommendations
            Base your analysis on the assessment and planning provided by other specialists.
            """,
        Kernel = kernel,
        Arguments = new KernelArguments(new OpenAIPromptExecutionSettings() { MaxTokens = 800 })
    };

    // Create group chat
    var chat = new AgentGroupChat(assessmentAgent, planningAgent, costAgent)
    {
        ExecutionSettings = new AgentGroupChatSettings
        {
            SelectionStrategy = new SequentialSelectionStrategy()
        }
    };

    // Start collaborative migration analysis
    await chat.AddChatMessageAsync(new ChatMessageContent(
        AuthorRole.User, 
        """
        Analyze this migration scenario collaboratively:
        
        Current Environment:
        - 3 Windows Server 2019 VMs (web servers)
        - SQL Server 2017 database (200GB)
        - .NET Framework 4.7 applications
        - Basic network setup
        
        Requirements:
        - Minimize downtime
        - Maintain performance  
        - Budget conscious approach
        
        Each specialist should provide their analysis in sequence.
        """));

    Console.WriteLine("💬 Group chat collaboration in progress...\n");

    // Process the collaborative discussion
    await foreach (var content in chat.InvokeAsync())
    {
        Console.WriteLine($"🤖 {content.AuthorName}:");
        Console.WriteLine($"{content.Content}");
        Console.WriteLine(new string('-', 60));
    }
    
    Console.WriteLine("✅ Group chat collaboration completed!");
}
```

**Build and Test**: Update your Main method to call `DemonstrateGroupChat(configuration)` and observe the collaborative planning process.

**Step 8: Complete Integration and Final Build (5 minutes)**

**Objective**: Integrate all components into a comprehensive migration orchestrator that demonstrates the full power of Semantic Kernel.

1. **Update Complete Main Method**:
```csharp
using Microsoft.Extensions.Configuration;
using Microsoft.SemanticKernel;
using Microsoft.SemanticKernel.Agents.AzureAI;
using Microsoft.SemanticKernel.Agents;
using Microsoft.SemanticKernel.Agents.Chat;
using Microsoft.SemanticKernel.ChatCompletion;
using Microsoft.SemanticKernel.Connectors.OpenAI;
using System.ComponentModel;

class Program
{
    static async Task Main(string[] args)
    {
        Console.WriteLine("🚀 Migration Orchestrator - Complete Semantic Kernel Demo");
        Console.WriteLine("========================================================\n");

        var configuration = new ConfigurationBuilder()
            .AddJsonFile("appsettings.json")
            .Build();

        try
        {
            // Progressive demonstration of each key topic
            Console.WriteLine("📚 Building upon each Semantic Kernel concept progressively...\n");

            // Foundation: Initialize kernel
            var kernel = CreateKernel(configuration);
            
            // Tool Integration: Add all tools from previous days
            kernel = await AddOpenApiIntegration(kernel, configuration);
            kernel = AddAzureSearchIntegration(kernel, configuration);
            kernel = AddFileSearchIntegration(kernel);
            kernel = AddBingSearchIntegration(kernel, configuration);

            // Agent Connection: Connect to Azure AI Foundry agent
            var azureAIAgent = await CreateAzureAIAgent(configuration);
            
            // Streaming: Demonstrate real-time responses with tools
            await DemonstrateStreamingWithTools(azureAIAgent, kernel);
            
            // Group Chat: Advanced orchestration
            await DemonstrateGroupChat(configuration);
            
            Console.WriteLine("\n🎉 Migration Orchestrator demo completed successfully!");
            Console.WriteLine("✅ All Semantic Kernel concepts demonstrated and integrated");
            
        }
        catch (Exception ex)
        {
            Console.WriteLine($"❌ Error: {ex.Message}");
            Console.WriteLine("🔧 Please check troubleshooting section below");
        }
    }

    // Include all the previous methods: CreateKernel, CreateAzureAIAgent, 
    // DemonstrateStreamingResponse, AddOpenApiIntegration, etc.
    
    private static async Task DemonstrateStreamingWithTools(AzureAIAgent agent, Kernel kernel)
    {
        Console.WriteLine("💡 Demonstrating agent with all integrated tools...\n");
        
        var thread = await agent.NewThreadAsync();
        
        Console.WriteLine("Query: Comprehensive migration analysis using all available tools");
        Console.WriteLine("Response (streaming with tool integration):\n");
        
        await foreach (var message in agent.InvokeStreamingAsync(
            thread,
            """
            Provide a comprehensive migration analysis using all available tools:
            1. Search knowledge base for similar cases
            2. Calculate cost estimates  
            3. Find current best practices documentation
            4. Provide technical assessment
            
            Environment: 3 web servers, 1 database server, legacy applications
            """))
        {
            Console.Write(message.Content);
        }
        
        Console.WriteLine("\n\n✅ Streaming with tools completed!");
    }
}
```

**Final Build and Test**: Run `dotnet run` to see the complete integrated experience.

**🔧 Troubleshooting and Common Issues**

**Issue 1: Agent Connection Fails**
- **Problem**: "Agent not found" or authentication errors
- **Solution**: Verify your Azure AI Foundry agent ID and API keys from Day 1
- **Check**: Ensure your agent is still deployed and accessible

**Issue 2: OpenAPI Integration Errors**
- **Problem**: "Plugin failed to load" errors
- **Solution**: Verify the OpenAPI specification format
- **Check**: Test the API endpoint independently first

**Issue 3: Streaming Responses Don't Appear**
- **Problem**: No streaming output visible
- **Solution**: Ensure console output is flushed: add `Console.Out.Flush()` after each write
- **Check**: Verify your Azure OpenAI deployment supports streaming

**Issue 4: Group Chat Agents Don't Respond**
- **Problem**: Agents return empty responses
- **Solution**: Check token limits and agent instructions
- **Check**: Ensure your Azure OpenAI deployment has sufficient quota

**Issue 5: Build Errors**
- **Problem**: Package version conflicts
- **Solution**: Use these specific versions:
```xml
<PackageReference Include="Microsoft.SemanticKernel" Version="1.0.1" />
<PackageReference Include="Microsoft.SemanticKernel.Agents.AzureAI" Version="1.0.1-alpha" />
```

**🎯 Key Learning Outcomes Achieved**

After completing this walkthrough, you have successfully:

1. **Mastered Semantic Kernel Foundation**: Understood kernel initialization and configuration
2. **Connected to Azure AI Agents**: Integrated existing AI Foundry agents into your application  
3. **Implemented Streaming Responses**: Created real-time user experiences for long operations
4. **Integrated Multiple Tools**: Combined OpenAPI, Azure AI Search, file search, and Bing grounding
5. **Built Group Chat Orchestration**: Created collaborative AI agent workflows
6. **Applied Progressive Learning**: Built each concept upon the previous one for comprehensive understanding

**🚀 Next Steps**

- Experiment with different agent personalities and specializations
- Integrate additional tools and APIs specific to your migration scenarios
- Explore more complex orchestration patterns using Semantic Kernel
- Deploy your orchestrator to Azure for production use

**Documentation References**:
- [Semantic Kernel Azure AI Agent](https://learn.microsoft.com/en-us/semantic-kernel/frameworks/agent/agent-types/azure-ai-agent?pivots=programming-language-csharp)
- [Semantic Kernel Group Chat Sample](https://github.com/microsoft/semantic-kernel/blob/main/dotnet/samples/GettingStartedWithAgents/Orchestration/Step03_GroupChat.cs)

// ...existing code...
