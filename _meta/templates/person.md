---
type: person
person_slug: "{{person_slug}}"
display_name: "{{display_name}}"
aliases:
  - "{{alias}}"
identifiers:
  youtube_channel_id: "{{youtube_channel_id}}"
  twitter: "{{twitter}}"
  github: "{{github}}"
  website: "{{website}}"
creator_types: []
created_at: "{{created_at}}"
updated_at: "{{updated_at}}"
tags:
  - person
---

# {{display_name}}

## About
<!-- AI:BEGIN about -->

{Brief bio or description of this person/creator}

<!-- AI:END about -->

## Content by {{display_name}}

### YouTube Videos
```dataview
TABLE title, duration, processed_at
FROM "sources/youtube"
WHERE contains(string(people), this.file.name)
SORT processed_at DESC
LIMIT 20
```

### Articles & Papers
```dataview
TABLE title, processed_at
FROM "sources/web" OR "sources/pdf"
WHERE contains(string(people), this.file.name)
SORT processed_at DESC
LIMIT 20
```

## Topics Covered

```dataview
LIST
FROM "topics"
WHERE file.inlinks AND contains(file.inlinks.path, this.file.path)
SORT file.name ASC
```

## My Notes
<!-- USER:BEGIN notes -->
^notes

{Your notes about this person/creator}

<!-- USER:END notes -->

---
*Created: {{created_at}} | Updated: {{updated_at}}*
