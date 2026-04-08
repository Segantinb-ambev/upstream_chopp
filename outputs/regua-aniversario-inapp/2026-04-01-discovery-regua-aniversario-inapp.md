[Discovery] Régua de Aniversário Inapp — Chopp em Casa

Owner: SEGANTIN, BRUNO <BRUNO.SEGANTIN@AB-Inbev.com> | Rocha, Guilherme <Guilherme.Rocha@ab-inbev.com>
Data: Abr/2026
Status: Em andamento
Objetivo do documento: consolidar contexto, problema, tamanho da oportunidade, insights de pesquisa, hipóteses e plano de discovery para embasar a decisão de avançar (ou não) com uma régua de aniversário inapp para Chopp em Casa no Zé Delivery.

---

## Sumário Executivo

Aniversário é a segunda maior ocasião de consumo de Chopp em Casa no Brasil — atrás apenas de churrasco — mas hoje o Zé Delivery não faz nada para estar presente nesse momento. Não há comunicação personalizada, não há gatilho de produto, não há nenhum ponto de contato entre o app e o maior evento social da vida do usuário. Essa lacuna representa uma oportunidade concreta de ativação: usuários com data de nascimento cadastrada no Zé podem ser abordados com 30 dias de antecedência — janela alinhada com o comportamento comprovado de planejamento de Chopp — por meio de um componente já existente na home do app, sem a necessidade de desenvolver nova infraestrutura.

A iniciativa não está no planejamento de Q2, mas pode ser executada como frente paralela de baixo custo de implementação e alto potencial de impacto em GMV incremental. O discovery a seguir consolida os dados que embasam essa hipótese, define a solução proposta e apresenta o plano de validação necessário antes de qualquer decisão de build.

---

## 1. Contexto Geral

O Chopp em Casa é um serviço de agendamento de chopeira e barril operado por franquias do Chopp Brahma Express, vendido via app e site do Zé Delivery. Diferente de um pedido de delivery convencional, o Chopp tem natureza de planejamento: o cliente escolhe data, define litragem e aguarda confirmação da franquia — um fluxo que exige antecedência e intenção ativa.

Hoje, toda a jornada de compra é reativa: o usuário descobre o produto por banner sazonal, navegação ou push genérico, e decide por conta própria quando e para qual ocasião comprar. Não há qualquer personalização baseada em momento de vida ou evento futuro.

O serviço está em crescimento. O Share do Zé Delivery no volume total de Chopp saiu de 1,8% em janeiro de 2025 para 44,8% em novembro de 2025. O Q1 de 2026 fechou com GMV de R$59,94M — superando o desafio de R$39M. O canal digital está ganhando relevância, mas a base de clientes que comprou pelo Zé ainda representa uma fração pequena do universo de consumidores de chopp no Brasil.

---

## 2. O Problema

**Do ponto de vista do cliente**

O usuário que vai fazer aniversário começa a planejar a festa com semanas de antecedência. Ele pensa em local, convidados, comida — e inevitavelmente, em bebida. Pesquisa qualitativa com consumidores (Rota do Consumidor, mar/2025) mostrou que o planejamento de Chopp ocorre com 1 mês ou mais de antecedência, motivado pelo medo de não ter disponibilidade na data. Apesar dessa intenção, o Zé Delivery não aparece nesse momento: não há comunicação, não há lembrança, não há sugestão contextualizada.

O resultado é que o usuário chega ao Zé por iniciativa própria — ou não chega. Uma parcela significativa simplesmente não descobre a opção ou não a associa ao contexto de aniversário.

**Do ponto de vista do negócio**

O maior gap está na ativação: 88% dos consumidores de chopp no Brasil nunca pediram via Zé Delivery (CBZe Painel, N=2.372, mar/2025). O produto existe, o canal existe, a ocasião existe — mas não há conexão entre eles no momento certo. Aniversário é a janela mais previsível e de maior intenção de compra de chopp, e hoje ela passa sem nenhuma atuação ativa do produto.

---

## 3. Princípios Orientadores (Tenets)

Antes de detalhar a solução, estes princípios guiam as decisões de produto desta iniciativa:

1. **Momento antes de canal.** A régua existe porque o momento (aniversário) é relevante — não para explorar um canal de notificação. Se o dado de aniversário não for confiável ou o componente de home não for o meio certo, a solução muda. O princípio não muda.

2. **Relevância antes de volume.** Prefira uma mensagem altamente contextualizada para um segmento menor do que uma campanha genérica para toda a base. O trigger de D-30 só tem valor se a comunicação for específica o suficiente para parecer feita para aquela pessoa.

3. **Infraestrutura existente antes de nova construção.** A hipótese de quick win depende de usar o que já existe (componente de home, dados de aniversário já coletados). Qualquer solução que exija nova infraestrutura muda o escopo e o risco do projeto.

