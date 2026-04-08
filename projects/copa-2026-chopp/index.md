---
type: project
environment: work
status: active
tags: [copa-2026, chopp, inapp, seasonal, gmv]
sensitive: true
created: 2026-04-06
updated: 2026-04-07
---

## Next Action
Apresentar a arquitetura da solução para o Guilherme: banner em 3 fases (Copa vem aí → Countdown → Urgência/Escassez) começando em Maio + Schedule da Copa como tela dedicada com jogos do Brasil e jogos grandes destacados. Ver [[outputs/2026-04-07-copa-showcase-arquitetura]].

## Contexto

Aproveitamento do calendário da Copa do Mundo 2026 como alavanca de GMV de Chopp. A ideia central é reutilizar o **componente de banner inapp da home** (já validado no projeto de aniversário) e adaptá-lo com trigger baseado nos dias de jogo do Brasil — em vez de data de aniversário, o gatilho passa a ser a proximidade dos jogos.

**Hipótese de valor:** Jogo do Brasil é o maior ocasionador coletivo de consumo de chopp no calendário anual. Ao contrário do aniversário (evento individual, D-30), o jogo da Copa é um evento público, massivo e com data certa — o que permite comunicação altamente contextualizada sem necessidade de dados pessoais do usuário.

**Período da Copa:** 11 de junho a 19 de julho de 2026
**Jogos do Brasil — fase de grupos:**

| Data | Jogo | Horário (BRT) | Local |
|------|------|---------------|-------|
| 13/jun (sáb) | Brasil x Marrocos | 19h | MetLife Stadium — NJ |
| 19/jun (sex) | Brasil x Haiti | 22h | Lincoln Financial Field — Filadélfia |
| 24/jun (qua) | Escócia x Brasil | 19h | Hard Rock Stadium — Miami |

Fase eliminatória começa em 28/jun com oitavas (se Brasil avançar).

**Vantagem estratégica vs. aniversário:**
- Não depende de dado cadastral (todos os usuários são elegíveis)
- Volume de alcance potencial: toda a base ativa do app
- Urgência natural: "hoje tem jogo" gera conversão no mesmo dia
- Alinhado ao Q2 Priority #1 do business profile

## Outputs

- [[context]] — benchmarks, calendário completo e análise das soluções
- [[outputs/2026-04-07-copa-showcase-arquitetura]] — arquitetura do produto (3 camadas, fluxos, métricas, roadmap)
- [[research/2026-04-07-calendar-marketing-desk-research]] — desk research: calendar marketing e duas versões da Showcase

## Notas

### 2026-04-06
Projeto criado após aprendizados do teste 1 do banner de aniversário (CTR 10,22%, GMV R$217k, Purchase/View 0,041%). A lógica de trigger contextual já provou funcionar; a Copa é a maior oportunidade sazonal do ano para replicar e escalar.

Próximos passos antes de apresentar ao Guilherme:
- [ ] Definir solução preferida das 4 benchmarkadas (ver [[context]])
- [ ] Verificar se componente da home suporta trigger baseado em data absoluta (vs. data relativa de aniversário)
- [ ] Estimar volume de alcance: base ativa total vs. base de aniversariantes do teste 1
- [ ] Avaliar janela de ativação: D-7, D-3 ou D-day?
- [ ] Checar com Guilherme se Copa está no roadmap oficial de Q2 ou precisa de aprovação separada
