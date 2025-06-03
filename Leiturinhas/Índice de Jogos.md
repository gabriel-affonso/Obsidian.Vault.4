---
date: 2025-05-20
hora: 15:59
tags:
---





```dataview
TABLE date AS "Data", console AS "Console", nota AS "Nota"
FROM "Jogos"
WHERE date AND console 
WHERE contains(status, "Terminado")
WHERE contains(media, "Jogo")
SORT date DESC
```

```dataview
TABLE date, fim, console, nota
FROM ""
WHERE contains(tags, "Jogo") AND contains(status, "Terminado")
SORT date DESC
```
```dataview
TABLE date, fim, console, nota
FROM ""
WHERE contains(tags, "Jogo") AND contains(status, "Jogando")
SORT date DESC
```
