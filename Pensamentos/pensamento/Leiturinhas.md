---
date: 2024-10-03
tags:
---

```dataview
TABLE date AS "Data", nota AS "Nota", autor AS "Autor"
FROM "Poética e Cidadania"
WHERE date AND autor AND nota
SORT date DESC
```