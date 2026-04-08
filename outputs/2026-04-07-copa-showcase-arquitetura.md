---
type: output
environment: work
sensitive: true
date: 2026-04-07
project: copa-2026-chopp
tags: [copa-2026, chopp, showcase, arquitetura, product-design]
---

# Arquitetura do Produto — Copa 2026 Showcase + Calendário
### Zé Delivery · Chopp em Casa · Q2 2026

---

## 0. O Problema Real: Awareness (dados de pesquisa)

Antes de definir qualquer componente, é necessário entender o problema que a Copa Showcase precisa resolver — e ele é maior do que parecia.

### Os números

| Dado | Fonte | N |
|------|-------|---|
| 88% dos consumidores de chopp nunca pediram via Zé Delivery | Survey Painel (mar/2025) + Typeform (jan/2026) | 2.372 + 967 |
| ~35% não sabem que Chopp+Chopeira existe no Zé | Combinação: 18% "não conhecia a modalidade" + 17% "não sabia ser possível" | Typeform jan/2026 |
| Preço é a barreira #1 (49%) | Ambos os surveys | 2.372 + 967 |
| Descoberta: nenhum usuário entrevistado descobriu o serviço por redes sociais | Rota do Consumidor (qualitativo) | 4 entrevistas |

**Preço está fora do escopo desse MVP.** É a barreira declarada mais comum, mas não é acionável agora. O foco vai para o segundo maior problema — que é o que o produto pode resolver diretamente.

### O insight que muda a arquitetura

**35% dos consumidores de chopp não sabem que podem pedir no Zé Delivery.** Isso significa que o componente Copa Showcase não é apenas uma ferramenta de *conversão* — é principalmente uma ferramenta de *descoberta*.

A Copa é a janela perfeita para resolver awareness porque:
- O contexto emocional do jogo reduz resistência cognitiva — o usuário está mais receptivo
- "Jogo do Brasil + chopp" é uma associação natural que não precisa ser criada do zero
- O app já está aberto (o usuário vai ao Zé por outros produtos) — a descoberta acontece sem custo de mídia

### Duas audiências distintas no mesmo componente

O componente precisa falar com dois públicos simultaneamente:

| Audiência | Tamanho estimado | Problema | O que o componente faz |
|-----------|-----------------|----------|------------------------|
| **Nunca soube** | ~35% da base | Não sabe que existe | **Descoberta**: apresenta o serviço pelo primeira vez |
| **Sabe, nunca pediu** | ~53% da base | Falta de momento/gatilho | **Ativação**: fornece o contexto certo na hora certa |
| **Já pediu, não recomprou** | ~12% da base | Fricção de recompra | **Reativação**: lembrete contextualizado |

**Implicação direta de design:** o copy e a arquitetura da informação não podem pressupor que o usuário já conhece o serviço. "Pedir Chopp" não basta — é necessário comunicar *o que é* o serviço em cada ponto de contato.

---

## 1. Ponto de Partida: Working Backwards (Amazon)

Antes de definir componentes, o método Amazon exige começar pela experiência do cliente desejada e trabalhar para trás até a solução técnica. A pergunta não é "o que vamos construir?" — é "o que o usuário vai sentir, e que jornada produz esse sentimento?"

### Os Jobs to Be Done

Usando o framework JTBD (Clayton Christensen / Tony Ulwick), a Copa Showcase resolve dois jobs distintos:

**Job 1 — Descoberta (35% da base: "nunca soube")**
> **"Quando** estou no app do Zé antes de um jogo do Brasil,  
> **quero** descobrir que posso pedir chopp com chopeira pelo app,  
> **para que** eu não precise organizar por outro canal ou desistir da ideia."

**Job 2 — Ativação/Reativação (65% da base: "sabe, nunca pediu" ou "já pediu")**
> **"Quando** estou planejando assistir ao jogo do Brasil,  
> **quero** garantir o chopp sem precisar lembrar de pesquisar isso separado,  
> **para que** eu possa focar na preparação da festa."

**Critério de sucesso unificado:** a arquitetura resolve os dois jobs quando o usuário consegue, em no máximo 2 toques a partir do banner, estar dentro da jornada de compra do Chopp em Casa — independentemente de já conhecer o serviço ou não.

### Press Release Interno (working backwards)

> **Zé Delivery lança Copa 2026 Showcase** — pelo app do Zé, você vê quando o Brasil joga e garante o chopp com chopeira antes do apito inicial. Para quem ainda não sabia: é possível pedir chopp geladinho com chopeira em casa direto pelo Zé. Para quem já sabia: o lembrete certo, na hora certa. Com um toque, você está na categoria. Simples assim.

