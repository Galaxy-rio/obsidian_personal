---
title: Obsidian Folder Structure
created: 2025-10-07 10:21:56
modified: 2025-10-07 10:21:56
status: Done
tags:
  - Obsidian
  - Structure
类别: "[[../Msic|Msic]]"
cssclasses:
  - misc
---
# Obsidian Folder Structure

此 Obsidian 仓库的文件存储路径如下：

```sh
Vault/Theme/Project(Type)/Note.md

Theme:
    - Curio
    - Knowledge
    - Misc
    - Museion
    - Tutorials
```

对于较复杂的 `Project`，将 `Note.md` 作为索引，同级创建 `detail` 文件夹存储项目的所有文件。

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

const container = dv.el("div", "", { cls: "sudoku-grid" });
for (let i = 0; i < sudoku.length; i++) {
  const num = sudoku[i] === "0" ? "" : sudoku[i];
  const cell = dv.el("div", num, { cls: ["sudoku-cell", sudoku[i] === "0" ? "empty" : ""] });
  container.appendChild(cell);
}
```
