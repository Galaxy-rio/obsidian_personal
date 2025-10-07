---
title: 基于 TikZ 绘制数独
created: 2025-10-07 14:34:29
modified: 2025-10-07 14:34:29
status: Done
tags:
  - Obsidian
  - TikZ
  - Sudoku
类别: "[[../Tutorials|Tutorials]]"
cssclasses:
  - tutorial
---
# 基于 TikZ 绘制数独

需要安装 TikZ 插件。

## 无候选数数独

要在正文中添加数独，使用 TikZ 代码块：

````markdown
```tikz
\begin{document}
\tikzset{
    highlight/.style = {gray, opacity=0.3},
    digit/.style = {minimum height=5mm, minimum width=5mm, anchor=center},
    circle/.style = {draw=black!80!black, dotted, very thick},
    cross/.style = {red, opacity=.5, shorten >=1mm, shorten <=1mm, very thick, line cap=round},
    hint/.style={black, font=\sf, minimum width=3mm, minimum height=3mm}
}

\newcounter{row}
\newcounter{col}

\newcommand\setrow[9]{
    \setcounter{col}{1}
    \foreach \n in {#1,#2,#3,#4,#5,#6,#7,#8,#9} {
        \edef\x{\value{col}-0.5}
        \edef\y{9.5-\value{row}}
        \node[digit,name={\arabic{row}-\arabic{col}}] at (\x,\y) {\n};
        \stepcounter{col}
    }
    \stepcounter{row}
}

% 高亮矩形
\def\highlightrectangle#1#2#3#4{
    \fill[highlight] (#1-#2.north west) rectangle (#3-#4.south east);
}

\begin{tikzpicture}[scale=0.5]
    % 绘制网格
    \draw (0,0) grid (9,9);
    \draw[very thick] (0,0) grid[step=3] (9,9);

    % 设置行计数
    \setcounter{row}{1}

    % 示例数据
    \setrow { }{ }{9} { }{ }{ } {2}{6}{ }
    \setrow {2}{ }{ } { }{8}{4} { }{ }{ }
    \setrow {5}{ }{ } {2}{ }{ } { }{ }{1}

    \setrow { }{6}{ } {1}{ }{9} {7}{ }{ }
    \setrow { }{9}{ } { }{7}{ } { }{4}{ }
    \setrow { }{ }{7} {4}{ }{3} { }{9}{ }

    \setrow {3}{ }{ } { }{ }{6} { }{ }{5}
    \setrow { }{ }{ } {5}{3}{ } { }{ }{8}
    \setrow { }{2}{5} { }{ }{ } {3}{ }{ }

    % 示例高亮
    \highlightrectangle{1}{4}{3}{6}
\end{tikzpicture}
\end{document}
```
````

## 有候选数数独