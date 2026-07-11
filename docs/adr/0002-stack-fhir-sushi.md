# ADR-0002 — Stack L3: FHIR R4 + FSH/SUSHI + IG Publisher

- **Status:** Aceito (2026-07-10) — herdado do template mareIA-ig (ADR-0002)

## Contexto
Precisamos gerar artefatos máquina-legíveis interoperáveis com o SUS Digital. O DAK (RNF-04)
define **HL7 FHIR R4** com LOINC, SNOMED CT e CID-10, e integração e-SUS APS/RNDS.

## Decisão
- **FHIR R4 (4.0.1)** como versão base (compatível com RNDS; ver também ADR-0008).
- **FSH + SUSHI** como linguagem-fonte dos artefatos (legível, versionável, padrão WHO/HL7).
- **IG Publisher** (HL7) para gerar o site e rodar o QA.
- Dependências: `hl7.fhir.uv.sdc` (Questionnaire/score) e `hl7.fhir.uv.cpg` (PlanDefinition/Library).
- Template de apresentação: `fhir2.base.template` (ver ADR-0007).

## Consequências
- (+) Pipeline reprodutível e validável; ecossistema maduro.
- (−) IG Publisher exige Java 11+ e download de pacotes (rede). Build de FSH (SUSHI) é leve e roda
  sem Java — usado como gate rápido.
