# Plano de reorganização do repositório dc-idc

Análise feita em 2026-07-02 sobre o estado atual do repositório e proposta de mudanças para (1) suportar posts de vários semestres sem quebrar o tema/site e (2) evitar que alunos precisem baixar o conteúdo de semestres anteriores.

## Status (atualizado em 2026-07-02)

Decisões confirmadas:
- Semestre existente: **2025.1**. Novo semestre em preparação: **2026.1**.
- Estratégia para o Objetivo 2: **Opção B** (um repositório por semestre, importado como Hugo Module pelo repo hub).
- Branch padrão real do repositório: **`master`**.
- Áudio/vídeo acima de 50 MB: usar **Git LFS** em vez da regra rígida de hospedagem externa — o GitHub Free/Pro agora inclui 10 GB de storage e 10 GB de banda de LFS por mês, o que cobre os ~450 MB/semestre com folga (fonte: [GitHub Docs — Git LFS billing](https://docs.github.com/billing/managing-billing-for-git-large-file-storage/about-billing-for-git-large-file-storage)).

O que já foi feito nesta sessão (só estrutura de arquivos local, sem tocar em git/GitHub — a pasta montada não tinha `.git`, então nenhum commit foi feito):
- `content/post/equipeXX` (15 equipes) movido para `content/post/2025.1/equipeXX`; `Equipe03` renomeado para `equipe03`.
- Criada `content/post/2026.1/` (vazia, pronta para os novos PRs).
- `exemplo`, `markdown-syntax` e `math-typesetting` marcados com `draft: true` (deixam de aparecer no site publicado, mas continuam acessíveis como referência).
- Lista de equipes tirada do `README.md` e movida para `docs/equipes-2025.1.md` (+ `docs/equipes-2026.1.md` vazio); `README.md` reescrito para ser genérico entre semestres.
- `guia-pull-request.md` adicionado ao repositório com a branch corrigida de `main` para `master` e caminho de pasta atualizado para `content/post/2026.1/equipeXX`.
- `.gitattributes` criado na raiz, rastreando `*.mp3 *.mp4 *.mpeg *.mpg *.wav *.mov` via Git LFS (ainda não ativado — precisa do `git lfs install` no ambiente real, ver abaixo).

## Próximos passos (dependem da sua conta GitHub — não executados aqui)

Estes comandos devem ser rodados no seu terminal local, onde o `.git` e as credenciais do GitHub existem de verdade.

**1. Levar a reorganização atual para o repositório único existente**, antes de qualquer split:

```bash
cd dc-idc
git add -A
git commit -m "Reorganiza posts por semestre, prepara guia e LFS para 2026.1"
git push origin master
```

**2. Ativar o Git LFS e migrar os áudios já commitados** (equipe10: 87 MB, equipe11: 54 MB, equipe15: ~49 MB, e os demais) para não pesarem no histórico:

```bash
git lfs install
git lfs migrate import --include="*.mp3,*.mp4,*.mpeg,*.mpg,*.wav,*.mov" --everything
git push --force origin master   # reescreve histórico — avise quem tiver clones/forks
```

**3. Quando estiver pronto para o split em repositórios por semestre (Opção B):**

```bash
# Cria o histórico isolado de cada semestre a partir da pasta correspondente
git subtree split --prefix=content/post/2025.1 -b split-2025.1
git subtree split --prefix=content/post/2026.1 -b split-2026.1

# Crie os repositórios vazios dc-idc-2025.1 e dc-idc-2026.1 no GitHub, depois:
git push git@github.com:emanueles/dc-idc-2025.1.git split-2025.1:master
git push git@github.com:emanueles/dc-idc-2026.1.git split-2026.1:master
```

Em cada repositório novo, rode `hugo mod init github.com/emanueles/dc-idc-2025.1` (e o equivalente para 2026.1) para virarem Hugo Modules válidos. **Importante:** esse comando roda dentro de um clone separado do repositório novo, não dentro da pasta do hub (`dc-idc`) — ele cria um `go.mod` na raiz de onde for executado, e essa raiz precisa ser o repo do semestre:

```bash
cd ..                                              # sai da pasta do hub (dc-idc)
git clone git@github.com:emanueles/dc-idc-2025.1.git
cd dc-idc-2025.1
hugo mod init github.com/emanueles/dc-idc-2025.1
git add go.mod go.sum
git commit -m "Inicializa dc-idc-2025.1 como Hugo Module"
git push origin master
```

Repita para `dc-idc-2026.1` numa pasta irmã separada. Ao final você terá três pastas lado a lado, cada uma com seu próprio `.git`: `dc-idc/` (hub), `dc-idc-2025.1/` e `dc-idc-2026.1/`.

No repo hub (`dc-idc`), adicione os imports em `config/_default/module.toml`:

```toml
[[imports]]
path = "github.com/emanueles/dc-idc-2025.1"
[[imports.mounts]]
source = "content/post"
target = "content/post/2025.1"

[[imports]]
path = "github.com/emanueles/dc-idc-2026.1"
[[imports.mounts]]
source = "content/post"
target = "content/post/2026.1"
```

Depois disso, remova os arquivos reais de `content/post/2025.1` e `content/post/2026.1` do repo hub (eles passam a vir dos módulos importados) e rode `hugo mod get -u` sempre que quiser puxar a versão mais recente de cada semestre antes do deploy.

Aviso a cada novo semestre: criar o repositório `dc-idc-<semestre>`, atualizar o `module.toml` do hub, e trocar o link do `guia-pull-request.md` para apontar para o novo repositório (upstream deixa de ser `emanueles/dc-idc` e passa a ser `emanueles/dc-idc-<semestre>`).

## 1. Diagnóstico do estado atual

**Estrutura de conteúdo.** Todos os posts ficam soltos em `content/post/equipeXX`, sem nenhuma marcação de semestre. Não há como saber, olhando a pasta, se `equipe01` é de 2025.2 ou 2026.1 — e no próximo semestre a numeração `equipeXX` vai colidir com a do semestre anterior (o time atual também terá um `equipe01`).

**Inconsistência de nomes.** Existe `content/post/Equipe03` (E maiúsculo) misturado com `equipe01`, `equipe02` etc. (minúsculo). É provavelmente um erro de um PR passado que não seguiu o guia — hoje isso não quebra o Hugo, mas mostra que não há validação automática do nome da pasta.

**Conteúdo de exemplo misturado com posts reais.** `content/post/exemplo`, `content/post/markdown-syntax` e `content/post/math-typesetting` (do tema) ficam dentro da mesma pasta que os posts dos alunos. Isso não quebra o site, mas confunde quem navega pela pasta pela primeira vez e polui a listagem de posts se algum aluno esquecer de definir `draft: true`.

**Tamanho do conteúdo.** `content/post` já soma **453 MB** com apenas 15 equipes em um semestre — principalmente áudio de podcast e alguns vídeos. Dois arquivos já estão perto do limite rígido de 100 MB por arquivo do GitHub (`equipe10`: 87 MB, `equipe11`: 54 MB). O guia de PR já orienta os alunos a hospedar áudio fora do repositório acima de 50 MB, mas isso não é validado automaticamente e alguns times já passaram do combinado. Sem mudança de estrutura, cada novo semestre soma mais ~450 MB ao histórico do repositório — em poucos anos o clone completo fica na casa dos gigabytes.

**Tema.** O tema (`hugo-theme-stack`) já é importado como Hugo Module (`go.mod` + `config/_default/module.toml`), então ele em si não é um obstáculo para múltiplos semestres — o tema só lista o que estiver em `content/post`, não importa a profundidade de subpastas. O ponto real de atenção não é o tema, é a ausência de uma taxonomia/seção por semestre para organizar e filtrar os posts (hoje só existem `categories` — usado só como "Post" — e `tags`, usados por tema do episódio).

**Workflow de deploy.** `.github/workflows/deploy.yml` dispara em push/PR para a branch `master`. O `guia-pull-request.md` (novo, orientando os alunos) refere-se à branch `main` em todos os exemplos de comando (`git push origin main`, `base: main`). Isso precisa ser conferido contra a branch padrão real do repositório no GitHub — se for `main`, o workflow está desatualizado e PRs mesclados não vão disparar o deploy.

**Guia de PR.** O `guia-pull-request.md` já está correto e completo para o fluxo fork → commit → push → PR. Não precisa mudar por causa da reorganização, só é preciso confirmar o nome da branch (ver ponto acima) e, se a estrutura de pastas mudar, atualizar o passo que manda criar `content/post/equipeXX` para o novo caminho.

## 2. Objetivo 1 — suportar múltiplos semestres na mesma estrutura

Proposta: nomear a pasta por semestre e manter as equipes dentro dela.

```
content/post/
  2025-2/
    equipe01/
    equipe02/
    ...
  2026-1/
    equipe01/
    equipe02/
    ...
```

Isso resolve a colisão de nomes entre semestres, deixa claro visualmente a que turma cada post pertence, e não exige nenhuma mudança na URL pública dos posts — `permalinks.toml` já define `post = "/p/:slug/"`, ou seja, o link final depende do campo `slug` do front matter, não do caminho da pasta. Basta orientar os alunos a manterem `slug` único (ex.: `equipeXX-tema`, como o README já pede).

Para poder filtrar/listar por semestre no próprio site (e não só organizar a pasta), o front matter de cada post pode ganhar um campo `semestre: "2026-1"`, transformado em taxonomia do Hugo. Isso é opcional — não é necessário para o site funcionar, mas melhora a navegação (ex.: um widget "arquivos por semestre" na home).

Ações concretas:
- Mover as pastas atuais para `content/post/2025-2/equipeXX` (confirmar comigo o identificador exato do semestre em que essas 15 equipes cursaram — usei `2025-2` como placeholder).
- Renomear `Equipe03` → `equipe03` no mesmo movimento.
- Mover `exemplo`, `markdown-syntax` e `math-typesetting` para fora de `content/post` (ex.: `exampleContent/` na raiz, fora do build) ou marcá-los com `draft: true` e um aviso no nome, para não aparecerem como posts reais.
- Atualizar `guia-pull-request.md` e `README.md` para instruir a criação da pasta em `content/post/<semestre>/equipeXX`.
- (Opcional) Adicionar taxonomia `semestre` em `config/_default/config.toml` e um widget de arquivo por semestre no `params.toml`.

## 3. Objetivo 2 — alunos não baixarem semestres anteriores

Aqui existem duas soluções de níveis bem diferentes. Recomendo decidirmos juntos qual faz sentido para o tempo que você tem disponível para manter isso.

### Opção A — sparse-checkout / clone parcial (rápida, dentro do repositório atual)

Mantém um único repositório, mas ensina o aluno a clonar só o necessário:

```bash
git clone --filter=blob:none --no-checkout https://github.com/SEU-USUARIO/dc-idc.git
cd dc-idc
git sparse-checkout init --cone
git sparse-checkout set content/post/2026-1 config layouts static assets
git checkout main
```

Isso baixa a árvore de arquivos completa (nomes/caminhos), mas só materializa em disco os blobs das pastas listadas — os áudios/vídeos de semestres antigos não são baixados. É uma mudança de **guia**, não de infraestrutura: dá pra fazer ainda essa semana, sem criar repositórios novos. A limitação é que o fork no GitHub continua "contendo" todo o histórico (embora isso não pese no armazenamento do aluno) e o repositório principal continua crescendo ~450 MB por semestre indefinidamente — ainda vale considerar Git LFS ou hospedagem externa de mídia em algum momento.

### Opção B — modularização de verdade, um repositório por semestre (mais trabalho, resolve o problema pela raiz)

Já que o tema é importado via Hugo Modules, o mesmo mecanismo pode ser usado para o conteúdo: cada semestre vira um repositório Hugo Module próprio (só com os posts daquele semestre), e o repositório principal (`dc-idc`) importa todos eles via `[[module.imports]]` com `mounts` apontando para `content/post/<semestre>`.

```
dc-idc (repo "hub")               → tema, layouts, config, deploy
dc-idc-2025-2 (repo por semestre) → só os posts de 2025.2
dc-idc-2026-1 (repo por semestre) → só os posts de 2026.1
```

Os alunos do semestre atual fazem fork **só** de `dc-idc-2026-1` — um repositório pequeno (dezenas de MB, não centenas), sem histórico de semestres anteriores. O repositório `dc-idc` (hub) faz `hugo mod get` para buscar a versão mais recente de cada módulo de semestre e builda o site completo no deploy.

Isso resolve os dois objetivos ao mesmo tempo: cada semestre é isolado (sem colisão de nomes, sem crescimento do repo que os alunos tocam) e o site consegue combinar todos eles automaticamente no build.

Custo: você precisa criar um repositório novo no GitHub a cada semestre, atualizar o `module.toml` do hub com o import do novo módulo, e o guia de PR passa a apontar para um repositório diferente a cada oferta da disciplina (o `guia-pull-request.md` atual cita `emanueles/dc-idc` como upstream fixo — isso mudaria para `emanueles/dc-idc-2026-1`, por exemplo). Também é preciso decidir como disparar o rebuild do hub quando um PR é mesclado no repositório de um semestre (webhook/Action no repo do semestre chamando `repository_dispatch` no hub, ou simplesmente rodar `hugo mod get -u` manualmente antes de cada aula/entrega).

### Comparação rápida

| | Opção A (sparse-checkout) | Opção B (multi-repo via Hugo Modules) |
|---|---|---|
| Esforço de implementação | Baixo (só documentação) | Médio/alto (repos novos + CI) |
| Resolve crescimento do repo principal | Não, só adia | Sim |
| Resolve confusão de nomes entre semestres | Sim (com a mudança do Objetivo 1) | Sim |
| Manutenção recorrente por semestre | Nenhuma além da pasta | Criar repo + atualizar import + garantir rebuild |
| Risco de erro do aluno | Médio (comando de clone incomum, fácil esquecer) | Baixo (fork simples, repo já pequeno) |

Minha recomendação: aplicar o Objetivo 1 (pastas por semestre) agora, que é barato e já melhora a organização; usar a Opção A como solução imediata para este semestre; e migrar para a Opção B quando/se o repositório principal começar a incomodar em tamanho (ele ainda está longe do limite de 5 GB do GitHub, mas os arquivos individuais de 87 MB já estão perto do limite de 100 MB por arquivo).

## 4. Decisão final e status

Resolvido em 2026-07-02 (ver seção "Status" no topo deste arquivo): Opção B escolhida, branch `master` confirmada, LFS adotado para mídia. A reorganização de arquivos (Objetivo 1) e a preparação de `.gitattributes`/documentação já foram feitas localmente nesta sessão. Falta apenas a parte que depende da sua conta GitHub: commit/push da reorganização, migração dos áudios já commitados para LFS, e — quando decidir seguir adiante — a criação dos repositórios `dc-idc-2025.1` e `dc-idc-2026.1` e os imports no `module.toml` do hub (comandos detalhados na seção "Próximos passos" no topo deste arquivo).

Antes de abrir PR com essas mudanças estruturais, rode `hugo server` localmente para confirmar que nenhum post quebrou com os novos caminhos.
