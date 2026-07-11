# ADR-0004 — Escore, faixas e codificação LOINC do ESAS

- **Status:** PROPOSTO — aguarda confirmação da equipe clínica (UFPel / CUIDATIVA)
- **Bloqueia:** componente L2 §6 (decisão), Questionnaire/Observations ESAS no L3

## Contexto
O DAK FamilIAr_Ativa define o ESAS com **6 domínios** (dor, dispneia, ansiedade, cansaço,
apetite, bem-estar), cada um 0–10 (§5.1), e classifica o risco pela soma (§4.2 etapa 4 e §6.1):
- **0–30 Baixo**, **31–50 Moderado**, **51–70 Alto**.

Inconsistências e pendências observadas:
1. Com 6 domínios × 10 pontos, a soma máxima aritmética é **60**, mas a faixa "Alto" vai até
   **70** — sugere que o instrumento completo (ESAS original tem 9–10 sintomas) ou outra
   ponderação possa estar prevista.
2. Os códigos **LOINC por domínio** transcritos do DAK (38208-5 para dor; 89443-6, 89444-4,
   89445-1, 89446-9, 89447-7 para os demais) precisam de **verificação na base LOINC** (o ESAS
   possui painel LOINC próprio; conferir correspondência item a item).
3. O DAK mapeia `nivel_risco` para `RiskAssessment.prediction.outcome` (SNOMED CT); o código
   SNOMED CT específico por faixa não é informado.

## Questões abertas (não decidir sozinho)
1. Confirmar o **número de domínios** (6 conforme DAK ou ESAS completo) e a **soma máxima**.
2. Confirmar as **3 faixas** (0–30 / 31–50 / 51–70) sobre a soma efetiva.
3. Validar os **códigos LOINC** por domínio e definir codificação SNOMED CT das faixas (ou manter
   CodeSystem local `familiarativa-esas-risk`, proposto).

## Decisão provisória (para destravar L2/L3, marcada como tentativa)
Codificar **como escrito no DAK**: 6 domínios, faixas 0–30 / 31–50 / 51–70, LOINC transcritos,
faixas em CodeSystem local, com `// REVISAR ADR-0004` nos artefatos. Reabrir como ADR-0004a se a
equipe ajustar.
