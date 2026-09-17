# Perfil GitHub · Michel Bocchi Junior

Kit para transformar o repositório especial `Michel1412/Michel1412` numa **landing page**. Quatro versões prontas, mesma Action: o último ano de commits vira Block Breaker e Pac-Man.

Escolhe uma, copia por cima do `README.md` do repositório de perfil, sobe, roda a Action uma vez.

---

## Como o README de perfil funciona

O GitHub só usa um README como capa do usuário se **o repositório tiver o mesmo nome do login**:

```text
https://github.com/Michel1412/Michel1412
                         └── repo = login
```

Esse `README.md` é a primeira coisa que aparece em [github.com/Michel1412](https://github.com/Michel1412). Não é um site de verdade: é Markdown sanitizado.

| o GitHub deixa | o GitHub corta |
| --- | --- |
| Markdown, HTML simples (`p`, `img`, `table`, `details`) | JavaScript |
| imagens e SVG (incluindo animação SMIL/CSS **dentro** do SVG) | `style=""` em tags, CSS externo |
| badges, `picture` light/dark, `align="center"` | terminal interativo de verdade |

Por isso a Action [Commit Breaker](https://github.com/marketplace/actions/commit-breaker) não “roda um jogo no Markdown”. Ela **gera um SVG** (o automático joga sozinho no perfil) e um **HTML** (teclado, via GitHub Pages).

---

## O que os bons perfis fazem (e o que copiamos)

Olhei padrões que realmente funcionam como landing, não só como currículo em emoji:

1. **Sessão de terminal** — um `whoami` / `neofetch` falso. O olho lê como sistema, não como texto solto. Referência de abordagem: [terminal-themed profile README](https://vulabs.dev/posts/github-terminal-profile-readme/) e templates tipo [neofetch-profile](https://github.com/jeantimex/neofetch-profile).
2. **Identidade em 5 segundos** — nome, função, empresa, cidade, uma linha de stack. Badges + typing SVG (`readme-typing-svg.demolab.com`).
3. **Um elemento único** — o teu é o Commit Breaker (e tu é o autor do [`commit-craft`](https://github.com/Michel1412/commit-craft)). Quase todo mundo cola o mesmo card de stats. Quase ninguém tem o ano de commits jogável.
4. **Stats vivos** — `github-readme-stats`, streak, top langs, activity graph. São imagens que atualizam sozinhas; não precisa de token se for só repo público.
5. **Prova de vida** — empresa, faculdade, repos. Recrutador não quer poesia, quer *onde você trabalha* e *o que você shippa*.

As versões usam o mesmo esqueleto: hero → about → **jogo do ano** → stats → stack → PlugLead / faculdade → contato. Muda o *skin*. A **4** é a mescla da 1 com a 2 (terminal Linux + grass block 3D no boot).

---

## As versões

Arquivos em [`versoes/`](./versoes/). São READMEs **completos** — não são rascunho. Copia um deles para a raiz do repo de perfil e renomeia para `README.md`.

| | **1 · Linux TTY** | **2 · Minecraft** | **3 · WhatsApp / PlugLead** | **4 · Linux + Grass Block** |
| --- | --- | --- | --- | --- |
| arquivo | [`versoes/01-linux-tty.md`](./versoes/01-linux-tty.md) | [`versoes/02-minecraft.md`](./versoes/02-minecraft.md) | [`versoes/03-pluglead-whatsapp.md`](./versoes/03-pluglead-whatsapp.md) | [`versoes/04-linux-steve.md`](./versoes/04-linux-steve.md) |
| vibe | `neofetch` + `systemctl` + Tux | inventário, advancements, SMP | conversa no WhatsApp + tmux | boot Linux com **bloco de grama 3D** no lugar do Tux |
| tema do jogo | `ciano` → `dist/ciano/` | `minecraft` → `dist/minecraft/` | `verde` → `dist/verde/` | `minecraft` → `dist/minecraft/` |
| stats | tokyonight | chartreuse / merko green | merko + verde WhatsApp | tokyonight (TTY) + jogo Minecraft |
| melhor se você quer | perfil “dev Linux” clássico | o mais gamer | PlugLead na frente | **mescla 1+2** — currículo + overworld |
| risco | terminal genérico | informal demais pra RH | parece produto | um pouco mais longo |

**Recomendação atual:** versão **4**. É a 1 com o grass block no boot, stack completa (Go, Redis Streams, k8s, pagamentos, Railway), side quest @RedeNerd / Chelzinho, e o fechamento que você pediu.

As versões citam, de propósito:

- **Linux** e programação (Java, Node, Go, Spring, Docker, Kubernetes, Redis Streams, GitHub Actions)
- **Minecraft** (hobby / tema da Action / nick Chelzinho / @RedeNerd)
- **WhatsApp** (domínio do produto)
- **[PlugLead.com](https://pluglead.com)** — 2+ anos (2024 → hoje)
- **Engenharia de Software**, formatura **2026**

---

## Como publicar (passo a passo)

### 1. Repositório de perfil

No GitHub: **New repository** → nome **exato** `Michel1412` → Public → cria o README inicial se quiser.

Este projeto (`perfil-tecnico`) pode ser o próprio repo de perfil, ou você copia os arquivos para lá.

### 2. Escolher a versão

Na raiz do repo de perfil:

```bash
# exemplo: Linux + Grass Block (mescla 1+2)
cp versoes/04-linux-steve.md README.md
```

No Windows (PowerShell):

```powershell
Copy-Item .\versoes\04-linux-steve.md .\README.md
```

### 3. Workflow da Action

O arquivo [`.github/workflows/commit-breaker.yml`](./.github/workflows/commit-breaker.yml) já gera **os três temas**, todo dia às 08:00 UTC, e também no `push` em `main` e no botão **Run workflow**.

Usa a Action pública:

```yaml
uses: Michel1412/commit-craft@v2
```

Inputs importantes (documentação no [Marketplace](https://github.com/marketplace/actions/commit-breaker)):

| input | aqui | efeito |
| --- | --- | --- |
| `github_user_name` | `github.repository_owner` | calendário **do usuário** no último ano |
| `extension` | `block-breaker` / `pac-man` | qual jogo |
| `out_dir` | `dist/ciano`, `dist/minecraft`, `dist/verde` | um tema por pasta |
| `theme` | `ciano` · `minecraft` · `verde` | paleta |
| `source` | default `user` | GitHub inteiro, não só este repo |

Cada README aponta só para a pasta do tema dele. Você pode deixar os três `dist/` no repo mesmo usando uma versão só — não atrapalha.

### 4. Primeira geração

1. Commit e push de `README.md` + workflow + pastas `dist/*/`.
2. Aba **Actions** → **commit-breaker** → **Run workflow**.
3. Quando o job terminar, `dist/<tema>/block-breaker.svg` e `pac-man.svg` entram no repo. O README para de mostrar imagem quebrada.

O cron cuida dos dias seguintes. Sem commit visual, o job sai sem push vazio.

### 5. Teclado público (opcional, mas vale)

**Settings → Pages → Deploy from a branch → `main` → `/ (root)`**.

Os jogos ficam em:

```text
https://Michel1412.github.io/Michel1412/dist/ciano/block-breaker.html
https://Michel1412.github.io/Michel1412/dist/minecraft/block-breaker.html
https://Michel1412.github.io/Michel1412/dist/verde/block-breaker.html
```

(e os pares `pac-man.html`). Os READMEs já linkam isso. Sem Pages, o SVG continua aparecendo; o clique abre o HTML como arquivo no GitHub, não como jogo.

---

## O que cada bloco do README está fazendo

Isso vale para as três versões — para você editar sem quebrar o layout.

```text
hero (typing SVG + badges)
  → quem é em uma linha

bloco de identidade (ASCII / chat / neofetch)
  → personalidade

Commit Breaker (SVG local)
  → o ano, jogável

github-readme-stats + streak + langs + graph
  → números que atualizam sozinhos

skillicons.dev
  → stack visível em um glance

PlugLead + faculdade + repos
  → prova

links
  → GitHub, pluglead.com, LinkedIn, Instagram
```

Widgets usados (todos via `<img>`, sem token):

- [Commit Breaker / commit-craft](https://github.com/Michel1412/commit-craft)
- [readme-typing-svg](https://github.com/DenverCoder1/readme-typing-svg)
- [github-readme-stats](https://github.com/anuraghazra/github-readme-stats)
- [github-readme-streak-stats](https://github.com/DenverCoder1/github-readme-streak-stats)
- [github-readme-activity-graph](https://github.com/Ashutosh00710/github-readme-activity-graph)
- [skillicons](https://skillicons.dev)
- [shields.io](https://shields.io)
- [komarev visitor counter](https://github.com/antonkomarev/github-profile-views-counter)

---

## Ajustes que você provavelmente vai querer

Abre a versão escolhida e troca o que estiver genérico:

- **LinkedIn / Instagram** — já apontam para os que achei (`michel-junior-275127272`, `@_bocchi_michel`). Confere se são esses mesmo.
- **E-mail** — não coloquei de propósito. Adiciona um badge `mailto:` se quiser.
- **Stack** — a v4 já traz Go, Redis, Kubernetes, Railway e APIs de pagamento. Ajuste se faltar Postgres, NX, etc.
- **Só um jogo** — apaga o `<p>` do Pac-Man (ou do Breaker) no README. A Action pode continuar gerando os dois.
- **Só um tema** — no workflow, deixa só o par `extension` + `out_dir` da versão escolhida. Fica mais rápido.
- **Repos em destaque** — na v4: `commit-craft`, `DEA-blog`, `damas`, `games_api`.

---

## Estrutura deste repo

```text
.
├── README.md                          ← landing do perfil (versão 4)
├── GUIA.md                            ← este guia
├── .github/workflows/commit-breaker.yml
├── assets/
│   └── grass-block.ascii              ← ASCII do bloco de grama 3D no boot
├── dist/
│   ├── ciano/                         ← SVG/HTML depois da Action
│   ├── minecraft/
│   └── verde/
└── versoes/
    ├── 01-linux-tty.md
    ├── 02-minecraft.md
    ├── 03-pluglead-whatsapp.md
    └── 04-linux-steve.md
```

O `README.md` da raiz **já é a versão 4**. Este arquivo (`GUIA.md`) fica como documentação do kit.