**Implicação de design:** o componente precisa comunicar *o que é o serviço* de forma implícita já no banner — não apenas chamar para ação. Um usuário que nunca viu "Chopp em Casa" não vai clicar em um CTA que não entende.

---

## 2. Norte Estratégico: Chopp em Maio

### O constraint que define tudo

Chopp é um serviço agendado. A Copa do Mundo começa em 11 de junho. O primeiro jogo do Brasil é 13 de junho. Mas **o pedido precisa ser feito com antecedência** — e a capacidade das franquias é limitada.

**Conclusão:** a janela de conversão da campanha é **Maio**, não Junho.

```
MAIO                               JUNHO
├── Campanha ativa ──────────────► ├── Copa começa
│   Awareness → Countdown          │   Jogo 1: 13/jun
│   → Urgência / Escassez          │   Jogo 2: 19/jun
│                                  │   Jogo 3: 24/jun
│   Objetivo: esgotar              │
│   estoque de Chopp               │   ← pedidos já foram feitos em Maio
└──────────────────────────────────┘
```

**Por que isso importa para o design:**
- O banner não é um lembrete no dia do jogo — é um instrumento de planejamento antecipado
- A urgência em Maio não é "Brasil joga hoje" — é "garanta o chopp agora antes que esgote"
- O CTA principal em todas as fases de Maio é agendamento, não compra imediata
- O schedule serve para o usuário planejar *quando* quer ter chopeira em casa

### A escassez é real

Cada franquia do Chopp Brahma Express opera em região exclusiva com número limitado de chopeiras disponíveis. Em um evento do tamanho da Copa, com campanha ativa para toda a base do app, **o estoque vai esgotar em algumas regiões antes do primeiro jogo**.

"Últimas unidades" na fase 3 não é apelo de marketing — é fato operacional. Essa escassez real é o maior diferencial de urgência da campanha: não é um countdown artificial, é um limite físico.

---

## 4. Arquitetura Geral — Três Camadas

A solução tem uma estrutura de três camadas com progressão de detalhe (princípio de **Progressive Disclosure**):

```
┌─────────────────────────────────────────────────────┐
│  CAMADA 1 — Entry Point                              │
│  Banner da Home (Showcase Component)                 │
│  → Ativo de Maio até o fim da Copa                   │
│  → Visual animado · 3 fases com copy e tom distintos │
│  → CTA muda conforme a fase                          │
└──────────────────────────┬──────────────────────────┘
                           │ Tap
                           ▼
┌─────────────────────────────────────────────────────┐
│  CAMADA 2 — Schedule da Copa                         │
│  Tela dedicada (full screen)                         │
│  → Schedule completo da Copa organizado por fase     │
│  → Jogos do Brasil + jogos grandes em datas boas     │
│    destacados com CTA de Chopp                       │
│  → Demais jogos visíveis sem CTA (utilidade real)    │
│  → Bloco de educação do serviço no topo              │
└──────────────────────────┬──────────────────────────┘
                           │ Tap no CTA de jogo destacado
                           ▼
┌─────────────────────────────────────────────────────┐
│  CAMADA 3 — Destino                                  │
│  Categoria Chopp em Casa (ou PDP direta)             │
│  → Jornada de compra existente                       │
└─────────────────────────────────────────────────────┘
```

**Princípio de design aplicado:** cada camada revela apenas o que é necessário para o próximo passo. O banner não precisa mostrar todos os jogos — só contextualizar a Copa + Chopp. O schedule é onde o usuário planeja. A PDP é onde compra.

---

## 3. Camada 1 — Showcase Component

### Contexto técnico

O componente Showcase já existe na home do Zé Delivery — o mesmo slot onde o banner de aniversário gerou CTR de 10,22% e GMV de R$217k. A infraestrutura de trigger por data já foi validada. O ponto de partida para Copa é adaptar o trigger e o conteúdo.

**Diferença-chave da Copa vs. aniversário:** o banner de aniversário era estático (mesmo visual, trigger pessoal). O banner da Copa tem **3 fases com visual, tom e copy distintos** — e começa em Maio, não em Junho. O componente precisa suportar troca de criativo por range de datas via CMS.

**Produção:** todas as fases são animadas. A animação captura atenção no scroll da home e comunica energia de Copa sem precisar de muito texto.

---

### Fase 1 — "Copa vem aí" (início de Maio → meados de Maio)

**Tom:** antecipação e planejamento. Não é urgência — é convite. A Copa ainda está longe, mas o momento de se programar é agora.

