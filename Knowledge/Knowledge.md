---
tags: [Index]
---

# Index of Knowledge

## Sudoku

```base
filters:
  and:
    - file.inFolder("Knowledge/Sudoku")
    - file.path.endsWith("Sudoku.md")
views:
  - type: cards
    name: 表格
    order:
      - file.name
    cardSize: 400

```

