# Upstream Chopp — Second Brain

Vault compartilhado de produto entre Bruno e Gui. Contém projetos, tasks, contexto e pesquisa do time.

---

## Pré-requisitos

| Ferramenta | Instalação |
|---|---|
| **Cursor** | [cursor.com](https://cursor.com) |
| **Git** | pré-instalado no macOS |
| **Obsidian** *(opcional)* | [obsidian.md/download](https://obsidian.md/download) — para navegar o vault visualmente |

---

## Setup inicial (fazer uma vez)

### 1. Configurar SSH para a org ambev

```bash
ssh-keygen -t ed25519 -C "seu-email" -f ~/.ssh/id_ed25519_ambev -N ""
```

Adicione a chave pública em: **github.com → Settings → SSH keys**

```bash
cat ~/.ssh/id_ed25519_ambev.pub
```

Configure o host SSH (`~/.ssh/config`):

```
Host github-ambev
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_ed25519_ambev
```

Teste a conexão:

```bash
ssh-keyscan github.com >> ~/.ssh/known_hosts
ssh -T git@github-ambev
# Hi Segantinb-ambev! You've successfully authenticated...
```

### 2. Clonar o repositório com submodules

```bash
git clone --recurse-submodules git@github-ambev:Segantinb-ambev/upstream_chopp.git
cd upstream_chopp
```

Se já clonou sem a flag:

```bash
git submodule update --init --recursive
```

### 3. Abrir no Cursor

Abra a pasta `upstream_chopp` no Cursor. As skills do projeto já estarão disponíveis automaticamente.

---

## Estrutura do vault

```
tasks/          — Tasks com due date
projects/       — Projetos com next actions
  <slug>/
    index.md    — Status, next action
    context.md  — Contexto do projeto
context/        — Perfis de contexto para o LLM
outputs/        — Entregáveis (docs, HTMLs, decks)
research/       — Transcrições e pesquisas brutas
ideas/          — Ideias capturadas
.cursor/skills/ — Skills disponíveis no Cursor
```

---

## Trabalho colaborativo

**Regra principal: sempre faça pull antes de editar.**

```bash
git pull origin main
```

**Depois de editar:**

```bash
git push origin main
```

Se o push rejeitar (alguém pushiou antes), faça pull primeiro:

```bash
git pull origin main
git push origin main
```

### Divisão de responsabilidade sugerida

| Área | Responsável |
|---|---|
| `tasks/` | Bruno |
| `projects/*/index.md` | Bruno (status e next action) |
| `projects/*/context.md` | Ambos |
| `context/research-*` | Ambos |
| `outputs/` | Ambos (nomes com datas evitam conflito) |

---

## Skills disponíveis

| Skill | Quando usar |
|---|---|
| `work-today` | Plano do dia com tasks e projetos ativos |
| `work-capture` | Capturar tasks, projetos, notas |
| `project-status` | Atualizar next action ou status de um projeto |
| `weekly-review` | Resumo semanal — o que foi feito, bloqueios, próxima semana |
| `git-sync` | Push, pull, histórico, rollback |
| `lipe` | Skill de design do time (submodule) |

Para usar uma skill, basta pedir em linguagem natural no Cursor:
> "atualiza o status do projeto régua de aniversário"
> "gera o plano de hoje"
> "push para o Bruno"

---

## Git como histórico

Cada alteração gera um commit automático com prefixo `cos:`.

```bash
# Ver histórico geral
git log --oneline -20

# Ver histórico de um arquivo
git log --oneline -- projects/regua-aniversario-inapp/index.md

# Ver como estava um arquivo antes
git show abc1234:projects/regua-aniversario-inapp/index.md
```

---

## Atualizar skills externas

A skill LIPE vem do repositório do time de design como submodule. Para pegar atualizações:

```bash
git submodule update --remote .cursor/skills/lipe
git add .cursor/skills/lipe
git commit -m "cos: update Skill-LIPE"
git push
```