4. **Discovery antes de decisão.** Avançar para build só após validar os dados e a viabilidade operacional. O custo de descobrir que o Zé não coleta data de nascimento depois de planejar a solução é maior do que investigar isso primeiro.

---

## 4. Como o Problema se Manifesta Hoje (AS IS)

Não existe nenhuma régua de comunicação por ocasião de vida do usuário no Zé Delivery para Chopp. O fluxo atual é inteiramente dependente de intenção ativa do cliente:

- Usuário abre o app e navega até Chopp por conta própria
- Descobre por banner sazonal, showcase ou pesquisa
- Não recebe nenhum estímulo baseado em data de nascimento ou evento futuro
- Franquias não têm visibilidade sobre usuários com aniversário próximo

Do ponto de vista operacional, o pedido de Chopp exige agendamento com antecedência: o cliente escolhe data de entrega e recolha, e a franquia confirma disponibilidade. Isso cria uma janela de planejamento que hoje não é aproveitada como ponto de entrada no funil.

---

## 5. Dados que Embasam a Oportunidade

### 5.1 Aniversário como ocasião de consumo de Chopp

| Fonte | Dado |
|-------|------|
| CBZe Painel (N=2.372, mar/2025) | Aniversário é a **2ª maior ocasião** de uso de chopp, atrás de churrasco (55%) |
| Chopp 24h Survey (N=54, mar/2026) | **38% dos usuários** que pediram Chopp 24h usaram para aniversário |
| Chopp Brahma Express (pesquisa interna) | **2,8% dos brasileiros** iriam a uma festa sem chopp ou cerveja |
| Diageo / Consumoteca | **81% dos consumidores** de bebidas alcoólicas têm socialização como motivador principal |
| Mintel Brasil | **45% dos brasileiros** bebem álcool especificamente em festas e eventos |

Leitura-chave: aniversário não é uma ocasião hipotética — é a segunda maior razão declarada para pedir Chopp no Zé. Já existe demanda; o que não existe é o produto se posicionando nela.

### 5.2 Comportamento de planejamento confirma o timing de D-30

Pesquisa qualitativa com consumidores (Rota do Consumidor, mar/2025) identificou planejamento antecipado como comportamento dominante: todos os entrevistados fizeram o pedido com 1 mês ou mais de antecedência, motivados pelo medo de indisponibilidade. Esse dado valida a escolha de D-30 como trigger: é o momento em que o usuário começa a planejar ativamente — antes de fechar local, lista de convidados e compras.

Nenhum concorrente de delivery tradicional consegue explorar esse timing da mesma forma, pois não têm o modelo de agendamento do Chopp.

### 5.3 Gap de ativação digital

| Dado | Valor |
|------|-------|
| Consumidores de chopp que nunca pediram via Zé | **88%** (CBZe Painel) |
| Principal barreira para não pedir no Zé | **Preço (49%)** + desconhecimento (35%) |
| Usuários que relataram descoberta via push/app | **Maioria** (Rota do Consumidor) |

Leitura: a base de usuários elegíveis é enorme. O gap entre consumo e conversão digital é de 88 pontos percentuais. Uma régua de aniversário atua exatamente nesse gap: encontra o usuário no momento de maior intenção com uma mensagem contextualizada.

### 5.4 Performance de campanhas inapp com trigger contextual

| Benchmark | Valor | Fonte |
|-----------|-------|-------|
| Open rate — push contextual (trigger) | **14,4%** | Batch 2025 |
| Open rate — push genérico | **4,19%** | Batch 2025 |
| CTR inapp pop-up (Android) | **12,8%** | Batch 2025 |
| CTR inapp pop-up (iOS) | **11,2%** | Batch 2025 |
| CTR inapp com promo code | **16–17%** | Batch 2025 |

Campanhas com trigger contextual têm open rate 3,4× maior do que campanhas genéricas. A régua de aniversário é por definição um trigger contextual de alta relevância — o que posiciona essa iniciativa no topo da curva de performance esperada.

---

## 6. Working Backwards — Como o Sucesso Se Parece

*Este trecho descreve o estado futuro desejado, escrito como se já tivesse sido entregue. É uma técnica Amazon de alinhamento de visão antes de começar o desenvolvimento.*

---

**Comunicado Interno — [Data futura]**

A squad de Chopp Consumer lançou a Régua de Aniversário Inapp: um componente personalizado na home do Zé Delivery que aparece automaticamente 30 dias antes do aniversário de cada usuário, sugerindo Chopp em Casa para a celebração.

