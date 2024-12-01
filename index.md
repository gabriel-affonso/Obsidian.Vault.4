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


Abaixo estão os links para todas as suas notas:

{% assign baseurl = site.baseurl %}
<ul>
{% for file in site.static_files %}
  {% if file.extname == ".md" %}
    <li><a href="{{ baseurl }}{{ file.path }}">{{ file.basename | escape }}</a></li>
  {% endif %}
{% endfor %}
</ul>


# Índice de Notas

## Coisas
- [Índice Geral]({{ site.baseurl }}/Coisas/Aleatoriedade/Índice%20Geral.md)
- [Orçamento Novembro]({{ site.baseurl }}/Coisas/Semanas/Novembro%202024.md)
  - [Semana 1]({{ site.baseurl }}/Coisas/Semanas/Novembro%202024/Novembro%20Semana%201.md)
  - [Semana 2]({{ site.baseurl }}/Coisas/Semanas/Novembro%202024/Novembro%20Semana%202.md)
  - [nota.teste] (/Obsidian.Vault.4/Nota.teste.md)

## Memórias, Silêncios e Heterodoxias
- [Informações Gerais]({{ site.baseurl }}/Memórias,%20Silêncios%20e%20Heterodoxias/!nformações%20Gerais%20%20-%20Memórias%20Silêncios%20e%20Heterodoxias.md)

## Pensamentos
- [Índice de Pensamentos]({{ site.baseurl }}/Pensamentos.md)

## Pessoas
- [Índice de Pessoas]({{ site.baseurl }}/Pessoas/!Índice%20PEssoas.md)

## Poética e Cidadania
- [Informações Gerais]({{ site.baseurl }}/Poética%20e%20Cidadania/!nformações%20Gerais-Poética%20e%20Cidadania.md)

## Template
- [Índice Template]({{ site.baseurl }}/Template/Índice%20Template.md)
