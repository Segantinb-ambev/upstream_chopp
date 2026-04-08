---
name: work-today
description: Generate today's work plan including sensitive tasks, active work projects, and professional priorities. Use when the user asks for their work plan, work agenda, what to focus on today, or a combined view of work tasks and projects.
---

# work-today — Plano de Trabalho do Dia

Gera o plano do dia com foco em trabalho, incluindo tasks e projetos sensíveis que o Claude Code não processa.

## Passos

1. **Ler** `context/business-profile.md` para entender prioridades atuais
2. **Verificar** se `daily/YYYY-MM-DD.md` já existe — se sim, ler e complementar
3. **Buscar tasks de trabalho** por data:
   ```bash
   # Tasks de hoje (work)
   grep -l "due: YYYY-MM-DD" tasks/*.md | xargs grep -l "environment: work"

   # Overdue (work)
   grep -l "due: YYYY-MM-D[0-9]" tasks/*.md | xargs grep -l "environment: work"
   ```
4. **Ler apenas os arquivos encontrados** — nunca glob all tasks
5. **Buscar projetos ativos de trabalho**:
   ```bash
   grep -l "status: active" projects/*.md | xargs grep -l "environment: work"
   ```
6. **Checar atividade recente**:
   ```bash
   git log --since="midnight" --grep="cos:" --oneline
   ```
7. **Criar ou atualizar** `daily/YYYY-MM-DD.md`
8. **Commit**

## Comportamento ao Atualizar

Quando o daily já existe:
- Manter `[x]` de itens completos
- Manter itens pessoais que o Claude Code criou
- Adicionar tasks de trabalho que não estão presentes
- Atualizar a seção de projetos com next actions atuais

## Output

```markdown
---
type: daily
date: YYYY-MM-DD
environment: work
---

## Trabalho — Hoje
- [ ] Tasks de trabalho com due date de hoje

## Trabalho — Overdue
- [ ] Tasks atrasadas (X dias)

## Projetos Ativos
- **Nome do Projeto** — próxima ação: [next action do arquivo]

## Prioridades do Quarter
- [da seção Priorities do business-profile]

## Atividade Recente
- commits cos: desde meia-noite
```

## Commit

```bash
git add daily/YYYY-MM-DD.md
git commit -m "cos: daily plan for YYYY-MM-DD"
```
