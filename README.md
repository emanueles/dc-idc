# Repositório da Disciplina de Divulgação Científica

Este repositório reúne, semestre a semestre, os posts produzidos pelos alunos da disciplina de
Introdução à Divulgação Científica. Cada semestre tem sua própria pasta dentro de
`content/post`, e a lista de equipes de cada semestre fica em `docs/equipes-<semestre>.md`.

## Semestre atual: 2026.1

A lista de equipes deste semestre está em [`docs/equipes-2026.1.md`](docs/equipes-2026.1.md).
Consulte esse arquivo para saber o número da sua equipe.

## O que fazer

1. Faça um fork deste repositório para o seu usuário no GitHub — veja o passo a passo completo em
   [`guia-pull-request.md`](guia-pull-request.md).
2. Crie uma pasta dentro de `content/post/2026.1/` com o nome `equipeXX`, usando o número da sua
   equipe (ex.: `content/post/2026.1/equipe01`).
3. Dentro dessa pasta, adicione um arquivo chamado `index.md`. Veja o exemplo em
   `content/post/exemplo/index.md` para ter uma ideia do conteúdo.

Altere o preâmbulo do `index.md` de acordo com os dados da sua postagem:

```
---
title: Exemplo de Post                    # <- Altere o título
description: Veja um exemplo de postagem  # <- Altere a descrição
slug: exemplo-post                        # <- Altere o slug com equipeXX-temaprincipal
date: 2025-07-24 00:00:00+0000            # <- Coloque a data do dia que inseriu o conteúdo
image: cover.jpg                          # <- Nome do arquivo de imagem com a capa (adicione à pasta)
categories:
    - Post                                # <- Deixe como está
tags:
    - Template                            # <- Remova essa linha
    - Visualização de Dados               # <- Altere para o tema do vídeo
    - Matemática Computacional            # <- Altere para o tema do episódio. Se for igual ao de cima, remova essa linha
weight: 1                                 # <- Deixe como está
---
```

Você deve adicionar os links para o vídeo no YouTube e para o episódio do podcast. O áudio do
podcast (mp3) e a imagem da capa do episódio podem ser adicionados à pasta da postagem.

> **Atenção:** arquivos de áudio/vídeo são versionados via Git LFS neste repositório (veja
> `.gitattributes`). Ainda assim, prefira exportar o podcast em mono e taxa de bits moderada
> (96–128 kbps) — isso mantém o clone do repositório leve para todo mundo.

Depois, faça o commit das alterações, o push para o seu fork e abra um Pull Request, como
detalhado em [`guia-pull-request.md`](guia-pull-request.md). **O Pull Request é o que conta como
entrega** — commits que ficam só no seu computador não chegam até o professor.

## Estrutura do repositório

```
content/post/
  2025.1/           # posts do semestre 2025.1 (arquivo, não editar)
  2026.1/           # posts do semestre atual — é aqui que sua equipe trabalha
  exemplo/          # post de referência (draft, não publicado)
  markdown-syntax/  # referência de sintaxe do tema (draft, não publicado)
  math-typesetting/ # referência de fórmulas matemáticas (draft, não publicado)
docs/
  equipes-2025.1.md # lista de equipes do semestre 2025.1
  equipes-2026.1.md # lista de equipes do semestre atual
```
