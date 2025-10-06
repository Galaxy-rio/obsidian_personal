---
title: <% tp.file.title %>
author:
cover:
translator:
sub-title:
original-title:
ISBN:
created: <% tp.file.creation_date("YYYY-MM-DD HH:mm:ss") %>
modified: <% tp.file.last_modified_date("YYYY-MM-DD HH:mm:ss") %>
status:
tags:
类别: "[[../Museion|Museion]]"
---

<%*
const cover = tp.frontmatter.cover;
if (cover) {
    tR += `<img src="${cover}" alt="cover">`;
}
%>

# <% tp.file.title %>
