---
name: git-sync
description: Sync the second brain vault with GitHub. Use when the user asks to push, pull, sync, share with Gui, send to GitHub, get updates from Gui, check what's pending to push, or check git status. Also use when the user says "git" or mentions GitHub.
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

## Atalhos que o usuário pode usar

| Comando | Ação |
|---------|------|
| `/push` | Enviar commits pendentes para o GitHub |
| `/pull` | Pegar atualizações do Gui |
| `/sync` | Pull + Push completo |
| `/status` | Ver o que está pendente |
