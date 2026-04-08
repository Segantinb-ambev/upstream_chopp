---
type: context
environment: work
sensitive: true
updated: 2026-03-31
source: Figma — Master-Chopp-2025
---

# Jornada de Compra — Chopp no Zé Delivery

> Mapeamento da jornada do usuário para comprar Chopp dentro do app/web Zé Delivery. Atualizar após mudanças significativas no fluxo.

## Fluxo Completo

```
Ponto de Entrada → PDP → Adicionar ao Carrinho → Confirmação de Endereço
→ Sacola (Agendar Entrega + Recolha) → Forma de Pagamento → Confirmação
→ Acompanhamento → Entrega → Pós-venda (WhatsApp)
```

## Pontos de Entrada (5 caminhos)

1. **Categoria Cervejas** — produtos de cerveja incluindo chopp
2. **Categoria Chopp** — categoria dedicada exclusivamente a chopp
3. **Categoria Churrasco** — contexto de consumo que inclui chopp
4. **Marcas que amamos → Brahma / Chopp Brahma** — entrada por marca
5. **Banner Sazonal na Showcase (home)** — temporário/sazonal

## Etapas Críticas e Diferenciais

### Confirmação de Endereço (ao adicionar ao carrinho)
- Disparada ao adicionar chopp ao carrinho
- Razão: usuários frequentemente entregam chopp em endereço diferente de casa
- **Resultado:** zerou cancelamentos relacionados a endereço incorreto

### Sacola — Configuração de Entrega (obrigatória)
Usuário deve definir 3 informações antes de prosseguir:
1. **Data de entrega** — dia em que o chopp será entregue
2. **Horário de entrega** — janela de recebimento
3. **Data de recolha** — devolução da chopeira (comodato)

### Pós-venda via WhatsApp
- Loja entra em contato diretamente após confirmação do pagamento
- Objetivos: confirmar documentos, esclarecer detalhes de entrega/recolha
- **Processo manual e externo ao app** — pain point conhecido, frente planejada para Q3

## Pain Points Atuais

| Pain Point | Status |
|------------|--------|
| Agendamento complexo (3 campos: entrega + horário + recolha) | Aberto |
| Validação de documentos via WhatsApp (fora do app) | Aberto — Q3 |
| Aguardo de confirmação da loja após pedido | Aberto |
| 5 pontos de entrada podem fragmentar descoberta | Em análise |
| Endereço incorreto | ✅ Resolvido |

## Oportunidades Mapeadas

- **Simplificar agendamento:** sugerir datas populares ou pacotes pré-configurados
- **Integrar validação de documentos:** trazer verificação para dentro do app (Q3)
- **In-app notifications:** trazer atualizações de status que hoje vão por WhatsApp
- **Recompra simplificada:** sugerir recompra com base em histórico
- **Tutorial de primeira compra:** explicar processo de comodato para novos usuários

## Referência Figma

Projeto: **Master-Chopp-2025** — [node-id=1:10421](https://www.figma.com/design/2YWOMBzsyN6tHIkMwEczYu/Master-Chopp-2025?node-id=1-10421)
