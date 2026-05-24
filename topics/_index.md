# Topics Index

This is the Map of Content (MOC) for all topics in the vault.

## All Topics

```dataview
TABLE
    topic_name as "Topic",
    length(file.inlinks) as "Sources"
FROM "topics"
WHERE type = "topic"
SORT topic_name ASC
```

## Topics by Source Count

```dataview
TABLE topic_name, length(file.inlinks) as "Sources"
FROM "topics"
WHERE type = "topic"
SORT length(file.inlinks) DESC
LIMIT 20
```

## Recently Updated

```dataview
TABLE topic_name, updated_at
FROM "topics"
WHERE type = "topic"
SORT updated_at DESC
LIMIT 10
```

## Browse by Domain

- [[topics/|All Topics]]

---

> [!tip] Creating New Topics
> Topics are automatically created when sources are processed. You can also manually create topic notes using the [[_meta/templates/topic|topic template]].
