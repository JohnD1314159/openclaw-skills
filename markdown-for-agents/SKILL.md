---
name: markdown-for-agents
description: Fetch web pages using Cloudflare's Markdown for Agents when available. Use this skill when Codex needs to browse, parse, or extract content from web pages. The skill attempts to get markdown format first, falling back to standard methods when unavailable.
---

# Markdown for Agents

Smart web content fetching that prioritizes markdown format from Cloudflare-enabled sites.

## When to Use This Skill

When Codex needs to:
- Browse or parse web pages
- Extract content from URLs
- Fetch structured data from websites

## Workflow

### Step 1: Try Markdown for Agents

Request with `Accept: text/markdown` header:

```bash
curl -s "https://example.com/page" -H "Accept: text/markdown"
```

### Step 2: Check Response

| Indicator | Meaning |
|-----------|---------|
| `Content-Type: text/markdown` | ✅ Success - use markdown content |
| Header `x-markdown-tokens:` | ✅ Success - Cloudflare supports markdown |
| Content starts with `---` frontmatter | ✅ Success - valid markdown format |

### Step 3: Fallback (if not supported)

If markdown not available, use:
- `web_fetch` tool for simple pages
- `browser` tool for complex/dynamic pages

## Example

```bash
# Try markdown first
curl -s "https://blog.cloudflare.com/markdown-for-agents/" -H "Accept: text/markdown"

# If no markdown, fallback
web_fetch url="https://example.com"
```

## Notes

- Only works on Cloudflare zones with Markdown for Agents enabled
- Saves tokens (80% reduction vs HTML)
- Cleaner, structured content is easier to process