**Objetivo:** awareness do serviço + primeira abertura do Schedule.

```
┌─────────────────────────────────────────┐
│                                          │
│  ⚽  Copa do Mundo 2026  ← bola animada  │
│                                          │
│  Se programe pra torcer                 │
│  com chopp em casa                      │
│                                          │
│  [Ver jogos do Brasil →]                 │
└─────────────────────────────────────────┘
```

**Por que esse copy:** "se programe" comunica planejamento antecipado — alinha ao comportamento real dos compradores (pedido com antecedência, às vezes semanas antes). "Chopp em casa" nomeia o produto de forma tangível sem usar o nome técnico "Chopp em Casa".

**CTA destino:** Schedule (Camada 2) — o usuário descobre o serviço no contexto da Copa, não em uma landing de produto.

**Animação:** elementos de Copa em movimento, tom leve. Energia de antecipação, não pressão.

---

### Fase 2 — Countdown (meados de Maio → fim de Maio)

**Tom:** urgência crescente e concreta. A Copa está chegando — o tempo para planejar está diminuindo.

**Objetivo:** conversão via agendamento antecipado. O countdown é o gatilho de urgência honesto: não é "Brasil joga hoje" — é "faltam X dias para a Copa".

```
┌─────────────────────────────────────────┐
│                                          │
│  ⚽  Copa começa em                      │
│                                          │
│        XX dias   ← número animado        │
│                                          │
│  Garanta o chopp antes que esgote       │
│                                          │
│  [Garantir agora →]                      │
└─────────────────────────────────────────┘
```

**Por que esse copy:** o countdown é concreto e verificável. "Antes que esgote" introduz escassez sem ser alarmista — e prepara o usuário para a Fase 3. "Garantir agora" é um CTA de ação afirmativa: não "ver mais", não "saiba como" — é reservar uma vaga.

**CTA destino:** A/B entre Schedule e PDP direta. Hipótese: nessa fase parte do usuário já sabe o que quer — o Schedule pode ser etapa desnecessária.

**Animação:** countdown com número decrementando. Sensação de tempo passando, mais urgente que Fase 1.

---

### Fase 3 — Urgência / Escassez (fim de Maio → Copa)

**Tom:** urgência real, escassez honesta. Cada franquia tem número limitado de chopeiras. Em Copa, esgota. Essa mensagem é factual.

**Objetivo:** conversão final de quem viu as fases anteriores e não comprou + primeira conversão de novos usuários com o argumento mais forte.

#### Variante A — Escassez por unidades

```
┌─────────────────────────────────────────┐
│                                          │
│  🇧🇷  Brasil joga em XX dias             │
│                                          │
│  Últimas unidades de chopp              │
│  disponíveis na sua região              │
│                                          │
│  [Reservar agora]                        │
└─────────────────────────────────────────┘
```

"Reservar" comunica que o estoque é finito e que o usuário está garantindo uma vaga — mais preciso para o modelo de agendamento do serviço.

#### Variante B — Urgência por prazo de antecedência

```
┌─────────────────────────────────────────┐
│                                          │
│  🇧🇷  Brasil joga em XX dias             │
│                                          │
│  Para ter chopp no dia do jogo          │
│  peça com XX dias de antecedência       │
│                                          │
│  [Pedir agora — ainda dá tempo]          │
└─────────────────────────────────────────┘
```

"Ainda dá tempo" é um CTA de alívio — reduz a barreira de quem achava que já era tarde demais. Educa sobre o prazo de agendamento ao mesmo tempo.

**Teste A/B:** rodar as duas variantes. A Variante A tende a converter mais rápido (escassez direta). A Variante B tende a ter CTR maior (menos intimidante). Medir Purchase/View, não só CTR.

**CTA destino:** PDP direta — urgência máxima, sem etapa intermediária.

**Animação:** mais intensa, cor mais presente (verde-amarelo do Brasil). Energia de decisão, não de convite.

---

### Resumo das três fases

| Fase | Período | Tom | Animação | CTA destino |
|------|---------|-----|----------|------------|
| **1 — Copa vem aí** | Início de Maio | Antecipação, convite | Leve, temática Copa | Schedule |
| **2 — Countdown** | Meados de Maio | Urgência crescente | Countdown animado | Schedule ou PDP (A/B) |
| **3 — Urgência** | Fim de Maio → Copa | Escassez real | Intensa, dinâmica | PDP direta |

**Nota de produção:** as três fases são criativos distintos. A troca entre elas é por range de datas no CMS ou Braze — não por lógica de código.

---

## 6. Camada 2 — Schedule da Copa

