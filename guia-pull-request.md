# Guia: como enviar sua postagem usando Fork e Pull Request

Este guia explica, passo a passo, como contribuir com o repositório da disciplina do jeito
correto. O erro mais comum é fazer as alterações **apenas no seu computador** e achar que a
entrega foi feita. Não foi. Enquanto você não **enviar (push)** as alterações e **abrir um
Pull Request**, ninguém consegue ver o seu trabalho.

Leia a seção de conceitos e depois siga **um** dos dois caminhos: pelo navegador (mais simples,
bom para arquivos pequenos) ou pela linha de comando (necessário para o áudio, que pode passar
de 25 MB).

---

## 1. Os conceitos em uma frase cada

- **Repositório original (upstream):** o repositório da disciplina, `emanueles/dc-idc`. Você
  **não** tem permissão para alterá-lo diretamente.
- **Fork:** uma cópia do repositório original feita **na sua conta** do GitHub. É nela que
  vocês trabalham.
- **Clone:** trazer o repositório da nuvem (GitHub) para o seu computador, para editar os
  arquivos localmente.
- **Commit:** registrar um conjunto de alterações, com uma mensagem que descreve o que mudou.
  Um commit fica só no seu computador até você fazer o push.
- **Push:** enviar os commits do seu computador para o seu fork no GitHub.
- **Pull Request (PR):** o pedido formal de "por favor, incorpore as minhas alterações no
  repositório original". **É este o passo que conta como entrega.**

O fluxo completo é sempre:

```
Fork  →  (editar)  →  Commit  →  Push  →  Pull Request
```

Se qualquer um dos últimos três passos faltar, a entrega não chegou ao destino.

---

## 2. Passo comum: fazer o fork (uma vez por equipe)

1. Acesse o repositório original: `https://github.com/emanueles/dc-idc`
2. Clique no botão **Fork**, no canto superior direito.
3. Confirme a criação do fork. Agora existe uma cópia em `github.com/SEU-USUARIO/dc-idc`.

> Apenas **uma pessoa** da equipe precisa fazer o fork. As outras podem ser adicionadas como
> colaboradoras desse fork (em *Settings → Collaborators*) ou contribuir por outros meios
> combinados pela equipe.

Depois do fork, siga um dos dois caminhos abaixo.

---

## 3. Caminho A — pelo navegador (arquivos até 25 MB)

Bom para textos, imagens e o `README`. **Não serve** para o áudio se ele passar de 25 MB.

1. Entre no **seu fork** (`github.com/SEU-USUARIO/dc-idc`), e não no repositório original.
2. Para editar um arquivo existente: abra o arquivo e clique no ícone de **lápis** (Edit).
3. Para adicionar um arquivo (imagem da capa, por exemplo): clique em **Add file → Upload files**
   e arraste os arquivos.
4. Ao terminar cada mudança, role até **Commit changes**, escreva uma mensagem curta e clara
   (ex.: "Adiciona capa do podcast em 1024x1024") e confirme.
5. Quando **todas** as alterações estiverem no seu fork, abra o Pull Request (seção 5).

---

## 4. Caminho B — pela linha de comando (necessário para o áudio, até 100 MB)

Use se o `.mp3` passar de 25 MB, ou se preferir trabalhar no terminal.

**4.1. Clonar o seu fork para o computador**

```bash
git clone https://github.com/SEU-USUARIO/dc-idc.git
cd dc-idc
```

**4.2. Editar e adicionar os arquivos**

Crie a pasta da sua equipe em `content/post/2026.1/equipeXX` (veja o `README.md` para o passo a
passo do conteúdo), coloque a imagem da capa e o arquivo de áudio na pasta, conforme as
instruções da atividade.

**4.3. Registrar as alterações (commit)**

```bash
git add .
git commit -m "Adiciona postagem: texto, capa e áudio do podcast"
```

Você pode fazer vários commits, um para cada etapa. Mensagens descritivas ajudam na nota.

**4.4. Enviar para o seu fork (push)**

```bash
git push origin master
```

> Confira o nome da branch principal do seu fork antes de rodar o comando (`git branch`). A
> branch padrão deste repositório é `master`; se o seu fork usar `main`, troque na linha acima.

**4.5. Conferir**

Abra `github.com/SEU-USUARIO/dc-idc` no navegador. Os arquivos e as mensagens de commit devem
estar lá. Se estiverem, o push funcionou. Agora falta o Pull Request.

---

## 5. Passo final e obrigatório: abrir o Pull Request

Este é o passo que a turma anterior esqueceu. **Sem ele, a atividade não foi entregue.**

1. Vá até o **seu fork** no GitHub.
2. Clique na aba **Pull requests** e depois em **New pull request**.
3. Confirme que a comparação está assim:
   - **base repository:** `emanueles/dc-idc`  → **base:** `master`
   - **head repository:** `SEU-USUARIO/dc-idc` → **compare:** `master`

   Ou seja: as suas alterações (head) indo **para** o repositório da disciplina (base).
4. Clique em **Create pull request**.
5. Escreva um **título** (ex.: "Postagem — Equipe [nome/nomes]") e uma **descrição** com o
   nome dos integrantes e um resumo do que foi enviado.
6. Clique em **Create pull request** novamente para confirmar.

Pronto. Se aparecer a página do PR com o seu título e a lista de commits, a entrega chegou.

---

## 6. Como saber se deu certo

A entrega está correta se **todas** as afirmações abaixo forem verdadeiras:

- [ ] Existe um fork em `github.com/SEU-USUARIO/dc-idc`.
- [ ] Os arquivos (texto, capa e áudio) aparecem **no fork**, no site do GitHub — não só no seu
      computador.
- [ ] Existe um Pull Request **aberto para** `emanueles/dc-idc`.
- [ ] O PR tem título e descrição com o nome da equipe.

Se você só vê as alterações no seu computador (VS Code, pasta local) mas não no site do GitHub,
faltou o **push**. Se vê no seu fork no GitHub mas não há Pull Request, faltou o **passo 5**.

---

## 7. Problemas comuns

- **"Fiz tudo, mas o professor não vê nada."** Você provavelmente parou no commit local. Rode
  `git push` e depois abra o Pull Request.
- **"Meu arquivo de áudio foi recusado."** Acima de 25 MB, use a linha de comando (Caminho B).
  O limite pelo terminal é 100 MB.
- **"Abri o Pull Request no repositório errado."** Feche esse PR e abra um novo garantindo que
  a **base** é `emanueles/dc-idc`.
- **"Aparece 'conflito' no Pull Request."** Avise a equipe e o professor; normalmente resolve-se
  atualizando o fork antes de reenviar.
