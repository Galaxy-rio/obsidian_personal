---
title: Sudoku
created: 2025-10-07 15:04:41
modified: 2025-10-07 15:04:41
status: On Going
tags:
  - Sudoku
  - Index
类别: "[[../Knowledge|Knowledge]]"
cssclasses:
  - knowledge
---

# Sudoku

```base
filters:
  and:
    - file.inFolder("Knowledge/Sudoku")
    - 级别 == 3
views:
  - type: cards
    name: 表格
    order:
      - file.name
    sort:
      - property: file.folder
        direction: ASC
    cardSize: 400
```