# ADR-0008 — FHIR R4 apesar da menção ao Starter Kit R5 no DAK

- **Status:** Aceito (2026-07-10)

## Contexto
A capa do DAK fonte cita o "SMART Guidelines Starter Kit v2.0.0 (WHO / HL7 **FHIR R5**)", mas o
requisito de interoperabilidade RNF-04 (§9.2) determina "Dados modelados em **HL7 FHIR R4**.
Integração com e-SUS APS e RNDS via padrão FHIR".

## Decisão
Adotar **FHIR R4 (4.0.1)**, priorizando o requisito normativo RNF-04 e a compatibilidade com a
RNDS e com o template. A menção ao Starter Kit R5 é tratada como referência metodológica (os 9
componentes do DAK), não como requisito de versão FHIR.

## Consequências
- (+) Compatível com RNDS/e-SUS APS e com o ecossistema atual do SUS Digital.
- (−) `ActorDefinition` e `Requirements` (R5) indisponíveis nesta fase (ver ADR-0006); mitigado
  por documentação no L2 e `CapabilityStatement` kind=requirements.
- Migração futura a R5/template SMART da WHO possível sem perda dos FSH (revisar bindings).