A solução utilizou o componente de home já existente no app, ativado por trigger de data de nascimento coletada no cadastro do Zé. Nenhuma nova infraestrutura foi necessária. O componente exibe uma mensagem contextualizada ("Seu aniversário está chegando — que tal celebrar com chopp em casa?") com CTA direto para a PDP de Chopp.

No primeiro mês de operação, o componente gerou X pedidos incrementais de Chopp, representando R$Y de GMV adicional. A taxa de clique ficou em Z%, acima do benchmark de inapp de 12,8%. Entre os usuários impactados, W% eram compradores de primeira vez na categoria — validando a hipótese de ativação.

---

## 7. A Solução Proposta

**Mecanismo:** ativação do componente existente na home do app Zé Delivery, disparado automaticamente 30 dias antes do aniversário do usuário.

**Fluxo esperado:**
1. Sistema identifica usuários com data de nascimento registrada e aniversário em D+30
2. Componente de home é ativado com conteúdo personalizado de aniversário
3. CTA direciona para PDP de Chopp em Casa
4. Usuário agenda pedido normalmente pelo fluxo existente

**Por que D-30 e não outra janela:**
O pedido de Chopp exige agendamento. D-30 é o momento em que o planejamento começa (validado por pesquisa qualitativa). D-7 seria tarde demais — a data pode já estar comprometida pela franquia. D-60 seria cedo demais — o usuário ainda não está em modo de planejamento de festa.

**Foco exclusivo no app — web fora do escopo desta iniciativa.**

**V2 (fora do escopo atual):** push notification como reforço antes do aniversário.

---

## 8. Tamanho da Oportunidade (Sizing Inicial)

*Nota: os números abaixo são estimativas de ordem de grandeza. A validação das premissas é parte do plano de discovery.*

**Premissas:**
- Total de usuários ativos no Zé Delivery com histórico de compra: base interna (a confirmar)
- % com data de nascimento cadastrada: **a investigar** — premissa inicial de 30–50% da base
- Ticket médio de pedido de Chopp: ~R$ 450 (30L mínimo)
- CTR esperado do componente inapp (baseline benchmark): ~12%
- Conversão CTR → pedido: estimativa 20–30% (conservadora, dado contexto de alta intenção)

**Cenário conservador (premissas baixas):**

| Métrica | Valor |
|---------|-------|
| Usuários com aniversário/mês (estimado) | [base × 1/12] |
| Com data de nascimento cadastrada (30%) | [sub-segmento] |
| CTR esperado (12%) | [impressões × CTR] |
| Conversão para pedido (20%) | [cliques × conv.] |
| GMV por pedido | R$ 450 |
| **GMV incremental mensal estimado** | **A calcular após validar base** |

*Ação necessária: obter da engenharia ou dados o volume de usuários com data de nascimento cadastrada para completar o sizing.*

---

## 9. Insights-Chave do Discovery (até agora)

1. **Aniversário é a segunda maior ocasião declarada para Chopp** — não é uma aposta, é comportamento confirmado em pesquisa quantitativa com N=2.372.
2. **38% dos usuários do Chopp 24h já usaram o serviço para aniversário** — demanda real, não latente.
3. **O planejamento começa com 1 mês de antecedência** — D-30 não é arbitrário, é comportamental.
4. **O componente de home já existe** — a hipótese de quick win depende de não precisar construir do zero.
5. **88% dos consumidores de chopp nunca pediram no Zé** — o público elegível é enorme.
6. **Campanhas contextuais têm 3,4× mais open rate** — o modelo de trigger é mais eficiente do que qualquer campanha genérica.

---

## 10. Hipóteses de Produto

**H1: Existe demanda real de Chopp para aniversário entre usuários cadastrados no Zé**
Evidência existente: 38% dos usuários do Chopp 24h declararam aniversário como ocasião. CBZe Painel confirma aniversário como 2ª ocasião. Confiança: alta.

**H2: D-30 é a janela ideal para ativar o usuário**
Evidência existente: comportamento qualitativo de planejamento com 1 mês+. Confiança: média — é uma inferência de pesquisa qualitativa, não um teste direto.

**H3: O componente de home existente é suficiente para gerar conversão sem nova infraestrutura**
Evidência existente: nenhuma. Confiança: baixa — depende de validação técnica.

**H4: O Zé Delivery coleta e armazena data de nascimento de forma acessível para trigger automatizado**
Evidência existente: nenhuma. Confiança: desconhecida — é a principal incógnita do projeto.

---

## 11. Perguntas em Aberto (FAQ Antecipado)

**P: O Zé coleta data de nascimento dos usuários?**
R: A investigar com engenharia ou dados. Se não coletado ou não acessível, o escopo muda completamente — a solução passa a depender de coleta ativa de dados, o que aumenta complexidade e prazo.

**P: Qual o volume de usuários com aniversário cadastrado?**
R: Crítico para o sizing. Sem esse número, não há como calcular GMV incremental com confiança.

