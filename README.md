# AVANT Docs
Documentação e tutoriais que compõem a base de conhecimento da AVANT.

## Como contribuir

Os documentos e tutoriais neste site são escritos em Markdown. Caso não conheça, Markdown é uma linguagem de marcação muito fácil de utilizar, por isso, o escolhemos! Para aprender a utilizar, visite este [site](https://www.markdownguide.org/).

Esse site é um repositório como qualquer outro. Então, para contribuir, basta

1) Clonar o repositório

```
git clone git@github.com:Eletronica-AVANT-UFMG/avantdocs.git
```

2) Fazer as melhorias que deseja

3) Criar um [pull request](https://docs.github.com/en/pull-requests)

Uma vez que suas mudanças sejam aprovadas, serão integradas ao repositório.

### Observações importantes
Lembre-se de guardar os arquivos de documentação na pasta `docs` para manter o repositório organizado!

Todo arquivo precisa de um cabeçalho (frontmatter) no início. O cabeçalho vai ser algo parecido com isso

```
--- # Não esqueça desses '---'!
layout: default
title: Títutlo do Documento
nav_order: [ordem que vai aparecer no menu]
--- # Aqui também
```

Há muitas outras configurações possíveis. Para mais detalhes, visite a documentação do Jekyll: [frontmatter](https://jekyllrb.com/docs/front-matter/), ou use os arquivos já existentes como exemplo.
