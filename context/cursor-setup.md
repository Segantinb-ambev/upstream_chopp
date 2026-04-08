---
type: context
---

# Cursor Setup — Second Brain

## Visão Geral

Este vault é compartilhado entre três ferramentas:

- **Obsidian** — leitura e edição visual (local, sem cloud)
- **Cursor** — edição com AI para conteúdo sensível de trabalho (aprovado pelo compliance)
- **Claude Code** — Chief of Staff pessoal, planejamento e captura rápida (conta pessoal, envia para servidores Anthropic)

## Regra de Ouro

> Dados sensíveis de trabalho (clientes, métricas, produto, estratégia) apenas via Cursor.

O Claude Code é conta pessoal — mesmo rodando localmente, o conteúdo é processado nos servidores da Anthropic. Não passar dados confidenciais por ele.

## Divisão de Responsabilidades

### Cursor — Trabalho sensível

Skills disponíveis em `.cursor/skills/`:

| Skill | Quando usar |
|-------|-------------|
| `work-capture` | Capturar tasks, projetos ou pessoas com dados reais de trabalho |
| `update-business-profile` | Atualizar role, prioridades, clientes, stakeholders, ferramentas |
| `work-today` | Plano do dia com tasks e projetos de trabalho (inclusive sensíveis) |
| `weekly-review` | Revisão semanal — entregues, bloqueios, prioridades da próxima semana |
| `project-status` | Atualizar próxima ação, status ou notas de um projeto após reunião |

### Claude Code — Pessoal e planejamento geral

Skills disponíveis em `.claude/skills/`:

| Skill | Quando usar |
|-------|-------------|
| `/today` | Plano do dia com tasks pessoais e projetos não-sensíveis |
| `/new` | Captura rápida de tasks, ideias e notas sem dados sensíveis |
| `/daily-review` | Revisão do dia — planejado vs realizado |
| `/history` | Atividade recente do vault via git log |

## Como os Dados Fluem

```
Cursor escreve → vault (git) → Claude Code e Obsidian leem
```

O vault é o mesmo para todos. O que o Cursor escreve, o Claude Code e o Obsidian leem — sem duplicação, com git como auditoria de tudo.

Arquivos marcados `sensitive: true` existem no vault e o Claude Code os lê **apenas no frontmatter** — título (via filename), `due`, `status` e `tags`. O corpo do arquivo, onde ficam nomes de clientes, métricas e detalhes de produto, nunca é processado pelo Claude.

## Convenções

Seguir os formatos definidos em `.cursorrules` na raiz do vault:
- Todo arquivo tem frontmatter YAML com `type` e `environment`
- `environment: work` para conteúdo profissional
- `sensitive: true` para arquivos com dados confidenciais
- Antes de qualquer tarefa de trabalho, ler `context/business-profile.md`

## Estrutura de Skills do Cursor

```
.cursor/
└── skills/
    ├── work-capture/          # Captura de trabalho sensível
    ├── update-business-profile/  # Manter o contexto de negócio atualizado
    ├── work-today/            # Plano do dia profissional
    ├── weekly-review/         # Revisão semanal
    └── project-status/        # Atualizar projetos após reuniões
```
