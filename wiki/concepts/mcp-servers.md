---
title: "MCP Servers"
type: concept
tags: [mcp, claude-code, tools, integration, protocol, foundational]
created: 2026-05-04
updated: 2026-05-04
sources: ["raw/Using CLAUDE.MD files Customizing Claude Code for your codebase.md"]
confidence: high
---

## Definition

MCP (Model Context Protocol) servers are external processes that extend Claude Code's capabilities by providing additional tools, data sources, and integrations. Claude Code functions as an MCP client, connecting to configured servers and gaining access to their exposed tools without the tools needing to be built into Claude Code itself.

## How It Works

### Client-Server Architecture
1. **MCP client**: Claude Code acts as client, managing connections to configured servers
2. **MCP servers**: Standalone processes exposing tools via MCP protocol
3. **Tool discovery**: Client discovers available tools when server connects
4. **Tool invocation**: Claude can call server tools like built-in tools (Read, Write, Bash, etc.)

### Configuration Methods
- **Project settings**: `.mcp.json` in project directory (can be checked in)
- **Global configuration**: User-level MCP server configuration
- **Managed settings**: Organization-wide MCP server policies

### Connection Lifecycle
- Servers connect at session start (OAuth flows if required)
- Tools become available to Claude throughout session
- Connection issues can be debugged with `--mcp-debug` flag

## Key Parameters

### Server Types
- **Data access**: Database servers, filesystem servers, API clients
- **External services**: Slack, GitHub, Linear, email servers
- **Custom tools**: Project-specific utilities exposed via MCP
- **State management**: Servers that maintain persistent state

### Tool Naming
MCP tools follow pattern: `mcp__<server>__<tool>`
- Example: `mcp__memory__create_entities`
- Example: `mcp__github__search_repositories`

Can be matched in [[concepts/hooks]] with patterns like `mcp__memory__.*` for all memory server tools.

### Documentation in CLAUDE.md
When documenting MCP servers:
- **Usage guidelines**: When to use specific tools
- **Rate limits**: API or service constraints
- **Permissions**: What the server can/cannot access
- **Conventions**: Project-specific patterns for tool use

Example:
```markdown
### Slack MCP
- Posts to #dev-notifications channel only
- Use for deployment notifications and build failures
- Do not use for individual PR updates
- Rate limited to 10 messages per hour
```

## When To Use

Use MCP servers when you need:
- **External data access**: Reading from databases, APIs, services Claude can't reach directly
- **Stateful operations**: Maintaining state between Claude sessions
- **Third-party integrations**: Slack, GitHub, Jira, email without custom implementation
- **Custom business logic**: Company-specific tools and workflows
- **Controlled access**: Mediating Claude's access to sensitive resources

Don't use for:
- Operations Claude's built-in tools already handle (file system, bash, etc.)
- Simple scripts that could run via Bash tool
- One-off integrations with no reuse value

## Risks & Pitfalls

### Common Issues
1. **Connection failures**: Server not running or authentication expired
2. **OAuth complexity**: Some servers require complex OAuth flows
3. **Rate limiting**: External API limits affect Claude's workflow
4. **Debugging difficulty**: MCP layer adds indirection vs direct tool calls
5. **Version compatibility**: Server updates may break compatibility
6. **Documentation overhead**: Team needs to know what MCP tools do

### Security Considerations
- MCP servers have access to data they're configured for
- OAuth tokens and credentials need secure storage
- Server code runs with user's permissions
- Malicious servers could exfiltrate data
- Use managed policies to control which servers are allowed

### Performance Implications
- Network latency for remote servers
- Authentication overhead on connection
- External service downtime affects Claude
- Multiple tool calls may hit rate limits

## Related Concepts

- [[concepts/claude-md-configuration]] - Where MCP servers are documented
- [[concepts/hooks]] - Can trigger on MCP tool calls
- [[concepts/claude-skills]] - Skills can invoke MCP tools
- [[concepts/tool-integration]] - Broader category of extending Claude
- [[concepts/api-clients]] - Common MCP server use case

## Sources

- "Using CLAUDE.MD files: Customizing Claude Code for your codebase" (Anthropic blog, 2001-11-25)
- References: "MCP fundamentals and best practices" (mentioned in source)
