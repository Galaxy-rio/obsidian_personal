---
title: direct-technique
created: 2025-10-07 16:47:33
modified: 2025-10-07 16:47:33
status: Done
tags:
  - Index
cssclasses:
  - detail
级别: 3
project: "[[../Sudoku|Sudoku]]"
---

# direct-technique

> 直观技巧

```base
filters:
  and:
    - file.inFolder("Knowledge/Sudoku/02-direct-technique")
    - '!file.hasTag("index")'
views:
  - type: cards
    name: 表格
    cardSize: 400
```