### O que é e por que é uma feature, não só uma lista

A Camada 2 é um **schedule completo da Copa do Mundo** embutido no app do Zé — não apenas uma lista dos jogos do Brasil. Essa distinção muda fundamentalmente o valor do componente:

| Abordagem | O que entrega |
|-----------|--------------|
| Lista de jogos do Brasil | Ferramenta de conversão — útil só para quem já quer comprar |
| Schedule completo da Copa | **Feature de utilidade genuína** — o usuário vem pelo calendário, fica pelo Chopp |

Um schedule completo tem valor independente da compra: o usuário o consulta para saber quando jogos acontecem, para planejar a semana, para ver que times estão na fase. O Chopp em Casa aparece ancorado nesse contexto de uso real — não como anúncio, mas como solução dentro de uma feature que o usuário já está usando.

**Isso é o princípio Amazon de "customer obsession":** entregar algo que o usuário quer usar por conta própria, e incorporar o produto como solução natural dentro desse uso.

### Padrão de interface recomendado: Tela dedicada (Full Screen)

Para um schedule completo da Copa (104 partidas, organizado por fase e data), o Bottom Sheet é insuficiente em termos de espaço e navegação. A recomendação é uma **tela dedicada** acessada via tap no Showcase, com navegação de retorno para a home.

Razões para Full Screen sobre Bottom Sheet nesse caso:

| Critério | Bottom Sheet | Tela Dedicada |
|----------|-------------|---------------|
| Espaço para 104 jogos | Insuficiente | Adequado com scroll |
| Navegação por fase/rodada | Difícil (scroll vertical único) | Tabs ou filtros superiores |
| Retorno para home | Gesto de dismiss | Back navigation nativa |
| Percepção de valor | Feature pequena, passageira | Feature completa, intencional |

### Arquitetura de informação do Schedule

O schedule é organizado por **fases** com navegação por tabs ou filtros horizontais no topo:

```
[ Grupos ]  [ Oitavas ]  [ Quartas ]  [ Semis ]  [ Final ]
```

Dentro de cada fase, os jogos são agrupados por **data** como seção header:

```
────────────────────────────────────────────
 Seg, 13 jun
────────────────────────────────────────────
```

#### Anatomia da tela

```
┌─────────────────────────────────────────────┐
│  ← Copa do Mundo 2026                        │  ← back navigation
│                                              │
│  [ Grupos ][ Oitavas ][ Quartas ][ Semis ]  │  ← filtro por fase
│  [ Final ]                                   │
│                                              │
│ ─── Sáb, 13 jun ──────────────────────────  │  ← seção por data
│                                              │
│  ┌────────────────────────────────────────┐  │
│  │  🇧🇷  19h  BRT          Grupo C        │  │
│  │  BRASIL     ×     Marrocos  🇲🇦        │  │  ← jogo do Brasil: card destacado
│  │                                        │  │
│  │  [Pedir chopp para esse jogo]          │  │  ← CTA só em jogos do Brasil
│  └────────────────────────────────────────┘  │
│                                              │
│  ┌────────────────────────────────────────┐  │
│  │  15h  BRT                   Grupo A    │  │
│  │  Argentina   ×   Austrália             │  │  ← outros jogos: card sem CTA
│  └────────────────────────────────────────┘  │
│                                              │
│  ┌────────────────────────────────────────┐  │
│  │  22h  BRT                   Grupo B    │  │
│  │  França      ×   México                │  │
│  └────────────────────────────────────────┘  │
│                                              │
│ ─── Dom, 14 jun ──────────────────────────  │
│                                              │
│  ┌────────────────────────────────────────┐  │
│  │  18h  BRT                   Grupo D    │  │
│  │  Alemanha    ×   Japão                 │  │
│  └────────────────────────────────────────┘  │
│  ...                                         │
│                                              │
│  ┌────────────────────────────────────────┐  │
│  │  [Ver Chopp em Casa]                   │  │  ← CTA fixo no bottom sempre visível
│  └────────────────────────────────────────┘  │
└─────────────────────────────────────────────┘
```

#### Diferenciação visual: três tipos de card

O schedule tem três níveis de destaque, não dois:

| Tipo | Critério | CTA | Visual |
|------|----------|-----|--------|
| **Jogo do Brasil** | Qualquer jogo com a seleção brasileira | "Pedir chopp para esse jogo" | Card destacado, cor Copa, 🇧🇷 em evidência |
| **Jogo grande em data boa** | Critérios abaixo | "Pedir chopp para esse jogo" | Card destacado, cor Copa, sem bandeira do Brasil |
| **Outros jogos** | Demais partidas | Sem CTA | Card neutro — presença de utilidade |

