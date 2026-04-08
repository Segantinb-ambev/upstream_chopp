---
type: context
environment: work
sensitive: true
updated: 2026-04-07
---

# Contexto — Copa 2026 com Chopp

## Calendário Completo da Copa do Mundo 2026

**Formato:** 48 seleções, 104 partidas, 12 grupos, 16 estádios
**Países-sede:** Estados Unidos, México e Canadá

### Jogos do Brasil

| Fase | Data | Jogo | Horário (BRT) | Local |
|------|------|------|---------------|-------|
| Grupo C — Rod. 1 | **13/jun (sáb)** | Brasil x Marrocos | 19h | MetLife Stadium, NJ |
| Grupo C — Rod. 2 | **19/jun (sex)** | Brasil x Haiti | 22h | Lincoln Financial Field, Filadélfia |
| Grupo C — Rod. 3 | **24/jun (qua)** | Escócia x Brasil | 19h | Hard Rock Stadium, Miami |
| 32-avos | 28/jun – 3/jul | A definir | — | — |
| Oitavas | 4–7/jul | A definir | — | — |
| Quartas | 9–11/jul | A definir | — | — |
| Semifinais | **14–15/jul** | A definir | — | — |
| Final | **19/jul (dom)** | A definir | — | MetLife Stadium, NJ |

> Primeiros dois melhores 3ºs classificados de cada grupo também avançam. Brasil precisaria de resultado mínimo nas 3 rodadas para estar nas eliminatórias.

### Janela Estratégica para Chopp

Os 3 jogos da fase de grupos do Brasil caem em **sábado, sexta e quarta** — todos dias com alta propensão de pedido de chopp (o teste de aniversário confirmou que 3ª e 5ª são picos, mas sábado e sexta-feira são dias naturais de festa). A janela 13/jun–19/jul é inteiramente de Q2, dentro do KPI foco de GMV.

---

## Componente Existente — Benchmark Interno (Aniversário)

O componente inapp da home do Zé já foi testado com o banner de aniversário. Resultados do Teste 1:

| Métrica | Resultado |
|---------|-----------|
| Views | 399.542 |
| CTR | 10,22% |
| PDP/Click | 10,9% |
| Purchase/View | 0,041% |
| Empty pós-clique | 18,5% |
| GMV gerado | R$ 217k |
| Lift GMV | +114% vs. baseline |

**O que isso significa para Copa:**
- Com a base total ativa (vs. apenas aniversariantes), o volume de Views pode ser 10x–50x maior
- CTR de ~10% já validada — é o ponto de partida
- O gargalo do pós-clique (empty state 18,5%) precisa ser corrigido antes ou junto com a Copa
- Purchase/View de 0,041%: se atingirmos 5M de views em dia de jogo → ~2.050 pedidos

---

## Benchmark Externo — Soluções de Copa em Apps

### PedidosYa — "World Cup Delivery" (2022, Argentina) ⭐ Referência-chave
**Mecanismo:** Reutilizou a tela de rastreamento de pedido (componente existente) para mostrar o rastreamento em tempo real do avião trazendo a taça do mundo. Push notification com texto "Seu pedido está a caminho" levava usuários a abrir o app esperando rastreamento de comida — e encontravam a taça.

- Zero investimento em mídia
- 25M de alcance em redes sociais
- 32% mais mencionado que Messi no dia da vitória
- ROI de $62 para cada $1 gasto em produção
- Ganhou Gold Creative Effectiveness Lion em Cannes

**Lição:** reutilizar a interface existente de forma contextual cria surpresa e engajamento sem custo extra de desenvolvimento.

### iFood (Brasil, 2026)
- Tornou-se patrocinador oficial da CBF (seleção masculina e feminina)
- Parceria com CazéTV para transmissões da Copa
- Campanha "100 dias de oferta" integrada à identidade "Brasileiro, Bom e Barato"
- Presença massiva em mídia (TV, OOH, digital)

**Lição:** concorrente principal está investindo pesado em Copa como diferencial de marca. Zé Delivery precisa de uma resposta no produto, não só em mídia.

### Mecânicas Gamificadas (Odicci Benchmark, 2026)
- **"Tap-to-Score Instant Win"** — toca na bola, revela desconto ou prêmio
- **"Spin the Wheel: Matchday Prizes"** — roleta com recompensas por jogo
- **"World Cup Digital Calendar"** — revelação diária (tipo Calendário do Advento)
- **Refer-a-Friend por jogo** — indica amigo antes do jogo, ambos ganham vantagem

**Lição:** mecânicas de daily engagement com a Copa sustentam 5 semanas de campanha — não só 1 banner.

---

## 4 Soluções Possíveis com o Componente da Home

### Solução 1 — Countdown Banner (Match Day Activation)
**Como funciona:** O banner inapp ativa automaticamente em janelas de tempo predefinidas ao redor dos jogos do Brasil:
- D-3 antes do jogo: "Brasil joga em 3 dias — garanta o chopp"
- D-1: "Amanhã é dia de Brasil. Agende agora"
- D-day (manhã): "Hoje tem Brasil às 19h. Peça o chopp"

**Diferença do aniversário:** Trigger é data absoluta (13/jun, 19/jun, 24/jun) em vez de data relativa do usuário. Todos os usuários elegíveis ao mesmo tempo.

**Prós:**
- Máximo alcance (base total, não segmento)
- Urgência natural do jogo cria conversão sem desconto
- Simples de implementar — mesma lógica do banner de aniversário

