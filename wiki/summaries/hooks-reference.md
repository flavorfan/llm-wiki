---
title: "Hooks Reference Documentation"
type: summary
tags: [hooks, claude-code, automation, reference, lifecycle-events, configuration]
created: 2026-05-04
updated: 2026-05-04
sources: ["raw/Hooks reference.md"]
confidence: high
---

## Key Points

### Overview
- **Definition**: User-defined shell commands, HTTP endpoints, or LLM prompts that execute automatically at specific lifecycle points
- **Purpose**: Automate workflows, validate operations, inject context, enforce policies without instructions in CLAUDE.md
- **Types**: Command hooks (shell), HTTP hooks (POST requests), MCP tool hooks, Prompt hooks (LLM evaluation), Agent hooks (subagent verification)

### Hook Lifecycle
Three cadences:
1. **Per-session**: `SessionStart`, `SessionEnd`, `Setup`
2. **Per-turn**: `UserPromptSubmit`, `Stop`, `StopFailure`
3. **Per-tool**: `PreToolUse`, `PostToolUse`, `PostToolUseFailure`, `PermissionRequest`, `PermissionDenied` (in agentic loop)
4. **Async events**: `Notification`, `ConfigChange`, `CwdChanged`, `FileChanged`, `WorktreeCreate/Remove`

### Configuration Structure
Three levels of nesting:
1. **Hook event**: Lifecycle point to respond to (e.g., `PreToolUse`)
2. **Matcher group**: Filter when it fires (e.g., "only for Bash tool")
3. **Hook handler**: Shell command, HTTP endpoint, MCP tool, or prompt that runs

### Hook Locations
- `~/.claude/settings.json` - All projects (local machine)
- `.claude/settings.json` - Single project (shareable)
- `.claude/settings.local.json` - Project-specific (gitignored)
- Managed policy settings - Organization-wide
- Plugin `hooks/hooks.json` - When plugin enabled
- Skill/agent frontmatter - While component active

### Matcher Patterns
- `"*"`, `""`, omitted - Match all
- Letters/digits/`_`/`|` only - Exact string or pipe-separated list
- Other characters - JavaScript regex
- MCP tools: `mcp__<server>__<tool>` naming pattern

### Decision Control via Exit Codes
- **Exit 0**: Success, process JSON output
- **Exit 2**: Blocking error (shows stderr to Claude, prevents action)
- **Other codes**: Non-blocking error (logged, execution continues)

### JSON Output Fields
- **Universal**: `continue` (stop entirely), `stopReason`, `suppressOutput`, `systemMessage`
- **Context injection**: `additionalContext` (wrapped in system reminder for Claude)
- **Decision control**: Event-specific fields (`decision: "block"`, `permissionDecision`, etc.)
- **Event-specific**: `hookSpecificOutput` with `hookEventName` field

### Key Events (Partial List)
- **SessionStart**: Load development context, set environment variables via `CLAUDE_ENV_FILE`
- **Setup**: One-time dependency installation (`--init-only`, `--init`, `--maintenance` in `-p` mode)
- **InstructionsLoaded**: When CLAUDE.md or rules files load (observability only)
- **UserPromptSubmit**: Validate/block prompts, add context before Claude processes
- **UserPromptExpansion**: When slash command expands (can block specific commands)
- **PreToolUse**: Before tool executes, can allow/deny/ask/defer
- **PostToolUse**: After tool succeeds, can run linters/formatters
- **PermissionRequest**: When permission dialog appears
- **PermissionDenied**: When auto mode classifier denies tool (can set `retry: true`)
- **FileChanged**: When watched files change on disk (specify patterns in matcher)

### Advanced Features
- **Path-specific rules**: `.claude/rules/` with `paths:` frontmatter for conditional loading
- **Async hooks**: Background execution with `async: true`, `asyncRewake: true` for failures
- **HTTP hooks**: POST JSON to URL with env var interpolation in headers
- **MCP tool hooks**: Call tools on connected MCP servers with `${path}` substitution
- **Prompt/agent hooks**: Send prompts to Claude models or spawn subagents for verification

### Environment Variables
- `$CLAUDE_PROJECT_DIR` - Project root
- `${CLAUDE_PLUGIN_ROOT}` - Plugin installation directory
- `${CLAUDE_PLUGIN_DATA}` - Plugin persistent data directory
- `CLAUDE_ENV_FILE` - File path for persisting env vars (SessionStart, Setup, CwdChanged, FileChanged)

## Relevant Concepts

- [[concepts/hooks]] - Core hooks concept
- [[concepts/lifecycle-events]] - Event-driven architecture
- [[concepts/code-style-automation]] - Using PostToolUse for formatting
- [[concepts/permission-system]] - PermissionRequest/PermissionDenied hooks
- [[concepts/context-injection]] - additionalContext field
- [[concepts/mcp-servers]] - MCP tool hooks integration
- [[concepts/event-matchers]] - Pattern matching for hook triggers

## Source Metadata

- **Type**: Technical reference documentation
- **Publisher**: Claude Code official documentation
- **URL**: https://code.claude.com/docs/en/hooks
- **Accessed**: 2026-05-03
- **Companion**: [Automate workflows with hooks](https://code.claude.com/docs/en/hooks-guide) (quickstart guide)
- **Note**: This summary covers ~1000 lines of 34,000+ token document; full reference contains detailed schemas for all hook events, input/output formats, and examples
