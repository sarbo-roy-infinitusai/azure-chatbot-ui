# InfiniChat UI


**Docker**

Build locally:

```shell
docker build -t chatgpt-ui .
docker run -e OPENAI_API_KEY=xxxxxxxx -p 3000:3000 chatgpt-ui
```

Pull from ghcr:

```
docker run -e OPENAI_API_KEY=xxxxxxxx -p 3000:3000 ghcr.io/mckaywrigley/chatbot-ui:main
```

## Running Locally

**1. Clone Repo**

```bash
git clone https://github.com/mckaywrigley/chatbot-ui.git
```

**2. Install Dependencies**

```bash
npm i
```

**3. Provide OpenAI API Key**

Create a .env.local file in the root of the repo with your OpenAI API Key:

Keys are [here](https://console.cloud.google.com/run/deploy/us-central1/infinichat-auth?hl=en&project=infinitus-dev)

```bash
OPENAI_API_TYPE=azure
OPENAI_API_HOST=https://infinitus-dev2.openai.azure.com
DEFAULT_MODEL=gpt-4
```

> You can set `OPENAI_API_HOST` where access to the official OpenAI host is restricted or unavailable, allowing users to configure an alternative host for their specific needs.

> Additionally, if you have multiple OpenAI Organizations, you can set `OPENAI_ORGANIZATION` to specify one.

**4. Run App**

```bash
npm run dev
```

**5. Use It**

You should be able to start chatting.

## Configuration

When deploying the application, the following environment variables can be set:

| Environment Variable              | Default value                  | Description                                                                                                                               |
| --------------------------------- | ------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------- |
| OPENAI_API_KEY                    |                                | The default API key used for authentication with OpenAI                                                                                   |
| OPENAI_API_HOST                   | `https://api.openai.com`       | The base url, for Azure use `https://<endpoint>.openai.azure.com`                                                                         |
| OPENAI_API_TYPE                   | `openai`                       | The API type, options are `openai` or `azure`                                                                                             |
| OPENAI_API_VERSION                | `2023-03-15-preview`           | Only applicable for Azure OpenAI                                                                                                          |
| AZURE_DEPLOYMENT_ID               |                                | Needed when Azure OpenAI, Ref [Azure OpenAI API](https://learn.microsoft.com/zh-cn/azure/cognitive-services/openai/reference#completions) |
| OPENAI_ORGANIZATION               |                                | Your OpenAI organization ID                                                                                                               |
| DEFAULT_MODEL                     | `gpt-3.5-turbo`                | The default model to use on new conversations, for Azure use `gpt-35-turbo`                                                               |
| NEXT_PUBLIC_DEFAULT_SYSTEM_PROMPT | [see here](utils/app/const.ts) | The default system prompt to use on new conversations                                                                                     |
| NEXT_PUBLIC_DEFAULT_TEMPERATURE   | 1                              | The default temperature to use on new conversations                                                                                       |




  - Chat.tsx: Main chat interface that displays messages and handles API communication
  - ChatInput.tsx: Text input for user messages
  - ChatMessage.tsx: Renders individual messages (user/AI)
  - MemoizedChatMessage.tsx: Performance-optimized message display
  - ModelSelect.tsx: AI model selection dropdown
  - SystemPrompt.tsx: Controls prompt that guides model behavior
  - Temperature.tsx: Adjusts model temperature parameter

  Navigation Components

  - Chatbar/: Left sidebar for conversation history
    - Uses context for state management
    - Handles conversation operations (create, delete, export)
  - Sidebar/: Reusable sidebar container
  - Promptbar/: Right sidebar for managing reusable prompts
    - Context-based state management
    - Organizes prompts in folders

  State Management

  - Uses React Context API for state
  - HomeContext: Manages conversations, settings, and UI state
  - ChatbarContext: Handles conversation list
  - PromptbarContext: Manages saved prompts
  - Custom reducer pattern for predictable state updates

  Data Flow

  1. User types in ChatInput
  2. Message sent to Chat component
  3. API request created with message, model, settings
  4. Request sent to Next.js endpoint
  5. Response streamed from Azure OpenAI
  6. Messages updated in real-time
  7. Conversation saved to localStorage

  Azure Integration

  - Configurable via environment variables
  - Supports Azure-specific authentication
  - Uses deployment IDs for model selection
  - API calls handled via streaming for real-time responses




## Contact

If you have any questions, feel free to reach out to Mckay on [Twitter](https://twitter.com/mckaywrigley).

[GCSE]: https://developers.google.com/custom-search/v1/overview
