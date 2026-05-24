# Research Vault Prompts

This directory contains LLM prompts used by the research vault system. These prompts are versioned alongside the vault content and can be edited in Obsidian.

## Available Prompts

| Prompt | Purpose |
|--------|---------|
| `summarize.md` | Generate comprehensive summaries of content |
| `research-perspectives.md` | Create research prompts from technical, practical, critical, and exploratory perspectives |
| `follow-up-questions.md` | Generate deep follow-up questions for investigation |
| `research-outline.md` | Create structured research outlines |
| `topic-extraction.md` | Extract topics for tagging and cross-referencing |
| `synthesis.md` | Synthesize knowledge across multiple sources |

## Template Variables

Prompts use `{{variable}}` syntax for substitution. Common variables:

- `{{title}}` / `{{video_title}}` - Content title
- `{{summary}}` - Generated summary
- `{{transcript}}` - Full transcript (videos)
- `{{focus_instruction}}` - Optional focus area

## Customization

You can edit these prompts to adjust:
- Output format and structure
- Level of detail requested
- Specific aspects to focus on
- JSON schema for responses

Changes take effect immediately when the backend reloads.

## Security Note

**Never include actual API keys or secrets in prompts.** Use placeholders like `YOUR_API_KEY_HERE` if examples are needed.
