---
name: work-capture
description: Capture work tasks, projects, and people notes with sensitive data. Use when the user mentions clients, meetings, deliverables, colleagues, product details, metrics, or any work-related item that needs to be filed in the vault. Adds sensitive: true to work files automatically.
---

# work-capture — Captura de Trabalho

Cria e atualiza arquivos no vault a partir de input de trabalho em linguagem natural. Sempre marca arquivos com dados reais como `sensitive: true`.

## Passos

1. **Ler** `context/business-profile.md` para entender o contexto de negócio
2. **Decompor** o input em entidades (pode ser mais de uma)
3. **Classificar** cada entidade: task | project | person | idea
4. **Extrair** dados estruturados (datas, clientes, tags)
5. **Verificar** se person/project já existe (Glob antes de criar)
6. **Criar/atualizar** os arquivos
7. **Commit** com o formato `cos: new <type> - <slug>`

## Decomposição

Exemplo: "reunião com a Ana da Acme amanhã sobre o contrato Q2, preciso preparar proposta"

Entidades:
- Person: Ana (empresa: Acme) → `people/ana-acme.md`
- Task: preparar proposta para Acme → `tasks/proposta-acme-q2.md` (due: amanhã)
- Task: reunião com Ana → `tasks/reuniao-ana-acme.md` (due: amanhã)

## Classificação

- Pessoa com contexto de relacionamento → **person**
- Trabalho contínuo com várias etapas → **project**
- Item acionável específico → **task**
- Especulativo, estratégico → **idea**

## Sensibilidade

Sempre adicionar `sensitive: true` quando o arquivo contiver:
- Nomes de clientes reais
- Métricas ou números de negócio
- Detalhes de produto não públicos
- Nomes de stakeholders internos

## Formatos

**Task:**
```yaml
---
type: task
environment: work
status: pending
due: YYYY-MM-DD
tags: []
sensitive: true
created: YYYY-MM-DDTHH:MM:SS
---
Descrição clara da ação.
[[projeto-relacionado]]
```

**Project:**
```yaml
---
type: project
environment: work
status: active
tags: []
sensitive: true
created: YYYY-MM-DD
---

## Next Action
Próximo passo mais importante.

## Contexto
Informações relevantes sobre o projeto.

## Notas
```

**Person:**
```yaml
---
type: person
environment: work
tags: [cliente | colega | stakeholder]
last-contact: YYYY-MM-DD
sensitive: true
---

## Contexto
Quem é, papel, empresa, como se relacionam.

## Follow-ups
- [ ] Itens pendentes
```

## Linking

Usar links Obsidian `[[slug]]` para conectar entidades. Ao criar task ligada a projeto, atualizar o projeto com `[[task-slug]]`.

## Commit

```bash
git add <arquivo(s)>
git commit -m "cos: new <type> - <slug>"
```
