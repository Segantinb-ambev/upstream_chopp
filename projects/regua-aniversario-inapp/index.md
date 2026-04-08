---
type: project
environment: work
status: active
tags: [crm, lifecycle, inapp, chopp]
sensitive: true
created: 2026-04-01
updated: 2026-04-02
---

## Next Action
Definir escopo da V2 do banner de aniversário: priorizar correção do empty state pós-clique, personalização por cluster/dia (focar em Core e Reativado em 3ª/5ª) e melhoria de copy — dado que volume aumentou, o impacto de otimizar o funil é maior.

## Contexto
Projeto fora do planejamento de Q2. Ideia: criar uma régua de comunicação inapp voltada para usuários que fazem aniversário, usando o evento como gatilho para conversão de Chopp em Casa.

**Hipótese de valor:** aniversário é um dos maiores ocasionadores de pedido de chopp (festa, reunião com amigos). Usuários que têm data de nascimento cadastrada e nunca compraram chopp podem ser ativados com uma oferta ou mensagem contextualizada próxima ao seu aniversário.

**Canais prováveis:** push notification + banner inapp / modal contextual na home do Zé Delivery.

**Dependências a mapear:**
- Zé Delivery coleta data de nascimento dos usuários? Em qual base?
- Existe integração com ferramenta de CRM/push (Braze, Iterable, etc.)?
- Quem é o responsável por automações de lifecycle no Zé?

## Outputs

- [[2026-04-01-discovery-regua-aniversario-inapp]] — documento de discovery completo
- [[primeiro-teste]] — resultados do primeiro experimento com o banner de aniversário

## Notas

### 2026-04-02
Primeiro teste do banner de aniversário concluído. GMV de R$ 217k (+114% vs. baseline na ocasião), com CTR sólida de 10,22% mas conversão pós-clique como principal gargalo (empty state 18,5%, PDP/Click 10,9%). Métrica de sucesso quase alcançada: 0,045 vs. meta 0,05. Volume cresceu bastante — hora de evoluir para V2 com foco em personalização por cluster/dia e correção do pós-clique. Dados completos em [[context]].

### 2026-04-01
- Não está no roadmap de Q2 — precisa de validação antes de colocar no Jira
- Pode ser um quick win se a infra de CRM já existir
- Avaliar se faz sentido restringir à jornada de Chopp ou expandir para o Zé como um todo
