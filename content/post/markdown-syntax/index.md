---
title: Guia de Sintaxe Markdown
date: 2025-07-23
description: Artigo de exemplo mostrando a sintaxe básica do Markdown e a formatação para elementos HTML.
tags: 
    - markdown
    - css
    - html
---

Este artigo oferece um exemplo de sintaxe básica do Markdown que pode ser usada em arquivos de conteúdo do Hugo e também mostra se elementos HTML básicos são decorados com CSS em um tema do [Hugo](https://gohugo.io/).

<!--more-->

## Cabeçalhos

Os seguintes elementos HTML `<h1>`—`<h6>` representam seis níveis de títulos de seção. `<h1>` é o nível de seção mais alto, enquanto `<h6>` é o mais baixo.

# H1
## H2
### H3
#### H4
##### H5
###### H6

## Parágrafo

Xerum, quo qui aut unt expliquam qui dolut labo. Aque venitatiusda cum, voluptionse latur sitiae dolessi aut parist aut dollo enim qui voluptate ma dolestendit peritin re plis aut quas inctum laceat est volestemque commosa as cus endigna tectur, offic to cor sequas etum rerum idem sintibus eiur? Quianimin porecus evelectur, cum que nis nust voloribus ratem aut omnimi, sitatur? Quiatem. Nam, omnis sum am facea corem alique molestrunt et eos evelece arcillit ut aut eos eos nus, sin conecerem erum fuga. Ri oditatquam, ad quibus unda veliamenimin cusam et facea ipsamus es exerum sitate dolores editium rerore eost, temped molorro ratiae volorro te reribus dolorer sperchicium faceata tiustia prat.

Itatur? Quiatae cullecum rem ent aut odis in re eossequodi nonsequ idebis ne sapicia is sinveli squiatum, core et que aut hariosam ex eat.

## Citações

O elemento citação representa conteúdo citado de outra fonte, opcionalmente com uma referência que deve estar dentro de um elemento `footer` ou `cite` e, opcionalmente, com alterações em linha, como anotações e abreviações.

### Citação sem atribuição

> Tiam, ad mint andaepu dandae nostion secatur sequo quae.
> **Note** que você pode usar a *sintaxe Markdown* dentro de uma citação.

### itação sem atribuição

> Don't communicate by sharing memory, share memory by communicating.<br>
> — <cite>Rob Pike[^1]</cite>

### Citação usando shortcode

{{< quote author="A famous person" source="The book they wrote" url="https://en.wikipedia.org/wiki/Book">}}
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.
{{< /quote >}}

[^1]: A citação acima foi obtida da [palestra de Rob Pike](https://www.youtube.com/watch?v=PAAkCSZUG1c) durante o Gopherfest, em 18 de novembro de 2015.

## Tabelas

As tabelas não fazem parte da especificação principal do Markdown, mas o Hugo oferece suporte imediato a elas.

   Name | Age
--------|------
    Bob | 27
  Alice | 23

### Markdown dentro de tabelas

| Italics   | Bold     | Code   |
| --------  | -------- | ------ |
| *italics* | **bold** | `code` |

| A                                                        | B                                                                                                             | C                                                                                                                                    | D                                                 | E                                                          | F                                                                    |
|----------------------------------------------------------|---------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------|------------------------------------------------------------|----------------------------------------------------------------------|
| Lorem ipsum dolor sit amet, consectetur adipiscing elit. | Phasellus ultricies, sapien non euismod aliquam, dui ligula tincidunt odio, at accumsan nulla sapien eget ex. | Proin eleifend dictum ipsum, non euismod ipsum pulvinar et. Vivamus sollicitudin, quam in pulvinar aliquam, metus elit pretium purus | Proin sit amet velit nec enim imperdiet vehicula. | Ut bibendum vestibulum quam, eu egestas turpis gravida nec | Sed scelerisque nec turpis vel viverra. Vivamus vitae pretium sapien |

## Blocos de código
### Blocos de código com aspas simples invertidas

```html
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title>Example HTML5 Document</title>
</head>
<body>
  <p>Test</p>
</body>
</html>
```

### Blocos de código indentado com 4 espaços

    <!doctype html>
    <html lang="en">
    <head>
      <meta charset="utf-8">
      <title>Example HTML5 Document</title>
    </head>
    <body>
      <p>Test</p>
    </body>
    </html>

### Bloco de código de diff

```diff
[dependencies.bevy]
git = "https://github.com/bevyengine/bevy"
rev = "11f52b8c72fc3a568e8bb4a4cd1f3eb025ac2e13"
- features = ["dynamic"]
+ features = ["jpeg", "dynamic"]
```

### Bloco de código de uma linha

```html
<p>A paragraph</p>
```

## Tipos de Listas

### Lista Ordenada

1. Primeiro item
2. Segundo item
3. Terceiro item

### Lista Não Ordenada

* Um item
* Outro item
* E ainda outro item

### Lista aninhada

* Frutas
  * Maçã
  * Laranja
  * Banana
* Laticínios
  * Leite
  * Queijo

## Outros Elementos — abbr, sub, sup, kbd, mark

<abbr title="Graphics Interchange Format">GIF</abbr> é um formato bitmap de imagem.

H<sub>2</sub>O

X<sup>n</sup> + Y<sup>n</sup> = Z<sup>n</sup>

Pressione <kbd>CTRL</kbd> + <kbd>ALT</kbd> + <kbd>Delete</kbd> para finalizar a sessão.

A maioria das <mark>salamandras</mark> são noturnas, e caçam insetos, vermese outras criaturas pequenas.