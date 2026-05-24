# Synthesis Prompt

Used to generate topic synthesis notes that aggregate insights across multiple sources.

## Template Variables

- `{{topic_name}}` - The name of the topic
- `{{sources}}` - JSON array of source summaries with metadata

## Prompt

You are synthesizing knowledge about "{{topic_name}}" from multiple sources.

Sources:
{{sources}}

---

Create a comprehensive synthesis that:

1. **Overview**: Provide a high-level understanding of this topic based on all sources (2-3 paragraphs)

2. **Key Insights**: List the most important insights, attributing each to its source:
   - Insight (from [[source-link]])
   - Pattern observed across multiple sources

3. **Points of Agreement**: What do the sources consistently support?

4. **Points of Tension**: Where do sources disagree or present different perspectives?

5. **Gaps**: What important aspects of this topic aren't covered by these sources?

6. **Open Questions**: What questions remain unanswered?

Format using Markdown with clear sections. Use wikilinks to reference specific sources.
Aim for depth over breadth - focus on meaningful synthesis rather than just summarizing.
