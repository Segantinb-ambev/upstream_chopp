---
name: git-sync
description: Sync the second brain vault with GitHub. Use when the user asks to push, pull, sync, share with Gui, send to GitHub, get updates from Gui, check what's pending to push, check git status, view file history, see past versions, or roll back a file or the vault to a previous state. Also use when the user says "git", mentions GitHub, or asks "como estava antes", "voltar para versão anterior", "histórico de alterações".
---

# git-sync — Sincronização com GitHub

Sincroniza o vault com o repositório `Segantinb-ambev/upstream_chopp` via SSH.

## Status — ver o que está pendente

```bash
cd /Users/bruno.segantin/Documents/Personal/second-brain-main

# Commits locais ainda não enviados ao GitHub
git log origin/main..HEAD --oneline

# Arquivos modificados mas não commitados
git status --short
```

Mostre o resultado ao usuário de forma resumida:
- Quantos commits não foram enviados
- Quais arquivos têm mudanças locais sem commit

## Pull — pegar atualizações do Gui

Sempre rode pull antes de trabalhar para pegar mudanças que o Gui fez:

```bash
cd /Users/bruno.segantin/Documents/Personal/second-brain-main
git pull origin main
```

Se houver conflito, liste os arquivos conflitantes e peça orientação antes de resolver.

## Push — enviar para o GitHub

```bash
cd /Users/bruno.segantin/Documents/Personal/second-brain-main
git push origin main
```

Após o push, confirme: quantos commits foram enviados e quais arquivos foram incluídos.

## Fluxo completo (pull + push)

Quando o usuário pedir "sync" ou "sincronizar":

1. `git pull origin main` — pega mudanças do Gui
2. Se houver novidades, mostre o que chegou
3. `git push origin main` — envia mudanças locais
4. Se houver novidades, mostre o que foi enviado

## Lembrete pós-edição

Sempre que criar ou editar arquivos no vault, verifique:

```bash
git log origin/main..HEAD --oneline | wc -l
```

Se o resultado for maior que 0, adicione ao final da resposta:

> **GitHub:** X commit(s) pendente(s) de push. Quer enviar agora? (`/push`)

## Histórico — ver o que mudou

```bash
VAULT=/Users/bruno.segantin/Documents/Personal/second-brain-main

# Histórico geral (últimos 20 commits)
git -C $VAULT log --oneline -20

# Histórico de um arquivo específico
git -C $VAULT log --oneline -- <caminho/do/arquivo.md>

# Ver o que mudou em um commit específico
git -C $VAULT show <hash>

# Ver o conteúdo de um arquivo em uma data/commit passado
git -C $VAULT show <hash>:<caminho/do/arquivo.md>

# Ver o que mudou em um arquivo entre hoje e N dias atrás
git -C $VAULT log --since="7 days ago" --oneline -- <caminho/do/arquivo.md>
```

Quando o usuário perguntar sobre histórico de um arquivo, primeiro liste os commits que o afetaram com datas legíveis:
```bash
git -C $VAULT log --pretty=format:"%h %ad %s" --date=short -- <arquivo>
```

## Rollback — voltar para versão anterior

**Ver uma versão antiga sem alterar nada** (apenas leitura):
```bash
git -C $VAULT show <hash>:<caminho/do/arquivo.md>
```
Mostre o conteúdo ao usuário e pergunte se quer restaurar.

**Restaurar um arquivo para uma versão anterior:**
```bash
git -C $VAULT checkout <hash> -- <caminho/do/arquivo.md>
git -C $VAULT commit -m "cos: revert <arquivo> para versão de <data>"
```

**Antes de restaurar, sempre:**
1. Mostre o conteúdo da versão antiga para o usuário confirmar
2. Execute o checkout e commit só após confirmação explícita
3. Faça push para o Gui ver a reversão

**Nunca use `git reset --hard`** — prefira `revert` ou `checkout` de arquivo específico para não perder histórico.

## Atalhos que o usuário pode usar

| Comando | Ação |
|---------|------|
| `/push` | Enviar commits pendentes para o GitHub |
| `/pull` | Pegar atualizações do Gui |
| `/sync` | Pull + Push completo |
| `/status` | Ver o que está pendente |
| `/history <arquivo>` | Ver histórico de alterações de um arquivo |
| `/rollback <arquivo>` | Restaurar um arquivo para versão anterior |