**Por que jogos grandes além do Brasil têm CTA:** o brasileiro assiste à Copa inteira — Argentina, finais, clássicos europeus. Um sábado à tarde com Argentina x França é tão boa oportunidade para chopeira quanto um jogo do Brasil em dia de semana.

---

### Critérios de curadoria: "jogo grande em data boa"

Um jogo não-Brasil recebe destaque e CTA se atender a pelo menos **2 dos 3 critérios**:

**Critério 1 — Data/horário favorável para chopeira**

Dias com alta propensão de receber visita em casa:

| Dia | Propensão | Observação |
|-----|-----------|-----------|
| Sábado | ⭐⭐⭐ Máxima | Dia de festa por excelência |
| Domingo | ⭐⭐⭐ Máxima | Churrasco, reunião familiar |
| Sexta-feira | ⭐⭐ Alta | Começo do fim de semana |
| Feriado (qualquer dia) | ⭐⭐⭐ Máxima | Equivale ao fim de semana |
| Quarta-feira | ⭐ Moderada | Possível se for final ou clássico |
| Segunda/Terça/Quinta | — | Apenas se for Final ou Brasil |

Horário: jogos às 15h BRT ou mais tarde (anteriores não chegam a tempo para chopeira).

**Critério 2 — Time de alto interesse para o brasileiro**

Times que o brasileiro assiste independentemente do Brasil:

- Argentina (rival histórico — assistido sempre)
- Portugal / Cristiano Ronaldo (quando na Copa)
- França, Alemanha, Espanha, Inglaterra (clássicos europeus)
- Seleções africanas com brasileiros naturalizados
- Anfitriã EUA (por curiosidade/volume de torcedores)

**Critério 3 — Peso da fase**

| Fase | Peso inerente |
|------|--------------|
| Final | Máximo — sempre destaque |
| Semifinal | Máximo — sempre destaque |
| Quartas de final | Alto |
| Oitavas de final | Médio |
| Fase de grupos | Só com critérios 1 e 2 |

#### Exemplos de aplicação dos critérios

| Jogo | Data | Critérios atendidos | Destaque? |
|------|------|---------------------|-----------|
| Brasil x Marrocos | Sáb 13/jun 19h | Brasil = automático | ✅ Sempre |
| Argentina x time qualquer | Sáb tarde | Data (Sáb) + Time (Argentina) | ✅ Sim |
| Final da Copa | Dom 19/jul | Fase (Final) + Data (Dom) | ✅ Sempre |
| Semifinal | Seg 14/jul | Fase (Semi) | ✅ Sim |
| França x Alemanha | Qua meio-dia | Apenas Times | ❌ Não |
| Argentina x França | Sáb 15h | Data (Sáb) + Times | ✅ Sim |
| Time A x Time B | Ter 12h | Nenhum | ❌ Não |

**Responsabilidade da curadoria:** a lista de jogos destacados (além do Brasil) é definida antes da Copa e atualizada via CMS conforme os confrontos das fases eliminatórias se confirmam. Não é automático — requer decisão editorial por rodada.

### Estados temporais do schedule

O schedule se comporta diferente dependendo do momento:

| Estado | Comportamento |
|--------|--------------|
| **Jogo futuro** | Card padrão com CTA ativo |
| **Jogo em menos de 24h** | Badge "Amanhã" ou "Hoje" no card + copy de urgência no CTA |
| **Jogo em andamento** | Badge "Ao vivo" no card (sem CTA de chopp — já é tarde) |
| **Jogo encerrado** | Card com placar, visual reduzido (opacidade), sem CTA |
| **Eliminatórias indefinidas** | Placeholder "A definir" até Brasil avançar |

### Bloco de educação do serviço

Antes da lista de jogos, um bloco fixo de 2 linhas apresenta o serviço para quem não conhece:

```
┌────────────────────────────────────────────┐
│  🍺 Chopeira + barril entregues em casa    │
│     Agende com antecedência. Sem           │
│     complicação.                           │
└────────────────────────────────────────────┘
```

Este bloco existe porque ~35% da base não sabe que o serviço existe (survey painel, mar/2025). O schedule é o momento de apresentação — o usuário chegou pela Copa, mas sai sabendo do Chopp em Casa.

### Princípios de design aplicados à Camada 2

**Hick's Law — reduzir o número de escolhas:**
Apenas os jogos do Brasil têm CTA. O usuário não precisa processar 104 cards com botão — o CTA aparece exatamente onde é relevante.

