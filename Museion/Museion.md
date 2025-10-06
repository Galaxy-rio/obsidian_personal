---
tags: [Index]
---

# Index of Museion

## Anime
```base
filters:
  and:
    - file.inFolder("Museion/Anime")
formulas:
  导演: if(导演.length > 1, 导演[0] + " 等", 导演[0])
views:
  - type: cards
    name: 表格
    order:
      - file.name
      - formula.导演
      - status
    sort:
      - property: file.ctime
        direction: DESC
    image: note.cover
    imageAspectRatio: 1.4
    cardSize: 140

```

## Books
```base
filters:
  and:
    - file.inFolder("Museion/Books")
formulas:
  作者: if(author.length > 1, author[0] + " 等", author[0])
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
    cardSize: 140

```

## Movies

