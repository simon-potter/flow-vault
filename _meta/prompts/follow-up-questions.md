# Follow-Up Questions Prompt

Used to generate deep follow-up questions for further investigation.

## Template Variables

- `{{video_title}}` - The title of the video
- `{{summary}}` - The generated summary
- `{{focus_instruction}}` - Optional focus area instruction

## Prompt

Based on the following video summary, generate deep follow-up questions for further investigation.

Video Title: "{{video_title}}"

Summary:
{{summary}}

{{focus_instruction}}

---

Generate 8-10 thought-provoking follow-up questions that:

- Dig deeper into key concepts mentioned
- Challenge assumptions or explore edge cases
- Connect ideas to broader contexts
- Identify gaps in the information provided
- Explore practical implications

Format your response as a JSON array of strings:
```json
["Question 1?", "Question 2?", "Question 3?", ...]
```

Each question should be specific, actionable, and designed to uncover deeper understanding.
