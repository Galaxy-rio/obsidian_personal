---
title: 基于 Dataviewjs 绘制数独
created: 2025-10-07 14:17:18
modified: 2025-10-07 14:17:18
status: Done
tags:
  - Dataview
  - Obsidian
  - Sudoku
类别: "[[../Tutorials|Tutorials]]"
cssclasses:
  - misc
---

# 基于 Dataviewjs 绘制数独

需要安装 Dataview 插件。

准备好 CSS 文件用于渲染：

```CSS
/* Sudoku Grid Styles */
.sudoku-grid {
  display: grid;
  grid-template-columns: repeat(9, 2rem);
  grid-template-rows: repeat(9, 2rem);
  border: 2px solid #000;
  border-radius: 8px;
  background: #fff;
  overflow: hidden;
  font-family: monospace;
  text-align: center;
  line-height: 2rem;
  font-size: 1.2rem;
  width: max-content;
}

/* 绘制粗线与细线 */
.sudoku-grid {
  background-image:
    linear-gradient(to right, #000 2px, transparent 2px),
    linear-gradient(to bottom, #000 2px, transparent 2px),
    linear-gradient(to right, #ccc 1px, transparent 1px),
    linear-gradient(to bottom, #ccc 1px, transparent 1px);
  background-size:
    calc(2rem * 3) calc(2rem * 9),
    calc(2rem * 9) calc(2rem * 3),
    2rem 2rem,
    2rem 2rem;
}

.sudoku-cell {
  width: 2rem;
  height: 2rem;
  display: flex;
  align-items: center;
  justify-content: center;
}

.sudoku-cell.empty {
  color: #ccc;
}
```

要在正文中添加数独，使用 Dataviewjs 代码块：

````markdown
```dataviewjs
const sudoku = `
530070000
600195000
098000060
800060003
400803001
700020006
060000280
000419005
000080079
`.replace(/\s+/g, '');

// 创建容器
const container = document.createElement("div");
container.className = "sudoku-grid";

// 填充格子
for (let i = 0; i < sudoku.length; i++) {
    const num = sudoku[i] === "0" ? "" : sudoku[i];
    const cell = document.createElement("div");
    cell.className = "sudoku-cell" + (sudoku[i] === "0" ? " empty" : "");
    cell.textContent = num;
    container.appendChild(cell);
}

// 挂到页面上
dv.container.appendChild(container);
```
````

