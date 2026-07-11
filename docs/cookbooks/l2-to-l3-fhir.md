# Cookbook — L2 (DAK) → L3 (FHIR/FSH)

## Mapeamento
| L2 | L3 (FSH em `input/fsh/`) |
|---|---|
| Personas | documentadas no L2 (R4 — ADR-0006); papéis refletidos no `CapabilityStatement` |
| Processos | BPMN (`l2/`) + `instances/` → `PlanDefinition` (workflow) |
| Dicionário de dados | `valuesets/`+`codesystems/` (terminologia), `profiles/` (StructureDefinition), `instances/` (`Questionnaire` ESAS/Zarit) |
| Lógica de decisão | `libraries/` (CQL) + `instances/` (`PlanDefinition` com `action`/`condition`) |
| Alertas | `profiles/` → `Flag` (tipo em `familiarativa-alert-type`; status active/inactive) |
| Indicadores | `instances/` → `Measure` (IND-01..IND-07) |
| Requisitos | `instances/` → `CapabilityStatement` / `Requirements` |

## Passos (`/fhir-generate`)
1. **Terminologia primeiro:** CodeSystems/ValueSets locais (risco ESAS, classificação Zarit,
   tipos de alerta, códigos de observação) + ValueSet LOINC dos domínios ESAS (ADR-0004).
2. **Questionnaires:** ESAS com 6 itens `integer` 0–10 (extensões `minValue`/`maxValue`) e código
   LOINC por item; Zarit com 22 itens placeholder (ADR-0005), linkIds `z01..z22`.
3. **Profiles:** `Observation` para sintoma ESAS, soma+risco ESAS (componente, código distinto —
   invariante `obs-7`) e pontuação Zarit (classificação em `interpretation`); `Patient` paliativo;
   `RelatedPerson` cuidador; `Flag` alerta clínico.
4. **Decisão:** `Library` (regras humano-legíveis; CQL na fase L4); `PlanDefinition` referencia a
   Library e define ações (registrar, classificar, alertar, agendar) com `condition` fhirpath.
5. **Indicadores:** um `Measure` por indicador — `proportion` (IND-01/02/03/04/06) e
   `continuous-variable` (IND-05/07).
6. **Validar incrementalmente:** rode `sushi .` após cada grupo; 0 erros antes de seguir.

## Convenções
- Ids: `familiarativa-<artefato>` (kebab-case). Ver ADR-0003 (idioma) e `CLAUDE.md` §4.
- Cada FSH inicia com comentário `// Fonte L1: <componente/seção do DAK>` e `// L2: <componente>`.