**Contras:**
- Sem personalização (todos recebem igual)
- Risco de oversaturation se ativar em todos os jogos da Copa, não só do Brasil

**Esforço:** Baixo — 1 sprint se o componente já suporta trigger por data

---

### Solução 2 — Calendário de Jogos na Showcase
**Como funciona:** Card fixo ou carrossel na seção Showcase (onde ficam os banners sazonais da home), exibindo os próximos jogos do Brasil com CTA direto para o Chopp em Casa.

Visual: `⚽ 13/jun — Brasil x Marrocos, 19h → [Peça o Chopp]`

Fica ativo durante toda a Copa (11/jun a 19/jul), não apenas nos dias de jogo.

**Prós:**
- Visibilidade contínua por 5 semanas
- Baixo esforço cognitivo para o usuário (contexto claro)
- Conecta intenção de assistir ao jogo com a compra com antecedência natural

**Contras:**
- Depende de aprovação de slot na Showcase (pode ter competição interna por espaço)
- Requer atualização de conteúdo a cada rodada (ou automação)

**Esforço:** Médio — precisa de slot na Showcase + automação de conteúdo por data

---

### Solução 3 — Match Day Modal (Inspirado no PedidosYa)
**Como funciona:** No dia do jogo do Brasil, ao abrir o app, o usuário vê um modal/overlay temático antes de chegar à home:
- Visual imersivo da Copa (bandeira, placar, countdown até o apito inicial)
- CTA: "Seu chopp já foi pedido?" com botão direto para PDP
- Pode incluir oferta especial de match day (ex.: entrega expressa ou pequeno desconto)

**Prós:**
- Máximo impacto visual — o usuário não pode ignorar
- Nível de engajamento alto (é um micro-momento de surpresa positiva)
- Fácil de A/B testar (modal vs. banner vs. nada)

**Contras:**
- Pode ser percebido como intrusivo se mal executado
- Depende de tooling de inapp messaging com suporte a modal (confirmar Braze SDK no app)
- Só vale a pena nos dias de jogo do Brasil (3 vezes na fase de grupos)

**Esforço:** Médio-alto — depende de Braze SDK no app (a ser confirmado)

---

### Solução 4 — Calendário do Advento Copa (Série de 5 Semanas)
**Como funciona:** Campanha de engagement progressivo ao longo das 5 semanas da Copa. A cada jogo do Brasil (ou semanalmente), o banner inapp revela uma oferta ou conteúdo diferente:
- Semana 1 (antes do 1º jogo): "A Copa começa em X dias — peça o chopp"
- Jogo 1 (13/jun): Oferta A
- Jogo 2 (19/jun): Oferta B + personalização por quem pediu na semana 1
- Jogo 3 (24/jun): Oferta C + reativação de quem não pediu ainda
- Eliminatórias: regime de urgência ("E se o Brasil for às semis?")

**Prós:**
- Sustenta engajamento por 5+ semanas (máximo aproveitamento da Copa)
- Permite aprendizado iterativo a cada jogo
- Usuários que compraram no Jogo 1 viram clientes de Copa — pós-compra pode ser personalizado

**Contras:**
- Maior complexidade de CRM e automação
- Requer mais produção de conteúdo (um criativo por rodada mínimo)
- Precisa de Guilherme + CRM team envolvidos desde o início

**Esforço:** Alto — envolve planning de campanha completo, não só ativação de componente

---

## Recomendação Preliminar

**Curto prazo (Q2, antes de 13/jun):** Solução 1 + Solução 2 em paralelo
- Solução 1 (Countdown Banner) para os 3 jogos do Brasil — baixo esforço, alto alcance, testa o trigger por data absoluta
- Solução 2 (Calendário na Showcase) como presença constante durante toda a Copa

**Se Braze SDK confirmar no app:** adicionar Solução 3 (Modal) para o jogo de abertura do Brasil (13/jun) como experimento de alto impacto.

**Solução 4** pode ser o framework para Copa do Mundo 2030 ou próxima sazonalidade longa (ex.: Olimpíadas).

---

---

## Duas Versões do Componente Showcase

Estudo completo em [[research/2026-04-07-calendar-marketing-desk-research]].

### Versão 1 — Calendário Passivo
Card estático com lista dos próximos jogos do Brasil e CTA direto para o Chopp em Casa. Ativo durante toda a Copa (11/jun–19/jul). Baixo esforço técnico (1 sprint), presença contínua de 5 semanas, CTR estimado ~8–10%.

### Versão 2 — Countdown Ativo
Card dinâmico com countdown regressivo até o próximo jogo. Copy muda automaticamente por janela de tempo: D-7, D-3, D-1, match day. Esforço médio (1,5–2 sprints), urgência crescente, CTR estimado de 12–15% nos dias de jogo.

**Estratégia de combinação:** V1 como base de awareness (5 semanas) + V2 ativando sobre a V1 nas janelas D-7 a D-day de cada jogo. Se apenas um slot disponível na Showcase, priorizar V2 para match days.

---

## Referências

- [[index]] — projeto principal
- [[regua-aniversario-inapp/context]] — dados do componente inapp e teste 1 do banner
- [[research/2026-04-07-calendar-marketing-desk-research]] — desk research: calendar marketing, produto+ocasião e lógica das duas versões da Showcase
- Business Profile Q2 Priority #1: Copa do Mundo com Chopp
