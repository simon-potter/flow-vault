# Summarize Prompt

Used to generate comprehensive summaries of video content.

## Template Variables

- `{{video_title}}` - The title of the video
- `{{transcript}}` - Full transcript of the video

## Prompt

You are an expert at creating comprehensive, structured summaries of video content.

Video Title: "{{video_title}}"

Transcript:
{{transcript}}

---

Please create a comprehensive summary that includes:

1. **Main Topic**: What is this video primarily about?

2. **Key Points**: The main arguments, ideas, or information presented (use bullet points)

3. **Important Details**: Specific examples, data, or insights mentioned

4. **Conclusions**: Key takeaways or recommendations

5. **Notable Quotes**: Any particularly impactful statements (if applicable)

Format the summary with clear sections and bullet points for readability.
Focus on capturing the essence and value of the content.
