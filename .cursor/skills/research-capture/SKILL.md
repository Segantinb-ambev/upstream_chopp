---
name: research-capture
description: Processa um arquivo bruto de pesquisa (transcrição de áudio, notas, export) e gera dois arquivos: transcrição organizada e legível em research/ e resumo + índice em context/. Nenhuma informação é cortada ou filtrada. Use quando o usuário quiser adicionar uma pesquisa ao vault.
---

# research-capture — Processamento de Pesquisa

Transforma input bruto em dois arquivos: um transcript completo e legível, e um resumo leve para contexto de LLM.

**Princípio:** nenhuma informação é removida. O transcript é o arquivo original reorganizado para leitura — não filtrado.

## Input aceito

- Caminho para arquivo já no vault (ex: `_temp/entrevistas-chopp.md`)
- Conteúdo colado diretamente na conversa
- Arquivo em qualquer pasta do vault

## Passos

1. **Ler** `context/business-profile.md` para entender o contexto do produto
2. **Ler** o arquivo bruto na íntegra
3. **Identificar participantes** e atribuir códigos neutros:
   - P1–Pn → usuários/clientes
   - F1–Fn → franqueados
   - E1–En → equipe interna
   - Pesq → pesquisador/entrevistador
4. **Identificar temas** presentes no conteúdo (não inventar — emergir do material)
5. **Gerar** `research/YYYY-MM-[slug]-transcript.md` — transcrição completa organizada
6. **Gerar** `context/research-[slug].md` — resumo e índice

## Formato: research/YYYY-MM-[slug]-transcript.md

Transcrição completa. Nada é cortado. Organizada por sessão/participante com cabeçalhos claros e fluxo de pergunta/resposta preservado.

```markdown
---
type: research
environment: work
sensitive: true
date: YYYY-MM-DD
method: entrevistas | survey | teste-usabilidade | desk-research | misto
participants: N
source: [nome do arquivo original ou "colado na conversa"]
---

# [Nome da Pesquisa] — Transcript Completo

## Participantes

| Código | Perfil |
|--------|--------|
| P1 | Descrição do perfil (ex: cliente, comprou via app, SP) |
| F1 | Descrição do perfil (ex: franqueado, região Sul, 3 anos) |

---

## Sessão 1 — P1 | YYYY-MM-DD

**Pesq:** Pergunta do entrevistador.

**P1:** Resposta completa do participante, exatamente como foi dita.
Pode ter múltiplos parágrafos se necessário.

**Pesq:** Próxima pergunta.

**P1:** Resposta.

---

## Sessão 2 — F1 | YYYY-MM-DD

**Pesq:** Pergunta.

**F1:** Resposta.
```

## Formato: context/research-[slug].md

Resumo leve. Sem transcrição, sem quotes longos. Só o suficiente para o LLM entender o que existe e onde buscar.

```markdown
---
type: context
environment: work
sensitive: true
updated: YYYY-MM-DD
transcript: research/YYYY-MM-[slug]-transcript.md
---

# Índice — [Nome da Pesquisa]

## O que é

Método, número de participantes, período, objetivo da pesquisa em 2–3 linhas.

## Participantes

| Código | Perfil |
|--------|--------|
| P1 | Perfil resumido |
| F1 | Perfil resumido |

## Temas cobertos

- Tema 1
- Tema 2
- Tema 3

## Achados principais

1. **Achado** — uma linha com o insight central
2. **Achado** — uma linha com o insight central

## Implicações de design

- Implicação direta para decisões de produto/design

## Como navegar o transcript

| Para encontrar... | Ver |
|-------------------|-----|
| Tema 1 | `research/YYYY-MM-[slug]-transcript.md#tema-1` |
| Sessão de P1 | `research/YYYY-MM-[slug]-transcript.md#sessão-1--p1` |
| Sessão de F1 | `research/YYYY-MM-[slug]-transcript.md#sessão-2--f1` |
```

## Sensibilidade

Sempre `sensitive: true` em ambos os arquivos.

## Commit

```bash
git add research/<arquivo>.md context/<arquivo>.md
git commit -m "cos: new research - [slug]"
```
