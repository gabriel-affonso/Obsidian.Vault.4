---
date: 2024-11-28
hora: 12:36
tags:
---

# Livros Lidos
```dataview
TABLE date AS "Data", autor AS "Autor", ano AS "Ano", nota AS "Nota"
FROM "Leiturinhas"
WHERE date AND autor AND ano 
WHERE contains(status, "Lido")
SORT date DESC
```

# Livros para Ler

```dataview
TABLE date AS "Data", autor AS "Autor", ano AS "Ano", status 
FROM "Leiturinhas"
WHERE date AND autor AND ano 
WHERE contains(status, "Ler")
SORT date DESC
```
