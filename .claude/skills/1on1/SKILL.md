---
name: 1on1
description: Generate 1:1 agenda with manager from weekly activity and active projects.
---

# /1on1 - Pauta do 1:1 com Gestor

Gera a pauta do 1:1 semanal consolidando o que foi feito na semana, projetos ativos e pontos para discutir.

## Steps

1. Determine a semana atual (segunda a domingo)
2. **Atividade da semana via git log:**
   ```bash
   git log --since="last monday" --grep="cos:" --oneline
   ```
3. **Tarefas concluídas na semana:** grep por `status: complete` nos arquivos de tasks modificados desde segunda
4. **Projetos ativos:** grep `status: active` em `projects/*/index.md`, ler cada um
5. **Tarefas pendentes/atrasadas** relevantes para discutir com gestor (due esta semana ou overdue)
6. Gerar output com pauta estruturada
7. Salvar em `outputs/YYYY-MM-DD-1on1.md` linkado à task `1-1-gestor.md`

## Sensitive Files

Para projetos com `sensitive: true`, usar apenas nome e next action do frontmatter — não ler corpo do arquivo além da seção `## Next Action`.

## Output Format

```markdown
---
type: output
date: YYYY-MM-DD
tags: [1:1, gestor]
---

# Pauta 1:1 — DD/MM/YYYY

## O que fiz essa semana
- Item 1 (projeto/contexto)
- Item 2

## Status dos projetos ativos
- **Projeto A** — next: próxima ação
- **Projeto B** — next: próxima ação

## Pontos para discutir
- [ ] Item que precisa de decisão ou alinhamento
- [ ] Blocker ou dependência

## Pendências / Atrasado
- Item overdue relevante (se houver)
```

## Notas

- Focar no que é relevante para o gestor — evitar detalhes operacionais
- "Pontos para discutir" deve ter no máximo 3-4 itens de maior impacto
- Se não houver nada overdue relevante, omitir a seção
