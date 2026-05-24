# Research Vault

Welcome to your research vault. This is your second brain for synthesizing knowledge from multiple sources.

## Quick Navigation

- [[topics/_index|Topics]] - Browse by theme
- [[people/|People]] - Content creators and authors
- [[projects/|Projects]] - Active research investigations

## Recent Sources

### YouTube Videos
```dataview
TABLE title, channel, processed_at
FROM "sources/youtube"
SORT processed_at DESC
LIMIT 10
```

### Web Articles
```dataview
TABLE title, domain, processed_at
FROM "sources/web"
SORT processed_at DESC
LIMIT 10
```

### PDFs & Papers
```dataview
TABLE title, author, processed_at
FROM "sources/pdf"
SORT processed_at DESC
LIMIT 10
```

## Vault Statistics

```dataview
TABLE length(rows) as "Count"
FROM ""
WHERE type = "source"
GROUP BY source_type
```

## Getting Started

1. **Capture content** - Use the Streamlit GUI to process videos, articles, and PDFs
2. **Explore topics** - Browse [[topics/_index|Topics]] to find related content
3. **Add your notes** - Each source has a "My Notes" section for your insights
4. **Create synthesis** - Build topic notes that connect ideas across sources

## Workflow Tips

- Use `Cmd/Ctrl + O` to quick switch between notes
- Use `Cmd/Ctrl + Shift + F` to search across all content
- The Graph View shows connections between notes
- Use tags in the Tag Pane for filtering

---
*Vault created: {{created_at}}*
