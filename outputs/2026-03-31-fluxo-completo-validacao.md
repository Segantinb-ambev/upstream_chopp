# Fluxo Completo — Second Brain com Claude + Cursor + GitHub

Documento para validação. Descreve como os três ambientes interagem, quem escreve o quê, e onde ficam os limites de segurança.

---

## Participantes

| Quem | Ferramenta | Acesso |
|------|-----------|--------|
| Bruno | Claude Code (conta pessoal) | Planejamento pessoal, captura não-sensível |
| Bruno | Cursor (conta corporativa) | Todo conteúdo de trabalho sensível |
| PM | Cursor (conta corporativa) | Todo conteúdo de trabalho sensível |
| Ambos | Obsidian | Leitura visual do vault (sem AI) |

---

## O Vault

Um único repositório git, hospedado no **GitHub corporativo** (privado).

- Bruno e PM clonam localmente
- Trabalham com suas ferramentas (Cursor, Obsidian)
- Sincronizam via `git push / pull`
- Cada ação vira um commit rastreável com prefixo `cos:`

```
GitHub corporativo (private repo)
        ↑ push / pull
    ┌───┴────────────┐
    │  Bruno (local) │     │  PM (local)  │
    └────────────────┘     └──────────────┘
```

---

## Regra de Ouro

> Dados sensíveis de trabalho entram no vault **apenas via Cursor**.

Claude Code (conta pessoal) processa conteúdo nos servidores da Anthropic. Por isso:
- Nunca recebe como input o corpo de arquivos `sensitive: true`
- Lê apenas o frontmatter desses arquivos (título, prazo, status, tags)
- Usa essas informações para planejamento — sem expor o conteúdo real

---

## O Que Cada Ferramenta Faz

### Claude Code — planejamento e captura pessoal

Ativa via terminal com comandos `/`:

| Comando | O que faz |
|---------|-----------|
| `/today` | Plano do dia — tasks pessoais + tasks de trabalho (só título e prazo) |
| `/new` | Captura rápida de tasks, ideias, notas pessoais |
| `/daily-review` | Revisão do dia — planejado vs realizado |
| `/history` | Atividade recente do vault via git log |

**Limite**: para arquivos com `sensitive: true`, Claude lê apenas o frontmatter. O corpo nunca é processado.

### Cursor — trabalho sensível (Bruno e PM)

Ativa automaticamente pelo contexto da conversa. Skills disponíveis:

| Skill | O que faz |
|-------|-----------|
| `work-capture` | Cria tasks, projetos e pessoas com dados reais de trabalho |
| `update-business-profile` | Atualiza role, prioridades, clientes, stakeholders |
| `work-today` | Plano do dia com tasks e projetos sensíveis completos |
| `weekly-review` | Revisão semanal — entregues, bloqueios, próxima semana |
| `project-status` | Atualiza próxima ação e notas de um projeto após reunião |

---

## O Limite do Que Claude Vê

Para qualquer arquivo com `sensitive: true`:

```
---                          ← Claude lê até aqui
type: task
environment: work
status: pending
due: 2026-04-10
tags: [proposta, q2]
sensitive: true
---                          ← Claude para aqui

## Contexto               ← Claude nunca lê isso
Cliente Acme, contrato de R$200k...

## Next Action
Enviar proposta revisada para Ana (Acme)...
```

O que aparece no plano do dia via `/today`:
```
- [ ] proposta-acme-q2 (due: 10 abr)
```

Sem nenhum dado do corpo. Apenas o título via filename e a data.

---

## Como um Item Flui no Sistema

**Exemplo: Bruno sai de uma reunião com o PM sobre um cliente.**

1. **Bruno abre o Cursor** → usa `work-capture`
   - Cria `projects/redesign-checkout-cliente-x.md` com `sensitive: true`
   - Cria `tasks/wireframes-fluxo-pagamento.md` com `sensitive: true` e `due: 2026-04-07`

2. **Git commita automaticamente**:
   ```
   cos: new project - redesign-checkout-cliente-x
   cos: new task - wireframes-fluxo-pagamento
   ```

3. **PM faz `git pull`** → vê os arquivos no Obsidian ou Cursor

4. **PM usa `project-status` no Cursor** → atualiza next action do projeto

5. **Bruno roda `/today` no Claude Code** → vê no plano:
   ```
   ## Trabalho — Hoje
   - [ ] wireframes-fluxo-pagamento (due: 07 abr)
   ```
   Claude não leu o corpo — só o frontmatter e o filename.

6. **Fim do dia**: Bruno roda `/daily-review` → Claude atualiza o status da task para `complete` no frontmatter, sem tocar no corpo.

---

## Estrutura de Arquivos

```
vault/
├── .claude/skills/          # Skills do Claude Code
│   ├── today/
│   ├── new/
│   ├── daily-review/
│   └── history/
├── .cursor/skills/          # Skills do Cursor (Bruno e PM)
│   ├── work-capture/
│   ├── update-business-profile/
│   ├── work-today/
│   ├── weekly-review/
│   └── project-status/
├── .cursorrules             # Regras sempre ativas no Cursor
├── context/
│   ├── business-profile.md  # sensitive: true — contexto de negócio real
│   ├── writing-style.md     # voz e tom (não sensível)
│   └── cursor-setup.md      # este sistema documentado
├── tasks/
├── projects/
├── people/
├── ideas/
├── daily/
├── weekly/
└── outputs/
```

---

## Convenções Obrigatórias

Todo arquivo tem frontmatter YAML:

```yaml
---
type: task | project | person | idea | daily | weekly | context
environment: personal | work
status: pending | in-progress | complete | cancelled
sensitive: true        # obrigatório se tiver dados reais de trabalho
created: YYYY-MM-DDTHH:MM:SS
---
```

**Regra de sensibilidade** — marcar `sensitive: true` sempre que houver:
- Nomes de clientes reais
- Métricas ou números de negócio
- Detalhes de produto não públicos
- Nomes de stakeholders internos

---

## Perguntas para Validação

1. O limite "frontmatter apenas" para arquivos sensíveis é suficiente para o compliance?
2. O PM precisa de algum onboarding específico além das skills do Cursor?
3. O vault no GitHub corporativo cobre o requisito de "ambiente seguro" para colaboração?
4. Tem algum tipo de dado que não deve aparecer nem no filename (ex: nome de cliente no slug)?

---

*Gerado em 2026-03-31 para validação do fluxo Dual-AI Second Brain.*
