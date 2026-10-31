MCP (model context protocol) is a standard way for an AI application to connect to external systems like databases, APIs and files.

### How it works
- **MCP client**: The AI application (e.g. Claude Desktop or Claude Code).
- **MCP Server**: Connects to an external system and exposes tools the AI can use.
- **Tools**: Functions the AI can request, such as querying a database or checking parcel status.

Example: I used the Supabase MCP server in Claude Code to inspect database tables, run SQL queries, and apply migrations while building my restaurant pipeline.

### MCP vs an API
AN API is for code to call a system. MCP is for a model to call a system: the server describes its tools so the model can pick them itself, and the server calls the real API underneath.