**Fitts's Law — tamanho e proximidade dos alvos:**
Cards com toque em toda a área. CTA principal fixo no bottom (zona verde do polegar). Touch targets mínimos de 44×44pt.

**Recognition over Recall (NNGroup):**
O schedule elimina a necessidade de o usuário lembrar datas e horários dos jogos. A informação está ali — o Chopp aparece como solução contextual, não como interrupção.

**Contextual Relevance (Amazon):**
Jogos passados ficam visíveis mas visualmente distintos (placar + opacidade reduzida). O usuário vê o histórico, mas o foco vai naturalmente para os próximos jogos.

---

## 7. Camada 3 — Destino

O CTA do calendário leva para a **categoria Chopp em Casa** no Zé Delivery. Não foi planejada nenhuma alteração nessa camada nesse MVP — mas há um ponto de atenção crítico herdado do projeto de aniversário:

**Empty state pós-clique: 18,5% de abandono** no teste do banner de aniversário. Usuários clicam e não encontram produto disponível (cobertura geográfica limitada das franquias).

**Recomendação para Copa:** antes de ativar o componente em escala total de base, corrigir o empty state com:
- Mensagem contextualizada ("O Chopp em Casa ainda não chegou na sua região, mas…")
- CTA alternativo para lista de espera ou notificação quando disponível
- Evitar dead end — qualquer dead end na Copa, com volume 10–50× maior, vai gerar ruído

---

## 8. Princípios de Design que Embasam a Arquitetura

### Da Amazon (Leadership Principles + Product Methodology)

| Princípio | Aplicação na solução |
|-----------|---------------------|
| **Customer Obsession** | A arquitetura começa pelo JTBD do usuário, não pelo slot disponível na home |
| **Working Backwards** | Definimos o press release antes de definir o componente |
| **Bias for Action** | Solução mínima viável é V1 (Calendário Passivo) em 1 sprint — não esperar V2 completo |
| **Invent and Simplify** | Reutilizar componente existente (Showcase) em vez de construir nova infraestrutura |
| **Are Right, A Lot** | Decisão baseada em dado existente (CTR 10,22% do banner de aniversário) como proxy |
| **Deliver Results** | KPI claro: GMV Chopp em Q2. Componente medido contra baseline |

### Da Nielsen Norman Group (UX Research)

| Princípio | Aplicação na solução |
|-----------|---------------------|
| **Progressive Disclosure** | Três camadas: banner → calendário → produto. Só o necessário em cada etapa |
| **Visibility of System Status** | Countdown no V2 informa o usuário sobre o tempo restante |
| **Recognition over Recall** | Calendário com data, hora e adversário visíveis — usuário não precisa lembrar |
| **Error Prevention** | Remover jogos passados do calendário para evitar CTAs sem propósito |

### Da Apple Human Interface Guidelines + Google Material Design

| Princípio | Aplicação na solução |
|-----------|---------------------|
| **Contextualize** | Componente só aparece no período da Copa (11/jun–19/jul) |
| **Touch Target 44pt** | Cards e CTAs com área de toque mínima garantida |
| **Bottom Sheet nativo** | Pattern familiar no iOS (UISheetPresentationController) e Android (ModalBottomSheet) |
| **Single Primary Action** | Um CTA por tela. Banner: "Ver calendário". Calendário: "Ir para Chopp em Casa" |

---

## 9. Fluxo de Interação Completo

```
USUÁRIO ABRE O APP (Maio → Julho)
        │
        ▼
    [Home do Zé]
        │
        ├── Banner ativo? (início Maio–19/jul)
        │         │
        │         ├── FASE 1 "Copa vem aí" (início Maio)
        │         │   CTA: "Ver jogos do Brasil →"
        │         │         │
        │         │         ▼
        │         │   [Schedule da Copa — Tela Dedicada]
        │         │   Jogos do Brasil + jogos grandes destacados
        │         │         │
        │         │         ├── Tap em card destacado (Brasil ou jogo grande)
        │         │         │         ▼
        │         │         │   [Chopp em Casa — Categoria/PDP]
        │         │         │
        │         │         ├── Tap em CTA fixo bottom "Ver Chopp em Casa"
        │         │         │         ▼
        │         │         │   [Chopp em Casa — Categoria]
        │         │         │
        │         │         └── Navegar pelo schedule (utilidade pura)
        │         │
        │         ├── FASE 2 "Countdown" (meados Maio)
        │         │   CTA: "Garantir agora →"
        │         │         │
        │         │         ├── Variante A → [Schedule] → [PDP]
        │         │         └── Variante B → [PDP] diretamente (A/B)
        │         │
        │         └── FASE 3 "Urgência" (fim Maio → Copa)
        │             CTA: "Reservar agora" / "Pedir agora"
        │                   │
        │                   ▼
        │           [Chopp em Casa — PDP]
        │           (sem schedule — urgência máxima)
        │
        ├── Usuário acessa Schedule diretamente
        │   (histórico de navegação, link externo)
        │         ▼
        │   [Schedule da Copa — Tela Dedicada]
        │   Mesmo fluxo do tap nos cards
        │
        └── Banner inativo (fora da janela) → home normal
```

