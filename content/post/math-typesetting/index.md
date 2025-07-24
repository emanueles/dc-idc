---
title: Textos Matemáticos
description: Textos matemáticos usando KaTeX
date: 2025-07-23 00:00:00+0000
math: true
---

Stack possui suporte integrado para textos matemáticos usando [KaTeX](https://katex.org/).

**Não é habilitado por padrão em todas as páginas,** mas você pode habilitá-lo para postagens individuais adicionando `math: true` à matéria principal. Ou você pode habilitá-lo em todas as páginas adicionando `math = true` à seção `params.article` em `config.toml`.

## Matemática em linha

Esta é uma expressão matemática em linha: $\varphi = \dfrac{1+\sqrt5}{2}= 1.6180339887…$

```markdown
$\varphi = \dfrac{1+\sqrt5}{2}= 1.6180339887…$
```

## Blocos matemáticos

$$
    \varphi = 1+\frac{1} {1+\frac{1} {1+\frac{1} {1+\cdots} } } 
$$

```markdown
$$
    \varphi = 1+\frac{1} {1+\frac{1} {1+\frac{1} {1+\cdots} } } 
$$
```

$$
    f(x) = \int_{-\infty}^\infty\hat f(\xi)\,e^{2 \pi i \xi x}\,d\xi
$$

```markdown
$$
    f(x) = \int_{-\infty}^\infty\hat f(\xi)\,e^{2 \pi i \xi x}\,d\xi
$$
```