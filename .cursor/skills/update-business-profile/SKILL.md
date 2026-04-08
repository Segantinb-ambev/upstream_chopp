---
name: update-business-profile
description: Update the business profile context file with real work data. Use when the user mentions changes to their role, team, OKRs, priorities, clients, stakeholders, or tools. This is the source of truth used by Claude to understand work context.
---

# update-business-profile — Atualizar Perfil Profissional

Mantém `context/business-profile.md` atualizado com dados reais de trabalho. Este arquivo é o que o Claude Code lê para entender o contexto profissional — mantê-lo atual é crítico para o sistema funcionar bem.

## Passos

1. **Ler** `context/business-profile.md` atual
2. **Identificar** o que muda: role, empresa, foco, stakeholders, ferramentas, prioridades
3. **Atualizar** apenas as seções relevantes (preservar o resto)
4. **Verificar** se o arquivo tem `sensitive: true` no frontmatter (adicionar se não tiver)
5. **Commit** com descrição do que mudou

## Seções do Business Profile

| Seção | Quando atualizar |
|-------|-----------------|
| Role | Mudança de cargo, time ou escopo |
| Company | Mudança de empresa, tamanho, indústria |
| Current Focus Areas | Novos projetos, iniciativas encerradas |
| Key Stakeholders | Novos contatos relevantes, mudanças de papel |
| Tools & Systems | Adoção ou descontinuação de ferramentas |
| Priorities This Quarter | Início de novo quarter, mudança de OKRs |

## Regras de Edição

- Preservar seções que o usuário não mencionou
- Usar linguagem direta (não usar "você" — o arquivo é lido como contexto pelo LLM)
- Datas de prioridades: incluir o quarter (Q1 2026, Q2 2026)
- Stakeholders: incluir papel e contexto do relacionamento, não só o nome

## Frontmatter Esperado

```yaml
---
type: context
sensitive: true
updated: YYYY-MM-DD
---
```

## Commit

```bash
git add context/business-profile.md
git commit -m "cos: update context - business-profile"
```
