---
date: 2024-11-27
tags: 
visibilidade: Público
---


```dataview
TABLE date AS "Data", file.folder AS "Pasta"
WHERE contains(visibilidade, "Público")
SORT file.folder ASC, date ASC

```



