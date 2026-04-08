---
name: weekly-review
description: Generate or update the weekly work summary. Use when the user asks for a weekly review, end of week summary, what was accomplished this week, or weekly retrospective. Creates weekly/YYYY-WNN.md with delivered work, blockers, and next week's priorities.
---

# weekly-review — Revisão Semanal de Trabalho

Cria ou atualiza `weekly/YYYY-WNN.md` com um resumo consolidado da semana profissional.

## Calcular a semana

```bash
# Número da semana ISO
date +%G-W%V  # ex: 2026-W14

# Início e fim da semana (segunda a sexta)
date -v-Mon +%Y-%m-%d  # início
date -v-Fri +%Y-%m-%d  # fim
```

## Passos

1. **Ler** `context/business-profile.md` (prioridades do quarter)
2. **Calcular** semana ISO atual e período (segunda–sexta)
3. **Verificar** se `weekly/YYYY-WNN.md` existe — se sim, ler
4. **Buscar atividade git da semana**:
   ```bash
   git log --since="last Monday" --until="now" --grep="cos:" --format="%ad %s" --date=short
   ```
5. **Buscar tasks concluídas esta semana**:
   ```bash
   grep -l "status: complete" tasks/*.md | xargs grep -l "environment: work"
   ```
6. **Ler projetos ativos de trabalho** para capturar próximas ações
7. **Criar ou atualizar** o arquivo semanal
8. **Commit**

## Output

```markdown
---
type: weekly
environment: work
week: YYYY-WNN
period: YYYY-MM-DD to YYYY-MM-DD
---

## Entregues
- ✅ O que foi concluído com impacto real

## Em Andamento
- **Projeto X** — status atual, próxima ação
- **Projeto Y** — status atual, próxima ação

## Travado / Bloqueado
- Item ou projeto parado e o motivo

## Aprendizados
- Padrões ou insights da semana

## Prioridades da Próxima Semana
1. Ação mais importante
2. Segunda prioridade
3. Terceira prioridade

## Atividade (git log)
- commits cos: da semana
```

## Commit

```bash
git add weekly/YYYY-WNN.md
git commit -m "cos: weekly summary - YYYY-WNN"
```
