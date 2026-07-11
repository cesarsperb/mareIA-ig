# ADR-0006 — Representação de personas no L3 (R4 não tem ActorDefinition)

- **Status:** Aceito (2026-07-10) — herdado do template mareIA-ig (ADR-0006)

## Contexto
O mapeamento DAK→FHIR prevê `ActorDefinition` para personas. Porém `ActorDefinition` é um recurso
**FHIR R5**; este IG usa **R4** (ADR-0002/0008, por compatibilidade com a RNDS).

## Decisão
Nesta fase, as personas (componente 2 do DAK) permanecem **documentadas no L2**
(página `l2-personas`). Não serão criados recursos de ator no L3.
O `CapabilityStatement` (kind=requirements) referencia os perfis usados por cada papel.

Quando/se o IG migrar para R5 (ou adotar o template SMART da WHO), criar um `ActorDefinition` por
persona, mantendo os ids já reservados (`caregiver`, `patient-selfcare`, `health-professional`,
`sus-manager`).

## Consequências
- (+) Evita abuso semântico (ex.: usar `Group` como ator) e mantém o build R4 limpo.
- (−) Atores não aparecem como artefatos navegáveis do IG nesta fase.
