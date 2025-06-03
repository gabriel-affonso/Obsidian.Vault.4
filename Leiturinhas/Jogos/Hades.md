---
date: 2025-06-01
hora: 21:25
tags:
  - Jogo
console: Switch
nota:
  - ⭐⭐⭐⭐⭐
status:
  - Terminado
media: Jogo
---




TABLE date AS "Data", console AS "Console", nota AS "Nota"
FROM "Jogos"
WHERE date AND console AND ano 
WHERE contains(status, "Terminado")
WHERE contains(media, "Jogo")
SORT date DESC
```