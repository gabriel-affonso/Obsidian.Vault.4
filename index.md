---
date: 2024-11-27
tags: 
visibilidade: Público
---

# Índice de Notas

## Coisas
- [Índice Geral](https://gabriel-affonso.github.io/Obsidian.Vault.4/Coisas/Aleatoriedade/Índice%20Geral)
- [Orçamento Novembro](https://gabriel-affonso.github.io/Obsidian.Vault.4/Coisas/Semanas/Novembro%202024.md)
  - [Semana 1](https://gabriel-affonso.github.io/Obsidian.Vault.4/Coisas/Semanas/Novembro%202024/Novembro%20Semana%201)
  - [Semana 2](https://gabriel-affonso.github.io/Obsidian.Vault.4/Coisas/Semanas/Novembro%202024/Novembro%20Semana%202)
  - [teste1](https://gabriel-affonso.github.io/Obsidian.Vault.4/Nota.teste)

## Memórias, Silêncios e Heterodoxias
- [Informações Gerais](https://gabriel-affonso.github.io/Obsidian.Vault.4/Memórias,%20Silêncios%20e%20Heterodoxias/!nformações%20Gerais%20-%20Memórias%20Silêncios%20e%20Heterodoxias)

## Pensamentos
- [Índice de Pensamentos](https://gabriel-affonso.github.io/Obsidian.Vault.4/Pensamentos/Índice%20de%20Pensamentos)

## Pessoas
- [Índice de Pessoas](https://gabriel-affonso.github.io/Obsidian.Vault.4/Pessoas/!Índice%20Pessoas)

## Poética e Cidadania
- [Informações Gerais](https://gabriel-affonso.github.io/Obsidian.Vault.4/Poética%20e%20Cidadania/!nformações%20Gerais-Poética%20e%20Cidadania)

## Template
- [Índice Template](https://gabriel-affonso.github.io/Obsidian.Vault.4/Template/Índice%20Template)
















```dataview
TABLE date AS "Data", file.folder AS "Pasta"
WHERE contains(visibilidade, "Público")
SORT file.folder ASC, date ASC

```

Aqui está uma lista de todas as notas disponíveis:

<ul>
  {% for page in site.pages %}
    {% assign url_fixed = page.url | prepend: site.baseurl %}
    <li><a href="{{ url_fixed }}">{{ page.title | default: page.name }}</a></li>
  {% endfor %}
</ul>


Abaixo estão os links para todas as suas notas:

{% assign baseurl = site.baseurl %}
<ul>
{% for file in site.static_files %}
  {% if file.extname == ".md" %}
    <li><a href="{{ baseurl }}{{ file.path }}">{{ file.basename | escape }}</a></li>
  {% endif %}
{% endfor %}
</ul>


# Índice Novo

Aqui está uma lista de todas as notas disponíveis (novas):

<ul>
  {% for page in site.pages %}
    <li><a href="https://gabriel-affonso.github.io/Obsidian.Vault.4{{ page.url }}">{{ page.title | default: page.name }}</a></li>
  {% endfor %}
</ul>


