---
name: expense
description: Registrar gasto manualmente no mês atual. Aceita linguagem natural. Parte do sistema financeiro do second brain.
argument-hint: <descrição do gasto, ex: "uber 35 reais ontem" ou "mercado 180 sexta">
allowed-tools: Read, Edit, AskUserQuestion
---

# /expense - Registrar Gasto

Registra um gasto no arquivo do mês atual em `finance/YYYY-MM.md`.

Input é `$ARGUMENTS`. Hoje é injetado pelo sistema via `currentDate`.

> **Do NOT commit manually.** O hook de PostToolUse auto-commita após Edit.

## Steps

1. **Parse** o input — extrair: valor, categoria, descrição, data
2. **Inferir data** — se não informada, usar hoje; se "ontem/sexta/etc", converter para data absoluta
3. **Inferir categoria** — mapear para as categorias do perfil (ver abaixo)
4. **Abrir arquivo do mês** — `finance/YYYY-MM.md` correspondente à data do gasto
5. **Adicionar linha** na tabela de Gastos Variáveis
6. **Confirmar** o que foi registrado

## Parse de Input

Exemplos de input válido:
- `"uber 35"` → Transporte, R$35, hoje
- `"mercado 180 sexta"` → Alimentação, R$180, sexta-feira passada
- `"restaurante 95 reais dia 25"` → Restaurantes, R$95, dia 25 do mês atual
- `"academia 120 março"` → Saúde, R$120, mês de março
- `"roupa 250 ontem"` → Vestuário, R$250, ontem
- `"dividido com namorada ifood 80"` → Restaurantes, R$40 (metade), hoje — nota: dividido

Se valor não informado → usar AskUserQuestion para perguntar.

## Mapeamento de Categorias

| Keywords | Categoria |
|----------|-----------|
| mercado, supermercado, hortifruti, feira | Alimentação |
| restaurante, ifood, delivery, lanche, pizza, sushi | Restaurantes / delivery |
| uber, 99, gasolina, estacionamento, metrô, ônibus, passagem | Transporte |
| farmácia, médico, academia, plano de saúde, consulta | Saúde |
| bar, cinema, show, viagem, passeio, entretenimento | Lazer |
| roupa, sapato, loja, shopping, vestuário | Vestuário |
| (qualquer outro) | Outros |

Se ambíguo (confiança < 0.7), perguntar com AskUserQuestion antes de registrar.

## Formato da Linha na Tabela

A tabela de Gastos Variáveis no arquivo do mês tem este formato:

```markdown
| Categoria | Data | Descrição | Valor | Split? |
|-----------|------|-----------|-------|--------|
| Alimentação | 28/03 | Mercado Extra | R$ 180 | — |
| Transporte | 28/03 | Uber | R$ 35 | — |
| Restaurantes / delivery | 27/03 | iFood (dividido) | R$ 40 | 50/50 |
```

Se a tabela ainda não existe no arquivo, criá-la antes de adicionar a linha.

## Atualizar Totalizador

Após adicionar a linha, atualizar o total da categoria na seção **Gastos Variáveis** se houver linha de total.

## Divisão com Namorada

Se o gasto for dividido (keywords: "dividido", "metade", "split", "50/50"):
- Registrar apenas a metade (valor / 2)
- Marcar coluna Split com "50/50"
- Se ela pagou e vai te cobrar → registrar o valor cheio e marcar Split com "a reembolsar"

## Resposta

Confirmar em uma linha:
```
Registrado: Alimentação — Mercado Extra — R$ 180 — 28/03
```
