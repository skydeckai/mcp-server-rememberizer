# MCP Server Rememberizer

[![smithery badge](https://smithery.ai/badge/mcp-server-rememberizer)](https://smithery.ai/server/mcp-server-rememberizer)

A [Model Context Protocol](https://www.anthropic.com/news/model-context-protocol) server for interacting with Rememberizer's document and knowledge management API. This server enables Large Language Models to search, retrieve, and manage documents and integrations through Rememberizer.

Please note that `mcp-server-rememberizer` is currently in development and the functionality may be subject to change.

## Components

### Resources

The server provides access to two types of resources: Documents or Slack discussions

### Tools

1. `rememberizer_search`

    - Search for documents by semantic similarity
    - Input:
        - `q` (string): Up to a 400-word sentence to find semantically similar chunks of knowledge
        - `n` (integer, optional): Number of similar documents to return (default: 5)
        - `from` (string, optional): Start date in ISO 8601 format with timezone (e.g., 2023-01-01T00:00:00Z). Use this to filter results from a specific date (default: None)
        - `to` (string, optional): End date in ISO 8601 format with timezone (e.g., 2024-01-01T00:00:00Z). Use this to filter results until a specific date (default: None)
    - Returns: Search results as text output

2. `rememberizer_agentic_search`

    - Search for documents by semantic similarity with LLM Agents augmentation
    - Input:
        - `query` (string): Up to a 400-word sentence to find semantically similar chunks of knowledge. This query can be augmented by our LLM Agents for better results.
        - `n_chunks` (integer, optional): Number of similar documents to return (default: 5)
        - `user_context` (string, optional): The additional context for the query. You might need to summarize the conversation up to this point for better context-awared results (default: None)
        - `from` (string, optional): Start date in ISO 8601 format with timezone (e.g., 2023-01-01T00:00:00Z). Use this to filter results from a specific date (default: None)
        - `to` (string, optional): End date in ISO 8601 format with timezone (e.g., 2024-01-01T00:00:00Z). Use this to filter results until a specific date (default: None)
    - Returns: Search results as text output

3. `rememberizer_list_integrations`

    - List available data source integrations
    - Input: None required
    - Returns: List of available integrations

4. `rememberizer_account_information`

    - Get account information
    - Input: None required
    - Returns: Account information details

5. `rememberizer_list_documents`

    - Retrieves a paginated list of all documents
    - Input:
        - `page` (integer, optional): Page number for pagination, starts at 1 (default: 1)
        - `page_size` (integer, optional): Number of documents per page, range 1-1000 (default: 100)
    - Returns: List of documents

## Installation

### Via mcp-get.com

```bash
npx @michaellatman/mcp-get@latest install mcp-server-rememberizer
```

### Via Smithery

```bash
npx -y @smithery/cli install mcp-server-rememberizer --client claude
```

### Via SkyDeck AI Helper App

If you have SkyDeck AI Helper app installed, you can search for "Rememberizer" and install the mcp-server-rememberizer.

![SkyDeck AI Helper](https://docs.rememberizer.ai/~gitbook/image?url=https%3A%2F%2F2952947711-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FyNqpTh7Mh66N0RnO0k24%252Fuploads%252FYyy7b70uYnO8Gm5V7spp%252Fimage.png%3Falt%3Dmedia%26token%3D008d56ea-44f8-482a-a889-f7d933f1d734&width=768&dpr=2&quality=100&sign=661e8789&sv=2)

## Configuration

### Environment Variables

The following environment variables are required:

-   `REMEMBERIZER_API_TOKEN`: Your Rememberizer API token

You can register an API key by creating your own [Common Knowledge in Rememberizer](https://docs.rememberizer.ai/developer/registering-and-using-api-keys).

### Usage with Claude Desktop

Add this to your `claude_desktop_config.json`:

```json
"mcpServers": {
  "rememberizer": {
      "command": "uvx",
      "args": ["mcp-server-rememberizer"],
      "env": {
        "REMEMBERIZER_API_TOKEN": "your_rememberizer_api_token"
      }
    },
}
```

### Usage with SkyDeck AI Helper App

Add the env REMEMBERIZER_API_TOKEN to mcp-server-rememberizer.

![SkyDeck AI Helper Configuration](https://docs.rememberizer.ai/~gitbook/image?url=https%3A%2F%2F2952947711-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FyNqpTh7Mh66N0RnO0k24%252Fuploads%252FwQnwWCWlNbdVmJqyxHQp%252Fimage.png%3Falt%3Dmedia%26token%3D6032aa53-c1e9-46ee-b0fd-089fcb63dcc6&width=768&dpr=2&quality=100&sign=38c5ec43&sv=2)

With support from the Rememberizer MCP server, you can now ask the following questions in your Claude Desktop app or SkyDeck AI GenStudio

-   _What is my Rememberizer account?_

-   _List all documents that I have there._

-   _Give me a quick summary about "..."_

-   and so on...

## License

This project is licensed under the Apache License 2.0 - see the [LICENSE](LICENSE) file for details.
