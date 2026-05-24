# Research Perspectives Prompt

Used to generate research prompts from four different perspectives.

## Template Variables

- `{{video_title}}` - The title of the video
- `{{summary}}` - The generated summary
- `{{focus_instruction}}` - Optional focus area instruction

## Prompt

Based on the following video summary, generate research prompts from four different perspectives.

Video Title: "{{video_title}}"

Summary:
{{summary}}

{{focus_instruction}}

---

Generate one detailed research prompt for each perspective:

1. **Technical**: A prompt for exploring the technical/implementation aspects, methodologies, or underlying mechanisms discussed.

2. **Practical**: A prompt for investigating real-world applications, use cases, or how to apply the concepts.

3. **Critical**: A prompt for evaluating limitations, counterarguments, potential issues, or alternative viewpoints.

4. **Exploratory**: A prompt for discovering related topics, deeper connections, or future implications.

Format your response as valid JSON:
```json
{
    "technical": "Your technical research prompt here...",
    "practical": "Your practical research prompt here...",
    "critical": "Your critical research prompt here...",
    "exploratory": "Your exploratory research prompt here..."
}
```

Each prompt should be 2-4 sentences and provide a clear direction for deep research.
