---
name: fhir-generate
description: Converte os componentes do DAK (l2/*) em FHIR Shorthand (input/fsh/**) para o IG FamilIAr_Ativa. Use após /dak-build.
---

# Skill: fhir-generate (L2 DAK → L3 FSH)

Terceira etapa do pipeline. Gera os artefatos FHIR.

## Pré-requisito
Componentes do DAK em `l2/*`.

## Como executar
Invoque o subagente **`fhir-author`**. Ordem recomendada (validar `sushi .` a cada grupo):
1. Terminologia: `input/fsh/codesystems/`, `input/fsh/valuesets/` (risco ESAS, classificação
   Zarit, tipos de alerta, códigos de observação, LOINC dos domínios ESAS).
2. Profiles: `input/fsh/profiles/` (Observation sintoma/soma ESAS + Zarit; Patient paliativo;
   RelatedPerson cuidador; Flag alerta).
3. Questionnaires ESAS (6 itens 0–10) e Zarit (22 placeholders — ADR-0005) em `input/fsh/instances/`.
4. Lógica: `input/fsh/libraries/` + PlanDefinition em `instances/`.
5. Measure (IND-01..IND-07), CapabilityStatement, Examples.

Siga `docs/cookbooks/l2-to-l3-fhir.md` e as convenções do `CLAUDE.md`.

## Critério de pronto
- `sushi .` com 0 erros; cada FSH com cabeçalho de rastreabilidade; pendências marcadas `REVISAR`.

## Próximo passo
`/ig-build`.
