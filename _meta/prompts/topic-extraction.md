# Topic Extraction Prompt

Used to extract topics from content for tagging and cross-referencing.

## Template Variables

- `{{title}}` - The title of the content
- `{{summary}}` - The generated summary

## Prompt

Based on the following content, extract relevant topics for categorization and cross-referencing.

Title: "{{title}}"

Summary:
{{summary}}

---

Extract 3-7 topics that best represent the main themes and subjects of this content.

Guidelines:
- Use lowercase, hyphenated slugs (e.g., "machine-learning", "climate-change")
- Be specific enough to be useful, but general enough to group related content
- Avoid overly broad topics like "technology" or "science" unless that's truly the focus
- Consider both the main subject and secondary themes
- Include methodological topics if relevant (e.g., "meta-analysis", "case-study")

Format your response as a JSON array:
```json
{
    "topics": ["topic-1", "topic-2", "topic-3"],
    "confidence": "high|medium|low",
    "reasoning": "Brief explanation of topic selection"
}
```
