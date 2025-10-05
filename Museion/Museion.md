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
views:
  - type: cards
    name: 表格
    sort:
      - property: file.ctime
        direction: DESC
    image: note.cover
    imageFit: contain
    imageAspectRatio: 1.4
    cardSize: 150

```

## Movies

