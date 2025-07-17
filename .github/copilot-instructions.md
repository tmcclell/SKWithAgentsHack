# GitHub Copilot Instructions for Semantic Kernel Azure AI Agents Project

## 🧠 Project Goal
Build a C# web application using the Semantic Kernel framework that connects to existing Azure AI Foundry agents. The app should expose a chat UI, support knowledge retrieval and action execution, leverage Semantic Kernel's group chat capabilities, include unit tests, and be deployable via `azd`.

---

## 🧱 Technology Stack & Integration Points

### Core Frameworks
- **Language**: C# (.NET 8+)
- **Framework**: Microsoft Semantic Kernel
- **Agent Integration**: Azure AI Foundry + AzureAIAgent SDK
- **Group Chat**: Semantic Kernel Group Chat API
- **UI**: Blazor Server or SignalR-based chat interface
- **Configuration**: .env file for secrets and keys
- **CI/CD**: Azure Developer CLI (`azd`)
- **Testing**: xUnit with test containers
- **Authentication**: Azure CLI credentials or Managed Identity

### Azure Services
- Azure AI Foundry (existing agents with knowledge and actions)
- Azure OpenAI Service (if needed for additional models)
- Azure App Service (deployment target)
- Azure Key Vault (production secrets)

---

## 🏗️ Project Structure

```
src/
├── SemanticKernelAgents.Web/          # Blazor/Web UI
├── SemanticKernelAgents.Core/         # Business logic and SK integration
├── SemanticKernelAgents.Agents/       # Azure AI Foundry agent wrappers
├── SemanticKernelAgents.Models/       # DTOs and models
└── SemanticKernelAgents.Tests/        # Unit tests
infra/                                 # Bicep/ARM templates for azd
.env                                   # Local development secrets
azure.yaml                           # azd configuration
appsettings.json                     # Application configuration
```

---

## 🔌 Agent Integration Patterns

### 1. Connect to Azure AI Foundry Agents
```csharp
using Microsoft.SemanticKernel;
using Microsoft.SemanticKernel.Agents.AzureAI;

// Load from .env file
var connectionString = Environment.GetEnvironmentVariable("AZURE_AI_FOUNDRY_CONNECTION_STRING");
var client = AzureAIAgent.CreateAzureAIClient(connectionString, new AzureCliCredential());
var agentsClient = client.GetAgentsClient();
var agent = new AzureAIAgent(agentDefinition, agentsClient);
```

### 2. Semantic Kernel Group Chat Setup
```csharp
using Microsoft.SemanticKernel.Agents;
using Microsoft.SemanticKernel.Agents.Chat;

var chatHistory = new ChatHistory();
var groupChat = new AgentGroupChat(agent1, agent2, agent3)
{
    ExecutionSettings = new()
    {
        TerminationStrategy = new KernelFunctionTerminationStrategy(terminationFunction, kernel)
    }
};
```

### 3. Knowledge Retrieval Integration
```csharp
// Integrate with existing agent's knowledge base
var knowledgeFunction = agent.AsKernelFunction("SearchKnowledge");
var result = await kernel.InvokeAsync(knowledgeFunction, new() { ["query"] = userQuery });
```

---

## 🎨 UI Development Guidelines

### Chat Interface Requirements
- Real-time messaging with SignalR
- Message history persistence
- File upload capabilities for knowledge queries
- Multi-agent conversation visualization
- Typing indicators and message status
- Responsive design for mobile/desktop

### Blazor Components Structure
```csharp
// ChatComponent.razor
@using Microsoft.SemanticKernel.Agents
@inject IAgentService AgentService
@inject IJSRuntime JSRuntime

<div class="chat-container">
    <ChatHistory Messages="@messages" />
    <MessageInput OnSendMessage="HandleSendMessage" />
</div>
```

---

## 🧪 Testing Strategy

### Unit Test Patterns
```csharp
[Fact]
public async Task Agent_Should_ProcessMessage_Successfully()
{
    // Arrange
    var mockAgent = new Mock<IAzureAIAgent>();
    var service = new AgentService(mockAgent.Object);
    
    // Act
    var result = await service.ProcessMessageAsync("test message");
    
    // Assert
    Assert.NotNull(result);
    mockAgent.Verify(x => x.InvokeAsync(It.IsAny<string>()), Times.Once);
}
```

