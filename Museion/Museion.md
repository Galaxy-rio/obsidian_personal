---
tags: [Index]
---

# Index of Museion

## Anime
```base
filters:
  and:
    - file.inFolder("Museion/Anime")
views:
  - type: cards
    name: 表格
    order:
      - file.name
      - 导演
      - status
    sort:
      - property: file.ctime
        direction: DESC
    image: note.cover
    imageAspectRatio: 1.4
    cardSize: 150

```

## Books
```base
filters:
  and:
    - file.inFolder("Museion/Books")
formulas:
  作者: author[0]
views:
  - type: cards
    name: 表格
    order:
      - file.name
      - formula.作者
      - status
    sort:
      - property: file.ctime
        direction: DESC
    image: note.cover
    imageFit: contain
    imageAspectRatio: 1.4
    cardSize: 150

```

## Movies

