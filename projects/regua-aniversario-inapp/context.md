---
type: context
environment: work
sensitive: true
updated: 2026-04-02
---

# Contexto — Régua de Aniversário Inapp

## Problema

Não existe hoje nenhuma comunicação personalizada por ocasião de vida do usuário dentro do Zé Delivery para Chopp. Aniversário é um dos maiores gatilhos de pedido de chopp (festa, reunião de amigos), mas esse momento não é explorado como alavanca de conversão.

## Hipótese

Usuários que têm data de nascimento cadastrada no Zé e nunca compraram Chopp podem ser ativados com uma mensagem contextualizada nos dias próximos ao aniversário — aumentando conversão e introduzindo a categoria para um público que ainda não conhece o produto.

## Público-alvo

- Usuários com data de nascimento cadastrada no Zé Delivery
- Preferência inicial: nunca compraram Chopp (ativação de novos)
- Secundário: já compraram Chopp mas há muito tempo (reativação)

## Solução Definida

Ativação de um **componente existente na home do app Zé Delivery**, disparado **30 dias antes do aniversário do usuário**.

O trigger de D-30 é justificado pela natureza agendada do pedido de Chopp — o usuário precisa de antecedência para planejar a festa. Essa janela posiciona o Chopp como sugestão proativa no momento ideal de decisão.

> Foco exclusivo no app — web fora do escopo desta iniciativa.

## Canais Previstos

- Componente inapp na home (já existente, a ser ativado por trigger de aniversário)
- Push notification como reforço pode ser avaliado numa V2

## Infraestrutura — O que já existe

- **Braze integrada ao site Zé** — entregue em Q1'26 para comunicação transacional, mas a integração cobre o **site**, não o app. É necessário verificar se existe SDK da Braze no app do Zé ou se há outra ferramenta de push/inapp para o canal mobile.

## Perguntas em Aberto

| Pergunta | Status |
|----------|--------|
| O Zé coleta data de nascimento do usuário? Em qual base? | A investigar |
| Qual o volume de usuários com aniversário cadastrado? | A investigar |
| Quem configura o trigger de D-30 no componente da home? (eng ou CRM?) | A investigar |
| O componente da home já suporta personalização de conteúdo por segmento? | A investigar |

## Dados que Embasam a Hipótese

### Aniversário como ocasião de consumo de chopp/cerveja

- **2,8% dos brasileiros iriam a uma festa sem chopp ou cerveja** — pesquisa Chopp Brahma Express. Ou seja, chopp é praticamente obrigatório em festas no Brasil.
- **45% dos brasileiros bebem álcool especificamente em festas e eventos**; 58% consomem em festividades em casa (churrascos, festas) — Mintel Brasil.
- **81% dos consumidores de bebidas alcoólicas no Brasil têm socialização como motivador principal** — pesquisa Diageo/Consumoteca. Aniversário é a ocasião social por excelência.
- **50,41% da população prefere churrasco para confraternizar** — e chopp é o item âncora dessas reuniões.

### Efetividade de campanhas inapp com trigger contextual

- **Campanhas com trigger contextual (event-based) têm open rate de 14,4% vs. 4,19% de campanhas genéricas** — Batch Benchmark 2025. A régua de aniversário é por definição um trigger contextual.
- **Formato pop-up inapp: 12,8% CTR no Android, 11,2% no iOS** — Batch Benchmark 2025.
- **Campanhas com código promocional inapp chegam a 16-17% de CTR** — reforça oportunidade de combinar o componente com uma oferta.
- **In-app messaging cresceu 793% em envios em 2023** — canal em aceleração, com audiência 100% endereçável (não depende de opt-in de push).

### Por que D-30 faz sentido

O pedido de Chopp requer agendamento com antecedência (data de entrega + recolha da chopeira). D-30 posiciona a comunicação exatamente na janela em que o usuário começa a planejar a festa — antes de fechar local, lista de convidados e compras. É uma vantagem competitiva de timing que nenhum concorrente de delivery tradicional consegue explorar da mesma forma.

---

## Posição no Roadmap

- **Q2:** fora do planejamento oficial — iniciativa paralela a validar com Guilherme
- **Q3:** potencial de entrar como frente de lifecycle/CRM, conectada à padronização do pós-compra

## KPI Potencial

- Conversão de novos usuários para Chopp (ativação)
- GMV incremental gerado via régua de aniversário
- CTR das comunicações inapp/push

## Resultados — Teste 1: Banner de Aniversário (App)

> Primeiro experimento rodado com o banner inapp voltado para aniversariantes.

### GMV

- **GMV gerado:** R$ 217k (3% do GMV total do período)
- **Lift de GMV:** +114% para a ocasião aniversário (público e período do teste)

### Funil

| Etapa | Resultado |
|-------|-----------|
| Views | 399.542 |
| Clicks (CTR) | 40.819 — **10,22%** |
| PDP/Click | 10,90% |
| ATC/PDP | 26,78% |
| Checkout/ATC | 97,06% |
| Payment/Checkout | 89,62% |
| Purchase/Payment | 15,93% |
| **Purchase/View** | **0,0413%** (= 4,13 compras / 10k views) |
| Empty após click | 18,46% |

### Métrica de Sucesso

- **Meta:** 0,05 (aniversariantes ativos que compram chopp)
- **Alcançado:** 0,045 — abaixo da meta, mas próximo

### O que Funcionou

- CTR sólida de 10–12%, com picos às **3ª e 5ª-feiras**
- Dias com melhor compra por alcance (purchases/10k views): **8ª (8,67) > 3ª (7,32) > 2ª (7,16)**
- Melhor propensão de compra (Purchase/View) por cluster: **Core (0,052%) > Reativado (0,049%) > ND (0,045%) > Lover (0,045%)**
- Combinações para escalar: Reativado-5ª, Core-3ª/5ª, Lover-2ª/5ª

### Onde Estamos Perdendo

- **Pós-clique é o gargalo #1** — PDP/Click baixo (10,9%) + Empty alto (18,5%)
- **Quarta-feira** atrai muitos cliques (CTR 11,8%), mas converte mal
- **Finais de semana** têm eficiência baixa em compra (≤ 2,4/10k views)
- Purchase/Payment em 15,9% — oportunidade de melhoria no fluxo de checkout

### Oportunidades para V2

- Correção do **pós-clique** (empty state quando produto não está disponível)
- **Personalização por cluster + dia da semana** (heatmap mostra padrões claros)
- Melhoria no **copy do botão** de CTA
- **Content cards** como formato complementar
- Excluir finais de semana ou testar criativos diferenciados para esse período

---

## Referências

- [[index]] — projeto principal
- Q2 Planning — Braze integrada ao site em Q1 como entrega de comunicação transacional
