---
name: l1-extract
description: Extrai os fatos clínicos do DAK fonte (L1) para l2/_l1-facts.yaml, base de todo o pipeline DAK. Use quando a fonte em sources/ mudar ou para iniciar a adaptação.
---

# Skill: l1-extract (L1 → fatos normalizados)

Primeira etapa do pipeline agêntico do IG FamilIAr_Ativa.

## Quando usar
- Início da adaptação, ou quando `sources/` (DAK/Documento de Requisitos) for atualizado.

## Como executar
1. Garanta que `sources/_dak_extract.txt` existe (se só houver PDF, extraia com PyMuPDF e
   grave em UTF-8 — ver `docs/hard-earned-lessons.md` HEL-001).
2. Invoque o subagente **`l1-extractor`** (Agent tool, subagent_type `l1-extractor`).
3. Saída esperada: `l2/_l1-facts.yaml` com `recommendations, dhi_who, actors, data_elements,
   decision_rules, business_processes, indicators, requirements`, cada item com `source`.

## Critério de pronto
- YAML válido; ambiguidades marcadas `status: review` + ADR; nada inventado além da fonte
  (em especial: itens do ZBI-22 não são transcritos — ADR-0005).

## Próximo passo
`/dak-build`.
