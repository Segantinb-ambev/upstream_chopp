---
name: project-status
description: Update a work project's status, next action, or notes after a meeting or progress update. Use when the user comes out of a meeting, completes a milestone, changes a project's direction, or wants to update what's blocking or what comes next on a specific project.
---

# project-status — Atualizar Status de Projeto

Atualiza um projeto de trabalho com o estado atual, próxima ação e notas. Ideal para registrar o resultado de reuniões ou avanços.

## Passos

1. **Identificar** o projeto pelo nome ou contexto
2. **Localizar** o arquivo:
   ```bash
   # Buscar por nome aproximado
   ls projects/*.md | grep -i "<termo>"
   ```
3. **Ler** o arquivo atual completo
4. **Atualizar** as seções relevantes:
   - `## Next Action` — substituir pelo novo próximo passo
   - `status:` no frontmatter — se mudou (active | paused | complete | archived)
   - `## Notas` — adicionar contexto da atualização com data
5. **Verificar** se há tasks relacionadas que precisam ser criadas ou fechadas
6. **Commit**

## Frontmatter do Projeto

```yaml
---
type: project
environment: work
status: active | paused | complete | archived
tags: []
sensitive: true
created: YYYY-MM-DD
updated: YYYY-MM-DD  # atualizar sempre
---
```

## Padrão de Atualização de Notas

Sempre adicionar uma entrada datada ao atualizar, não sobrescrever:

```markdown
## Notas

### YYYY-MM-DD
O que aconteceu, decisão tomada, ou por que mudou.

### YYYY-MM-DD (anterior)
...
```

## Quando Criar Tasks Associadas

Se a próxima ação requer uma data ou é delegável, criar uma task separada em `tasks/` e linkar no projeto:

```markdown
## Next Action
[[slug-da-task]]
```

## Status Changes

| Situação | Status |
|----------|--------|
| Ativo, em andamento | `active` |
| Esperando algo externo | `paused` |
| Entregue / encerrado | `complete` |
| Não relevante mais | `archived` |

## Commit

```bash
git add projects/<slug>.md
git commit -m "cos: update project - <slug>"
```
