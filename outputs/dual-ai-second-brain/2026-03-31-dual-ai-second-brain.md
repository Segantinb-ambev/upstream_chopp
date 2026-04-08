# Dual-AI Second Brain: Claude + Cursor

**Problema**: usar IA para gerenciar um Second Brain pessoal e profissional ao mesmo tempo, sem vazar dados sensíveis de trabalho para servidores externos de uma conta pessoal.

**Solução**: dois agentes com responsabilidades separadas, um vault único como fonte de verdade.

---

## O Problema

Claude Code roda localmente, mas processa conteúdo nos servidores da Anthropic via conta pessoal. Isso é ótimo para tarefas pessoais — mas inviável para dados de trabalho sujeitos a compliance: nomes de clientes, métricas, detalhes de produto, estratégia.

Ao mesmo tempo, o Cursor conecta a modelos via conta corporativa (aprovada pelo time de segurança). É o ambiente certo para trabalho sensível, mas precisava de skills estruturadas para funcionar como Chief of Staff.

---

## A Arquitetura

```
┌─────────────────────────────┐   ┌─────────────────────────────┐
│       CLAUDE CODE           │   │           CURSOR             │
│    (conta pessoal)          │   │      (conta corporativa)     │
│                             │   │                              │
│  Skills:                    │   │  Skills:                     │
│  • /today                   │   │  • work-capture              │
│  • /new                     │   │  • update-business-profile   │
│  • /daily-review            │   │  • work-today                │
│  • /history                 │   │  • weekly-review             │
│                             │   │  • project-status            │
│  Dados: pessoal, não-       │   │                              │
│  sensível, planejamento     │   │  Dados: clientes, métricas,  │
│  geral                      │   │  produto, stakeholders       │
└──────────────┬──────────────┘   └──────────────┬──────────────┘
               │                                  │
               └──────────────┬───────────────────┘
                              ↓
               ┌──────────────────────────┐
               │     VAULT (Obsidian)     │
               │   git como auditoria     │
               │                          │
               │  tasks/   projects/      │
               │  people/  daily/         │
               │  weekly/  ideas/         │
               │  context/ outputs/       │
               └──────────┬───────────────┘
                          ↓
                     Obsidian (leitura)
```

---

## Divisão de Responsabilidades

### O que o Claude Code faz

Planejamento e captura de itens **sem dados confidenciais**.

| Skill | Uso |
|-------|-----|
| `/today` | Plano do dia — tasks pessoais e projetos não-sensíveis |
| `/new` | Captura rápida em linguagem natural |
| `/daily-review` | Revisão do dia — planejado vs realizado |
| `/history` | Atividade recente do vault via git log |

### O que o Cursor faz

Tudo que envolve **dados reais de trabalho**.

| Skill | Uso |
|-------|-----|
| `work-capture` | Captura tasks, projetos e pessoas com nomes reais |
| `update-business-profile` | Mantém `context/business-profile.md` atualizado |
| `work-today` | Plano do dia incluindo tasks e projetos sensíveis |
| `weekly-review` | Revisão semanal — entregues, bloqueios, próxima semana |
| `project-status` | Atualiza próxima ação e notas após reuniões |

---

## Como os Dados Fluem

O vault é o mesmo arquivo para todos. Não há duplicação.

1. **Cursor escreve** um projeto com nome de cliente real → `projects/nome-cliente.md` com `sensitive: true`
2. **Git registra** o commit com `cos: new project - nome-cliente`
3. **Claude Code lê apenas o frontmatter** do arquivo — título (via filename), `due`, `status`, `tags`
4. **O corpo do arquivo nunca é lido pelo Claude** — nomes de clientes, métricas e detalhes de produto ficam protegidos
5. **Obsidian** exibe tudo visualmente, sem enviar nada para lugar nenhum

---

## Convenções do Vault

Todo arquivo tem frontmatter YAML obrigatório:

```yaml
---
type: task | project | person | idea | daily | weekly | context
environment: personal | work
status: pending | in-progress | complete | cancelled   # tasks e projects
sensitive: true                                         # se tiver dados confidenciais
created: YYYY-MM-DDTHH:MM:SS
---
```

### Regra de sensibilidade

Adicionar `sensitive: true` sempre que o arquivo contiver:
- Nomes de clientes reais
- Métricas de negócio
- Detalhes de produto não públicos
- Nomes de stakeholders internos

### O que o Claude lê em arquivos sensitive

| Campo | Claude lê? |
|-------|-----------|
| `type`, `status`, `due`, `tags` | ✅ Sim (frontmatter) |
| Filename / título | ✅ Sim |
| Corpo do arquivo (## Next Action, ## Notas, etc.) | ❌ Não |

O título via filename já é suficiente para planejamento: `proposta-cliente-acme-q2` aparece no `/today` como prazo e prioridade, sem expor o conteúdo.

---

## Estrutura de Arquivos

```
vault/
├── .claude/
│   ├── hooks/
│   │   └── auto-commit.sh       # commit automático após Write/Edit
│   └── skills/                  # skills do Claude Code
│       ├── today/
│       ├── new/
│       ├── daily-review/
│       └── history/
├── .cursor/
│   └── skills/                  # skills do Cursor
│       ├── work-capture/
│       ├── update-business-profile/
│       ├── work-today/
│       ├── weekly-review/
│       └── project-status/
├── .cursorrules                  # regras sempre ativas no Cursor
├── context/
│   ├── business-profile.md      # contexto de negócio (sensitive: true)
│   ├── writing-style.md         # voz e tom
│   └── cursor-setup.md          # este sistema documentado
├── tasks/
├── projects/
├── people/
├── ideas/
├── daily/
├── weekly/
└── outputs/
```

---

## Auto-commit no Claude Code

O Claude Code tem um hook `PostToolUse` que comita automaticamente após cada operação de escrita em diretórios de conteúdo (`tasks/`, `projects/`, `people/`, etc.).

Formato do commit:
```
cos: new task - nome-da-task
cos: update project - nome-do-projeto
cos: daily plan for 2026-03-31
```

No Cursor, o commit é feito pela própria skill ao final de cada operação.

---

## Por que Funciona

- **Vault único** — sem sincronização, sem conflito, sem duplicação
- **Git como auditoria** — toda ação de qualquer agente vira commit rastreável
- **Skills especializadas** — cada agente faz o que seu ambiente permite
- **Separação por ambiente** — `environment: work` e `sensitive: true` tornam o limite explícito no próprio arquivo

---

*Documentado em 2026-03-31. Vault: second-brain-main.*
