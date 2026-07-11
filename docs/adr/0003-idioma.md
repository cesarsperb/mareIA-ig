# ADR-0003 — Idioma dos artefatos

- **Status:** Aceito (2026-07-10) — herdado do template mareIA-ig (ADR-0003)

## Contexto
O DAK fonte é PT-BR. FHIR convenciona ids/nomes técnicos em ASCII/inglês, mas suporta conteúdo
localizado.

## Decisão
- `language: pt-BR` no IG.
- **Conteúdo visível** (`title`, `description`, `display`, textos de `Questionnaire`, narrativa
  do IG) em **PT-BR**.
- **Identificadores técnicos** (`id`, `name`, nomes de FSH, URLs canônicas) em **ASCII/inglês**.
- Códigos de CodeSystems locais: código ASCII curto + `display` PT-BR
  (ex.: `familiarativa-esas-risk#alto` "Alto").

## Consequências
- (+) IG legível para a equipe clínica brasileira; ids estáveis e válidos.
- (−) Dupla convenção exige atenção; mitigado por exemplos em `docs/cookbooks/`.
