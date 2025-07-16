# Day 3: GitHub Copilot & MCP

## 🎯 Learning Objectives

By the end of Day 3, you will:
- Install and configure GitHub Copilot in Visual Studio Professional
- Understand GitHub Copilot key concepts including agent mode
- Learn the different modes of GitHub Copilot
- Understand how to configure tools for Visual Studio Code
- Understand how to configure tools for Visual Studio Enterprise
- Learn how to setup a GitHub instruction file

## 📚 Key Concepts

### GitHub Copilot Architecture
- **AI-Powered Assistant**: Context-aware code completion and generation
- **Agent Mode**: Conversational AI for complex development tasks
- **Multi-IDE Support**: Integration across Visual Studio, VS Code, and other environments
- **Enterprise Integration**: Organizational policies and compliance features

### Copilot Modes Overview
- **Inline Suggestions**: Real-time code completion while typing
- **Chat Mode**: Interactive conversations for code explanations and generation
- **Agent Mode**: Specialized AI agents for specific development tasks
- **Workspace Mode**: Project-aware assistance with full context understanding

### MCP (Model Context Protocol)
- **Client-Server Architecture**: Standardized communication between AI models
- **Tool Integration**: Extensible framework for custom AI capabilities
- **Context Management**: Efficient handling of large codebases and documentation
- **Security Framework**: Enterprise-grade access controls and data protection

## 🚀 Session 1: GitHub Copilot Installation & Configuration (45 minutes)

### Prerequisites
- Visual Studio Professional 2022 (17.8 or later)
- Active GitHub account with Copilot subscription
- Azure subscription for enterprise features

### Step 1: Install GitHub Copilot Extension
1. Open Visual Studio Professional
2. Navigate to **Extensions** → **Manage Extensions**
3. Search for "GitHub Copilot"
4. Install the official GitHub Copilot extension
5. Restart Visual Studio when prompted

### Step 2: Authentication Setup
1. Sign in to GitHub through Visual Studio
2. Authorize GitHub Copilot access
3. Verify subscription status in account settings

### Step 3: Basic Configuration via UI
1. In Visual Studio, navigate to **Tools** → **Options**
2. Expand **GitHub Copilot** in the left panel
3. Configure the following settings:
   - **Enable Suggestions**: Check to enable code suggestions
   - **Show Suggestions for**: Select file types (C#, JavaScript, etc.)
   - **Inline Suggestions**: Enable for real-time code completion
   - **Chat Features**: Enable conversational assistance
4. Under **Advanced Settings**:
   - Set **Suggestion Delay**: 100ms (recommended)
   - Configure **Max Suggestions**: 3-5 suggestions
   - Enable **Workspace Context**: For project-aware suggestions
5. Click **OK** to save configuration
6. Restart Visual Studio to apply changes

### Step 4: Verify Installation
1. Open a new C# file in Visual Studio
2. Start typing a function declaration
3. Verify that Copilot suggestions appear
4. Test chat functionality with **Ctrl+/**
```

**Reference**: [GitHub Copilot Documentation](https://docs.github.com/en/copilot/getting-started-with-github-copilot)

## 🤖 Session 2: Understanding Copilot Modes (60 minutes)

### Inline Suggestions Mode
- **Trigger**: Automatic suggestions while typing
- **Navigation**: Tab to accept, Escape to dismiss
- **Cycling**: Alt+] for next suggestion, Alt+[ for previous

### Chat Mode Fundamentals
- **Activation**: Ctrl+/ or click chat icon
- **Context Awareness**: Understands current file and project structure
- **Slash Commands**: `/explain`, `/fix`, `/generate`, `/tests`

### Agent Mode Deep Dive
- **Specialized Agents**: Task-specific AI assistants
- **Agent Types**: Code review, testing, documentation, refactoring
- **Conversation Flow**: Multi-turn interactions with maintained context

### Workspace Mode
- **Project Understanding**: Full repository analysis
- **Cross-File References**: Intelligent suggestions across multiple files
- **Architecture Awareness**: Understands design patterns and project structure

**Reference**: [GitHub Copilot Chat](https://docs.github.com/en/copilot/github-copilot-chat)

## 🔧 Session 3: Tool Configuration for VS Code (45 minutes)

### Extension Setup
1. Install GitHub Copilot and GitHub Copilot Chat extensions
2. Configure workspace settings via UI:
   - Open **File** → **Preferences** → **Settings**
   - Search for "GitHub Copilot"
   - Configure the following settings:
     - **Editor: Enable Auto Completions**: Check to enable automatic suggestions
     - **Advanced: Length**: Set to 500 characters for suggestion length
     - **Advanced: Temperature**: Set to 0.1 for more focused suggestions
     - **Advanced: Secret Key**: Configure GitHub Copilot authentication key
   - Settings are automatically saved to workspace configuration

### Custom Tool Integration
- **API Endpoints**: Configure external service connections
- **Authentication**: Set up tokens and credentials
- **Workspace Configuration**: Project-specific tool settings

### Explore Extension Library for MCP

#### Popular MCP Extensions for VS Code

1. **Open VS Code Extensions Marketplace**
   - Click the Extensions icon in the Activity Bar (Ctrl+Shift+X)
   - Search for "MCP" or "Model Context Protocol"

2. **Microsoft AI Extensions**
   - **Azure AI Services**: Integrates Azure OpenAI and Cognitive Services
   - **Azure Functions**: Serverless function development with AI assistance
   - **Azure DevOps**: CI/CD pipeline integration with intelligent suggestions

3. **Third-Party MCP Extensions**
   - **OpenAI Connector**: Direct integration with OpenAI API endpoints
   - **Anthropic Claude**: Claude model integration for code assistance
   - **Hugging Face Hub**: Access to open-source models and datasets


## 📋 Session 5: GitHub Copilot Instructions File (45 minutes)

### Creating `.github/copilot-instructions.md`
This file provides context-aware instructions for Copilot across your repository.

### Structure and Best Practices
```markdown
# GitHub Copilot Instructions for [Project Name]

## Project Overview
Brief description of project architecture and goals

## Technology Stack & Integration Points
- Primary frameworks and libraries
- Azure services and configurations
- Development patterns and conventions

## Development Workflow
- Project structure explanation
- Common commands and setup procedures
- Testing and deployment patterns

## Project-Specific Conventions
- Coding standards and patterns
- Migration domain expertise (for our hackathon)
- Documentation requirements

## When Working on This Codebase
- Key architectural decisions
- Integration points and dependencies
- Common patterns to follow
```

**Reference**: [GitHub Copilot Instructions](https://docs.github.com/en/copilot/customizing-copilot/adding-custom-instructions-for-github-copilot)

## 🎯 Next Steps

Prepare for Day 4 by understanding how GitHub Copilot's enhanced context and MCP integration will improve Semantic Kernel development workflows and multi-agent orchestration.

