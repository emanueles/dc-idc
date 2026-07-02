# Repositório da Disciplina de Divulgação Científica

Este é o repositório "hub" do site: contém o tema, o layout e a configuração do Hugo. O
conteúdo de cada semestre **não** fica aqui — cada semestre é um repositório próprio, importado
como [Hugo Module](https://gohugo.io/hugo-modules/) e montado em `content/post/<semestre>/` na
hora do build. Isso existe para que você não precise baixar o conteúdo (áudio/vídeo pesado) de
semestres anteriores só para enviar a sua postagem.

**Se você é aluno da disciplina, não faça fork deste repositório.** Vá direto para a seção
"Semestre atual" abaixo.

## Semestre atual: 2026.1

O repositório do semestre atual é [`emanueles/dc-idc-2026.1`](https://github.com/emanueles/dc-idc-2026.1).
É **nele** que você faz fork, edita e abre o Pull Request — veja o passo a passo completo em
[`guia-pull-request.md`](https://github.com/emanueles/dc-idc-2026.1/blob/master/guia-pull-request.md),
no próprio repositório `dc-idc-2026.1`.

A lista de equipes deste semestre está em
[`EQUIPES.md`](https://github.com/emanueles/dc-idc-2026.1/blob/master/EQUIPES.md), no próprio
repositório `dc-idc-2026.1`. Consulte esse arquivo para saber o número da sua equipe.

## O que fazer

1. Faça um fork de [`emanueles/dc-idc-2026.1`](https://github.com/emanueles/dc-idc-2026.1) para
   o seu usuário no GitHub — veja o passo a passo completo em
   [`guia-pull-request.md`](guia-pull-request.md).
2. No seu fork, a pasta da sua equipe **já existe** na raiz do repositório (`equipeXX/`, com um
   `index.md` de template dentro) — não crie uma pasta nova, isso evita erro de nome. Abra a
   pasta com o número da sua equipe (veja `EQUIPES.md`) e edite o `index.md` que já está lá.
3. O `index.md` já vem com o `slug` e a estrutura corretos — veja
   [`content/post/exemplo/index.md`](content/post/exemplo/index.md) (neste repositório, o hub)
   se quiser um exemplo de postagem completa para se inspirar.

Altere o preâmbulo do `index.md` de acordo com os dados da sua postagem:

```
---
title: Título do Post                     # <- Altere o título
description: Breve descrição da postagem  # <- Altere a descrição
slug: equipeXX-temaprincipal              # <- Só troque "temaprincipal", mantenha o prefixo
date: 2026-01-01 00:00:00+0000            # <- Coloque a data do dia que inseriu o conteúdo
image: cover.jpg                          # <- Nome do arquivo de imagem com a capa (adicione à pasta)
categories:
    - Post                                # <- Deixe como está
tags:
    - Tema do Vídeo                       # <- Altere para o tema do vídeo
    - Tema do Podcast                     # <- Altere para o tema do episódio. Se for igual ao de cima, remova essa linha
weight: 1                                 # <- Deixe como está
draft: true                               # <- IMPORTANTE: troque para false (ou apague a linha) quando terminar
---
```

Você deve adicionar os links para o vídeo no YouTube e para o episódio do podcast. O áudio do
podcast (mp3) e a imagem da capa do episódio podem ser adicionados à pasta da postagem.
**Sem tirar o `draft: true`, a postagem não aparece no site publicado.**

> **Atenção:** arquivos de áudio/vídeo são versionados via Git LFS no repositório `dc-idc-2026.1`
> (veja o `.gitattributes` dele). Ainda assim, prefira exportar o podcast em mono e taxa de bits
> moderada (96–128 kbps) — isso mantém o clone leve para todo mundo.

Para ver como fica uma postagem **completa**, de verdade (não só o template), veja o exemplo de
uma equipe do semestre anterior:
[`equipe01/index.md` em `dc-idc-2025.1`](https://github.com/emanueles/dc-idc-2025.1/blob/master/equipe01/index.md).

Depois, faça o commit das alterações, o push para o seu fork de `dc-idc-2026.1` e abra um Pull
Request **para `emanueles/dc-idc-2026.1`**, como detalhado em
[`guia-pull-request.md`](https://github.com/emanueles/dc-idc-2026.1/blob/master/guia-pull-request.md).
**O Pull Request é o que conta como entrega** — commits que ficam só no seu computador não
chegam até o professor.

## Estrutura (para referência — só relevante para quem mantém o hub)

```
dc-idc/                     # este repositório (hub): tema, layout, config
  content/post/
    2025.1/                 # NÃO existe como pasta local — vem do módulo dc-idc-2025.1
    2026.1/                 # NÃO existe como pasta local — vem do módulo dc-idc-2026.1
    exemplo/                # post de referência (draft, não publicado)
    markdown-syntax/        # referência de sintaxe do tema (draft, não publicado)
    math-typesetting/       # referência de fórmulas matemáticas (draft, não publicado)
  config/_default/module.toml  # imports dos módulos de cada semestre
  guia-pull-request.md         # aponta para a cópia real em dc-idc-2026.1
  docs/
    equipes-2025.1.md          # lista de equipes de 2025.1 (semestre encerrado)
    equipes-2026.1.md          # aponta para EQUIPES.md em dc-idc-2026.1

dc-idc-2025.1/               # repositório separado — conteúdo do semestre 2025.1
dc-idc-2026.1/               # repositório separado — conteúdo do semestre atual (alunos fazem fork aqui)
  EQUIPES.md                  # lista de equipes do semestre atual
  guia-pull-request.md         # guia completo (cópia real, mantida aqui)
```
