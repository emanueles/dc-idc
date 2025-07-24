# Repositório da Disciplina de Divulgação Científica

Para adicionar a sua página ao repositório, você vai primeiro fazer um fork desse repositório para o seu usuário no github. 

Depois vai criar uma pasta dentro da pasta `content/post` com o nome `equipeXX`, seguindo a numeração abaixo:

## Equipes

equipe01: 
 - Caio Passos, Felipe Bomfim e Pedro Henrique
  
equipe02: 
 - Amir, Antonio Irineu, Carlos Eduardo e João Luca

equipe03: 
 - Adriane, Luiz Gustavo e Victor Gabriel

equipe04: 
 - Adilio, Kauã e Mateus Sousa

equipe05: 
 - Ayuri, Isaack e Michael Cauan

equipe06: 
 - Arthur Wagner, Eduardo Cardoso, Francisco Alexandre e Wesely Yan

equipe07: 
 - Carlos Henrriky, Francisco Arley, Juan Victor e Vinicius

equipe08: 
 - Alison, Larissa, Patricia e Sandy

equipe09: 
 - Gustavo Albuquerque, João Igor, Maria Eduarda e Missara Lisia

equipe10: 
 - Arthur Tome, Maria Leticia, Nikelly e Victor Lucio

equipe11: 
 - Eduardo Rodrigues, Emanuel Victor, Felipe dos Reis e Paulo Gustavo

equipe12: 
 - Gisele, Julio Gabriel e Samuel

equipe13: 
 - Caik e Rogerio

equipe14: 
 - Francisco Renan, José Enilson, Kelvin e Victor Pena

equipe15: 
 - Caio Rubem, Gleidstony, Mateus Walraven e Tamires.

## O que fazer
Dentro da pasta `equipeXX` você vai adicionar um arquivo chamado `index.md`. Veja o exemplo `content/post/exemplo/index.md`, para ter uma ideia do conteúdo. 

Você deve alterar o preâmbulo do `index.md` de acordo com os dados da sua postagem:

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
Você deve adicionar os links para o vídeo no Youtube e para o episódio do podcast. O áudio do podcast no formato mp3 e a imagem da capa do episódio podem ser adicionados à pasta da postagem.

> **Atenção:** O arquivo de áudio não pode ter mais de 50 MB. Mais do que isso, você terá que hospedar em outro lugar.


Depois você vai fazer o commit das alterações e fazer um push (se estiver trabalhando localmente) para o seu repositório e solicitar um Git Pull Request das alterações, como mostrado em sala. 

