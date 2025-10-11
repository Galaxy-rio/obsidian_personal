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

## 简单数独

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

## 复杂数独

要在正文中添加具有候选数、高亮、连线的数独，使用 TikZ 代码块：

````markdown
```tikz
\begin{document}
\tikzset{
    biggrid/.style={very thick, black},
    cell/.style={minimum width=1cm, minimum height=1cm, anchor=center},
    digit/.style={font=\bfseries\Large},
    hint/.style={font=\scriptsize, black!70}
}

% === 坐标换算：将 row, col 转为坐标 ===
\newcommand{\cellpos}[2]{%
    % #1=row (1–9), #2=col (1–9)
    \pgfmathsetmacro{\x}{(#2-1)*3}
    \pgfmathsetmacro{\y}{(9-#1)*3}
}

% === 绘制整盘 ===
\newcommand{\drawboard}{
    % 外框
    \draw[step=3cm, very thin, black!50] (0,0) grid (27,27);
    % 粗线（每3格加粗）
    \foreach \i in {0,9,18,27}{
        \draw[biggrid] (\i,0)--(\i,27);
        \draw[biggrid] (0,\i)--(27,\i);
    }
}

% === 设置候选数 ===
\newcommand{\setcandidates}[3]{%
    % #1=row, #2=col, #3={候选数字列表，如 1,3,7}
    \cellpos{#1}{#2}
    \begin{scope}[shift={(\x,\y)}]
        \foreach \n in {1,...,9} {
            \pgfmathtruncatemacro{\xx}{mod(\n-1,3)}
            \pgfmathtruncatemacro{\yy}{2-floor((\n-1)/3)}
            % 检查 \n 是否在列表中
            \foreach \m in {#3} {
                \ifnum\n=\m
                    \node[hint] at (0.5+\xx,0.5+\yy) {\n};
                \fi
            }
        }
    \end{scope}
}

% === 设置主数字 ===
\newcommand{\setdigit}[3]{%
    \cellpos{#1}{#2}
    \node[digit] at (\x+1.5,\y+1.5) {#3};
}

% === 高亮矩形 ===
\newcommand{\highlightrectangle}[5]{%
    % #1,#2 = 左上角 row,col
    % #3,#4 = 右下角 row,col
    % #5 = 颜色和深浅（如 red!30、blue!20、yellow!40 等）
    \cellpos{#1}{#2}  % 左上角
    \pgfmathsetmacro{\xA}{\x}
    \pgfmathsetmacro{\yA}{\y+3} % 上边缘 +3
    \cellpos{#3}{#4}  % 右下角
    \pgfmathsetmacro{\xB}{\x+3}
    \pgfmathsetmacro{\yB}{\y}   % 下边缘
    \fill[fill=#5, opacity=0.5, rounded corners=0.5mm] (\xA+0.15,\yB+0.15) rectangle (\xB-0.15,\yA-0.15);
}

% === 高亮候选数（圆角矩形） ===
\newcommand{\highlightcandidate}[4]{%
    % #1=row, #2=col, #3={候选数字列表，如 1,3,7}, #4=颜色
    \cellpos{#1}{#2}
    \begin{scope}[shift={(\x,\y)}]
        \foreach \n in {#3} {
            % 计算候选数在3×3格内的位置
            \pgfmathtruncatemacro{\xx}{mod(\n-1,3)}
            \pgfmathtruncatemacro{\yy}{2-floor((\n-1)/3)}
            % 绘制标记方块
            \fill[fill=#4, opacity=1, rounded corners=0.5mm]
                (0.15+\xx, 0.15+\yy) rectangle (0.85+\xx, 0.85+\yy);
        }
    \end{scope}
}

\newcommand{\linkcandidates}[8]{%
    % #1,#2,#3 = 起点 row,col,候选数
    % #4,#5,#6 = 终点 row,col,候选数
    % #7 = 颜色
    % #8 = 线型 ("solid" or "dashed")
    % 计算起点坐标
    \cellpos{#1}{#2}%
    \pgfmathtruncatemacro{\xA}{mod(#3-1,3)}%
    \pgfmathtruncatemacro{\yA}{2-floor((#3-1)/3)}%
    \pgfmathsetmacro{\xApos}{\x+0.5+\xA}%
    \pgfmathsetmacro{\yApos}{\y+0.5+\yA}%

    % 计算终点坐标
    \cellpos{#4}{#5}%
    \pgfmathtruncatemacro{\xB}{mod(#6-1,3)}%
    \pgfmathtruncatemacro{\yB}{2-floor((#6-1)/3)}%
    \pgfmathsetmacro{\xBpos}{\x+0.5+\xB}%
    \pgfmathsetmacro{\yBpos}{\y+0.5+\yB}%

    % 一行绘制：将样式 (#8) 直接放进去；颜色 (#7) 与透明度固定为0.5
    \draw[#7, opacity=0.5, line width=1.5pt, #8] (\xApos,\yApos) -- (\xBpos,\yBpos);
}


\begin{tikzpicture}[scale=0.4]
    % 高亮区域
    \highlightrectangle{4}{2}{6}{8}{red!20}
    \highlightrectangle{2}{4}{8}{6}{blue!20}

    % 绘制棋盘
    \drawboard

    % 主数字
    \setdigit{1}{3}{9}
    \setdigit{1}{7}{2}
    \setdigit{1}{8}{6}
    \setdigit{2}{1}{2}
    \setdigit{2}{5}{8}
    \setdigit{2}{6}{4}

    % 强弱链
    \linkcandidates{4}{5}{1}{4}{5}{3}{red!80}{solid}
    \linkcandidates{4}{5}{5}{5}{5}{5}{red!80}{dashed}

    % 高亮候选数
    \highlightcandidate{5}{5}{4,8}{blue!30}
    \highlightcandidate{4}{5}{1,5,3}{red!30}
    \highlightcandidate{5}{5}{5}{red!30}

    % 候选数
    \setcandidates{4}{5}{1,3,5,7}
    \setcandidates{5}{5}{2,4,5,8,9}

\end{tikzpicture}
\end{document}
```
````