### Integration Tests
- Test containers for Azure services
- Mock Azure AI Foundry responses
- End-to-end chat flow testing
- Group chat orchestration tests

---

## 📋 Environment Configuration

### .env File Structure
```env
# Azure AI Foundry
AZURE_AI_FOUNDRY_CONNECTION_STRING=your_connection_string_here
AZURE_AI_FOUNDRY_ENDPOINT=https://your-instance.cognitiveservices.azure.com/
AZURE_AI_FOUNDRY_API_KEY=your_api_key_here

# Azure OpenAI (if needed)
AZURE_OPENAI_ENDPOINT=https://your-openai.openai.azure.com/
AZURE_OPENAI_API_KEY=your_openai_key_here
AZURE_OPENAI_DEPLOYMENT_NAME=gpt-4

# Application Settings
ASPNETCORE_ENVIRONMENT=Development
AZURE_CLIENT_ID=your_client_id
AZURE_CLIENT_SECRET=your_client_secret
AZURE_TENANT_ID=your_tenant_id
```

### appsettings.json Configuration
```json
{
  "SemanticKernel": {
    "AgentSettings": {
      "MaxTokens": 4000,
      "Temperature": 0.7,
      "GroupChatSettings": {
        "MaxRounds": 10,
        "TimeoutMinutes": 5
      }
    }
  }
}
```

---

## 🚀 Development Workflow

### Common Commands
```bash
# Setup development environment
azd auth login
azd env new
azd up

# Run locally
dotnet run --project src/SemanticKernelAgents.Web

# Run tests
dotnet test

# Deploy to Azure
azd deploy
```

### Azure Developer CLI Configuration
```yaml
# azure.yaml
name: semantic-kernel-agents
metadata:
  template: semantic-kernel-agents@1.0.0
services:
  web:
    project: src/SemanticKernelAgents.Web
    language: csharp
    host: appservice
```

---

## 📝 Coding Standards & Patterns

### Dependency Injection Setup
```csharp
// Program.cs
builder.Services.AddSemanticKernel();
builder.Services.AddAzureAIAgents(builder.Configuration);
builder.Services.AddSignalR();
builder.Services.AddScoped<IAgentService, AgentService>();
builder.Services.AddScoped<IChatOrchestrator, ChatOrchestrator>();
```

### Error Handling
- Use structured logging with Serilog
- Implement retry policies for Azure service calls
- Graceful degradation for agent failures
- User-friendly error messages in chat UI

### Security Considerations
- Validate all user inputs
- Implement rate limiting
- Use Azure Key Vault for production secrets
- Secure SignalR connections with authentication

---

## 🔄 CI/CD Pipeline

### GitHub Actions Integration
```yaml
# .github/workflows/deploy.yml
name: Deploy to Azure
on:
  push:
    branches: [main]
jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Setup .NET
        uses: actions/setup-dotnet@v3
      - name: Login to Azure
        uses: azure/login@v1
      - name: Deploy with azd
        run: azd deploy --no-prompt
```

### Testing in Pipeline
- Unit tests with code coverage
- Integration tests with test containers
- UI tests with Playwright
- Security scanning with CodeQL

---

## 🎯 Development Best Practices

### Performance Optimization
- Use async/await patterns consistently
- Implement caching for frequently accessed data
- Optimize SignalR connection management
- Monitor Azure service quotas and limits

### Monitoring & Observability
- Application Insights integration
- Custom telemetry for agent interactions
- Performance counters for group chat
- Health checks for Azure services

### Documentation Requirements
- XML documentation for public APIs
- README with setup instructions
- API documentation with OpenAPI/Swagger
- Architecture decision records (ADRs)

---

## 🤖 Copilot Agent Mode Instructions

When working in agent mode:
1. **Multi-file Context**: Always consider the full project structure
2. **Incremental Development**: Build features incrementally with tests
3. **Azure Integration**: Prefer Azure services and follow cloud-native patterns
4. **Real-time Features**: Implement SignalR for chat functionality
5. **Configuration-driven**: Use .env and appsettings for all configurations
6. **Testing-first**: Write tests alongside feature implementation
7. **Deployment-ready**: Ensure all code works with azd deployment