---

## 10. Estados de Erro e Edge Cases

| Cenário | Comportamento esperado |
|---------|----------------------|
| Usuário sem cobertura de chopp | CTA de jogo do Brasil mostra empty state contextualizado: "Ainda não chegou na sua região — avise quando quiser saber" |
| Brasil eliminado nas eliminatórias | Schedule continua mostrando os demais jogos da Copa; CTA some dos próximos jogos; card do Brasil mostra resultado final |
| Jogo adiado ou horário alterado | Conteúdo atualizado via CMS — schedule não é hardcoded; horário atualiza automaticamente |
| Usuário acessa schedule após a Copa encerrar | Tela mostra estado final — campeão, resultados — sem CTA de chopp |
| App sem conexão | Schedule em cache com último estado conhecido; badge "ao vivo" não aparece offline |
| Jogos com horário não definido (eliminatórias) | Placeholder "A definir" no horário; CTA aparece quando data/hora for confirmada |
| Usuário quer ver só jogos do Brasil | Filtro ou tab "🇧🇷 Brasil" destaca apenas os jogos do Brasil no schedule |

---

## 11. Estratégia de Awareness por Camada

O problema de awareness (35% não sabem do serviço) não é resolvido por uma única tela — precisa ser distribuído ao longo do funil. Cada camada contribui de forma diferente:

| Camada | O que resolve | Como |
|--------|--------------|------|
| **Showcase (C1)** | Primeiro sinal de existência | Copy que nomeia o produto tangível ("chopp com chopeira") sem assumir conhecimento prévio |
| **Calendário (C2)** | Apresentação do serviço | Bloco de educação de 2 linhas antes dos cards de jogo |
| **Chopp em Casa (C3)** | Confirmação e compra | PDP existente — já explica volumes, preços, prazos |

### O que NÃO fazer (armadilhas de awareness)

| Armadilha | Por que evitar |
|-----------|---------------|
| CTA "Pedir Chopp" sem contexto | Pressupõe que o usuário sabe o que é o serviço — invisível para os 35% |
| "Chopp em Casa" como único label no banner | É o nome interno do produto, não é autoexplicativo para quem nunca viu |
| Foco em benefício de preço/oferta | Está fora do escopo e não é o principal driver de conversão identificado nas pesquisas |
| Banner só no match day | Perde a janela de descoberta pré-Copa, quando o usuário ainda tem tempo de planejar |

### Funil de awareness projetado

```
Base ativa do app (toda)
        │
        ▼  Vê o Showcase Component
~100%   │  "Chopp com chopeira pra Copa"
        │
        ▼  Clica (CTR ~8–12%)
~10%    │  Abre Calendário → vê "o que é"
        │
        ▼  Clica em CTA do Calendário (~40%)
~4%     │  Entra em Chopp em Casa
        │
        ▼  Converte (~0,04% do total de views)
        │
        └─ Associação produto-Copa plantada para 100% que viram o banner
           (incluindo os que não clicaram)
```

**O valor de awareness não está só na conversão.** Cada usuário que viu o banner e *não clicou* ainda assim foi exposto à existência do serviço. Nas próximas semanas da Copa, essa exposição acumula. Esse impacto não aparece na métrica de GMV imediato — mas é real.

---

## 12. Métricas de Sucesso

Herdando o modelo de medição do banner de aniversário, as métricas por camada são:

| Camada | Métrica | Referência (aniversário) | Meta Copa |
|--------|---------|--------------------------|-----------|
| Showcase (C1) | Views | 399.542 | 2M–10M (base total) |
| Showcase (C1) | CTR | 10,22% | ≥8% |
| Calendário (C2) | Abertura / Click | — (novo) | ≥60% dos cliques no banner |
| Calendário (C2) | CTA Click / Abertura | — (novo) | ≥40% |
| Destino (C3) | Purchase / View (C1) | 0,041% | ≥0,040% |
| Destino (C3) | Empty rate pós-clique | 18,5% | ≤10% |
| Global | GMV Copa | — | +R$X M vs. baseline (definir com Guilherme) |

