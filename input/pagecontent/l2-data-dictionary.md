Componente 5 do DAK — *Core data elements*. Fonte estruturada: `l2/5-data-dictionary.csv`.

> **Codificação.** Os domínios do ESAS usam os códigos **LOINC** transcritos do DAK (§5.1) —
> verificação pendente junto à base LOINC (ver ADR-0004). Soma/risco ESAS e pontuação Zarit usam o
> CodeSystem local `familiarativa-obs-code` por não haver código consagrado para os valores
> calculados; nível de risco em `familiarativa-esas-risk` e classificação Zarit em
> `familiarativa-zarit-class`.

### Formulário ESAS

| Campo | Tipo | Min | Max | Obrig. | Mapeamento FHIR/LOINC |
|---|---|---|---|---|---|
| dor | integer | 0 | 10 | Sim | `Observation` (LOINC **38208-5**) |
| dispneia | integer | 0 | 10 | Sim | `Observation` (LOINC **89443-6**) |
| ansiedade | integer | 0 | 10 | Sim | `Observation` (LOINC **89444-4**) |
| cansaco | integer | 0 | 10 | Sim | `Observation` (LOINC **89445-1**) |
| apetite | integer | 0 | 10 | Sim | `Observation` (LOINC **89446-9**) |
| bem_estar | integer | 0 | 10 | Sim | `Observation` (LOINC **89447-7**) |
| nivel_risco | enum (calculado) | — | — | Calculado | componente de `Observation` / `RiskAssessment.prediction.outcome` |
| data_registro | timestamp (UTC) | — | — | Auto | `Observation.effectiveDateTime` (imutável — RF-PC01) |

**Soma e risco** (códigos locais): soma → `familiarativa-obs-code#esas-total-score`; nível de
risco → `familiarativa-obs-code#esas-nivel-risco` com valor em `familiarativa-esas-risk`
(`baixo` 0–30 · `moderado` 31–50 · `alto` 51–70 — **REVISAR ADR-0004**).

### Escala Zarit

| Campo | Tipo | Min | Max | Obrig. | Mapeamento FHIR |
|---|---|---|---|---|---|
| respostas[22] | array int | 0 | 4 × 22 | Sim | `QuestionnaireResponse.item[0..21]` |
| pontuacao | int (calculado) | 0 | 88 | Calculado | `Observation.valueInteger` (`familiarativa-obs-code#zarit-total-score`) |
| classificacao | enum (calculado) | — | — | Calculado | `Observation.interpretation` (`leve`/`moderada`/`severa`) |
| data_avaliacao | timestamp (UTC) | — | — | Auto | `Observation.effectiveDateTime` |

> Os **itens do ZBI-22 não são transcritos** (instrumento sob copyright) — ver **ADR-0005**.

### Alerta clínico

| Campo | Tipo | Descrição / Mapeamento FHIR |
|---|---|---|
| alerta_id | UUID | `Flag.id` |
| paciente_id | UUID (FK) | `Flag.subject` → `Patient` |
| profissional_id | UUID (FK) | `Flag.author` → `Practitioner` |
| tipo | Enum | `ESAS_ALTO` \| `ZARIT_SEVERA` \| `ADESAO_BAIXA` → `Flag.code` (`familiarativa-alert-type`) |
| status | Enum | Aberto \| Resolvido → `Flag.status` (active/inactive) |
| criado_em | Timestamp | `Flag.period.start` |

*Fonte: DAK FamilIAr_Ativa, Componente 5 (§5.1–5.3).*