**P: Quem configura o trigger no componente de home — engenharia ou CRM?**
R: Define se isso é uma sprint de tech ou uma configuração de ferramenta. Impacta diretamente o custo de implementação.

**P: O componente de home suporta personalização de conteúdo por segmento?**
R: Se não suportar, a solução deixa de ser um quick win e passa a exigir desenvolvimento.

**P: Por que não usar push notification ao invés de inapp?**
R: Inapp não depende de opt-in e atinge 100% da audiência endereçável. Push tem opt-in de 56–67% (Batch 2025) e é mais intrusivo. Push como reforço vai para V2, após validar o canal principal.

**P: Por que não é Q2?**
R: Iniciativa fora do planejamento oficial. A decisão de incluir em Q2 depende do resultado deste discovery — especialmente da validação técnica de H3 e H4. Se forem positivas, o custo de implementação pode ser pequeno o suficiente para caber em Q2 como frente paralela.

---

## 12. Plano de Discovery

**Escopo do discovery:**
- Viabilidade de dados (H4)
- Viabilidade técnica do componente (H3)
- Validação do timing D-30 (H2)
- Sizing real da oportunidade

**Atividade 1 — Investigação de dados: coleta de aniversário**
Responsável: Rocha, Guilherme + Engenharia

- Verificar se o Zé Delivery coleta data de nascimento no cadastro
- Checar base e % de usuários com esse campo preenchido
- Verificar acessibilidade do dado para trigger automatizado

**Atividade 2 — Investigação técnica: componente de home**
Responsável: SEGANTIN, BRUNO + Engenharia

- Mapear como o componente de home é ativado hoje
- Verificar se suporta segmentação por atributo de usuário (data de nascimento)
- Estimar esforço de configuração vs. desenvolvimento

**Atividade 3 — Sizing real da oportunidade**
Responsável: Rocha, Guilherme + Dados

- Com base nos dados de aniversário disponíveis, calcular: usuários elegíveis/mês, GMV incremental estimado por cenário de CTR e conversão

**Atividade 4 — Decisão de priorização**
Responsável: SEGANTIN, BRUNO + Rocha, Guilherme

- Com os resultados das atividades 1–3, decidir: avançar para build em Q2 como frente paralela, ou incluir no planejamento de Q3.

---

## 13. Cronograma Proposto (Discovery)

| Atividade | Descrição | Início | Fim |
|-----------|-----------|--------|-----|
| Investigação de dados | Verificar coleta e volume de datas de nascimento | Semana 1 de abr | Semana 1 de abr |
| Investigação técnica | Mapear componente de home e esforço de config | Semana 1 de abr | Semana 2 de abr |
| Sizing real | Calcular GMV incremental com dados reais | Semana 2 de abr | Semana 2 de abr |
| Decisão de priorização | Avançar para Q2 paralelo ou Q3 | Semana 2 de abr | Semana 2 de abr |

---

## 14. Critério de Sucesso do Discovery

- Clareza sobre disponibilidade e volume de dados de aniversário
- Confirmação de viabilidade técnica do componente sem novo desenvolvimento
- Sizing real calculado com dados internos
- Decisão documentada: avançar para Q2 (paralelo) ou Q3

---

## 15. Referências Consolidadas

**CBZe Painel (N=2.372, mar/2025)**
Survey quantitativo de painel com consumidores adultos. Dado-chave: aniversário é a 2ª maior ocasião de uso de chopp; 88% dos consumidores nunca pediram no Zé.

**Rota do Consumidor: Chopp Brahma (mar/2025)**
Entrevistas qualitativas com 4 compradores via Zé (Beth, Verônica, Eduardo, Jennifer). Dado-chave: planejamento com 1 mês+ de antecedência como comportamento dominante.

**Chopp 24h: Validação de Entrega no Mesmo Dia (mar/2026)**
Survey com N=54 usuários do Chopp 24h. Dado-chave: 38% usaram o serviço para aniversário — principal ocasião declarada.

**CSAT Pós-Compra de Chopp (always-on, N=255+)**
Survey de satisfação contínuo. Dado contextual: NPS altíssimo, chopp é percebido como "luxo acessível" que eleva a experiência da festa.

**Batch Push Notification Benchmark 2025**
Benchmark de mercado. Dado-chave: campanhas contextuais (trigger) têm 14,4% de open rate vs. 4,19% para genéricas; CTR inapp pop-up de 12–13%.

**Chopp Brahma Express — A Festa Perfeita (pesquisa interna CBE)**
Dado-chave: 2,8% dos brasileiros iriam a uma festa sem chopp ou cerveja.

**Context: Régua de Aniversário Inapp**
→ `projects/regua-aniversario-inapp/context.md`