**Nota sobre o funil:** a introdução da Camada 2 (Calendário) cria uma etapa intermediária que pode reduzir a conversão direta comparado ao banner que vai direto para a PDP. Isso deve ser testado via A/B:
- **Variante A:** Banner → Calendário → PDP
- **Variante B:** Banner → PDP diretamente (sem calendário)

O calendário agrega valor de awareness e associação produto-ocasião, mas pode prejudicar conversão direta nos estados de urgência (match day). A hipótese é que no match day, o CTA deve ir direto para a PDP — o calendário é mais valioso nos estados de pré-Copa e entre-jogos.

---

## 13. Roadmap de Entrega Sugerido

**Linha do tempo da campanha:**

```
ABRIL         MAIO                        JUNHO              JULHO
│             │  Fase 1  │  Fase 2  │ Fase 3  │ Copa      │
├─────────────┼──────────┼──────────┼─────────┼───────────┼──────────►
│  Discovery  │  "Copa   │ Countdown│ Últimas │ 13/jun    │ Final
│  + Design   │  vem aí" │ animado  │ unidades│ Jogo 1 BR│ 19/jul
│  + Build    │          │          │         │ 19/jun J2 │
│             │ ◄─── CONVERSÃO EM MAIO ───► │ 24/jun J3 │
```

**Sprints:**

| Sprint | Período alvo | Entregável | Esforço |
|--------|-------------|-----------|---------|
| Sprint 1 | Abril | Banner (C1) — Fase 1 "Copa vem aí": criativo animado, trigger por range de datas, CTA abre Schedule | 1 sprint |
| Sprint 2 | Abril/início Maio | Schedule (C2) — tela dedicada, tabs por fase, cards Brasil + jogos grandes destacados, CTA por card, bloco de educação, CTA fixo no bottom | 1,5 sprint |
| Sprint 3 | Meados Maio | Banner Fase 2 — countdown animado ("Copa em XX dias"), troca de criativo via CMS, A/B Schedule vs. PDP | 0,5 sprint |
| Sprint 4 | Fim Maio | Banner Fase 3 — criativos de urgência/escassez (Variante A e B), CTA direto para PDP | 0,5 sprint |
| Sprint 5 | Antes de 13/jun | Correção do empty state pós-clique + estados temporais dos cards no schedule (Ao vivo, Encerrado, Amanhã) | 0,5 sprint |
| Ongoing | Junho–Julho | Curadoria editorial: atualizar jogos destacados conforme eliminatórias confirmam confrontos | Conteúdo (não eng.) |

**Decisões que precisam ser tomadas antes do Sprint 1:**
- [ ] Confirmar que o componente Showcase suporta troca de criativo por range de datas (CMS ou hardcode)
- [ ] Confirmar slot exclusivo na Showcase para Copa durante Maio–Julho
- [ ] Definir com Guilherme a meta de GMV Chopp em Maio como KPI primário da campanha
- [ ] Alinhar com time de CRM/Braze a lógica de troca de fase (trigger por data)

---

## Referências

### Pesquisas internas (dados de awareness)
- [[context/research-cbze-painel]] — Survey painel mar/2025 (N=2.372): 88% nunca pediram, 35% não sabem do serviço, barreira #1 preço (49%)
- [[context/research-habitos-consumo-jan26]] — Typeform jan/2026 (N=967): confirmação dos dados do painel, estabilidade dos números
- [[context/research-rota-consumidor-chopp]] — Entrevistas qualitativas mar/2025 (N=4): descoberta via app/push, não redes sociais
- [[context/research-csat-pos-compra]] — CSAT pós-compra always-on: satisfação alta (89% nota 5) — o produto em si não é o problema

### Projeto Copa
- [[projects/copa-2026-chopp/context]] — benchmarks e soluções detalhadas
- [[projects/copa-2026-chopp/index]] — projeto principal
- [[research/2026-04-07-calendar-marketing-desk-research]] — desk research: calendar marketing e duas versões da Showcase
- [[projects/regua-aniversario-inapp/index]] — dados do Teste 1 (referência de métricas)

### Referências metodológicas
- Amazon Leadership Principles — customer obsession, working backwards, bias for action
- Clayton Christensen / Tony Ulwick — Jobs to Be Done framework
- Nielsen Norman Group — Progressive Disclosure, Hick's Law, Thumb Zone
- Steven Hoober, "Designing Mobile Interfaces" — thumb zone research
- Apple Human Interface Guidelines — Bottom Sheet, touch targets
- Google Material Design — Modal Bottom Sheet
