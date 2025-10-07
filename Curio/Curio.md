---
tags: [Index]
---

# Index of Curio

```base
views:
  - type: cards
    name: 表格
    filters:
      and:
        - file.folder.startsWith("Curio")
        - '!file.folder.endsWith("details")'
        - '!file.hasTag("Index")'
    cardSize: 400

```
