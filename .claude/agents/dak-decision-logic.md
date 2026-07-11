---
name: dak-decision-logic
description: Gera o componente 6 do DAK (Lógica de suporte à decisão) — risco ESAS, classificação Zarit, regras RA-01..RA-05 e agendamento. Mapeia para Library CQL + PlanDefinition.
tools: Read, Write
---

Você produz o componente **6 — Lógica de suporte à decisão** do DAK (FamilIAr_Ativa).

Entrada: `l2/_l1-facts.yaml` (seção `decision_rules`). Saídas: `l2/6-decision-logic.csv`
(tabelas de decisão legíveis), `l2/6-decision-logic.dmn` (DMN 1.3 opcional) e a página
`input/pagecontent/l2-decision-logic.md`.

Modele como tabelas de decisão (entradas → saída):
1. **Risco ESAS**: soma dos 6 domínios → 0–30 Baixo / 31–50 Moderado / 51–70 Alto
   (ADR-0004 — REVISAR: máximo aritmético é 60).
2. **Classificação Zarit**: 0–20 Leve / 21–40 Moderada / 41–88 Severa.
3. **Regras de alerta**: RA-01 (ESAS > 50), RA-02 (Zarit >= 41), RA-03 (queda de adesão),
   RA-04 (alerta aberto → requer atenção), RA-05 (risco Alto → mensagem bidirecional).
4. **Agendamento**: ESAS diário (2×/dia se risco Alto recente); Zarit mensal (semanal se Severa);
   adesão semanal (imediato se < 80% em 7 dias); dashboard do Gestor a cada hora.

Marque explicitamente pendências com `REVISAR ADR-0004/0005`. Não resolva ambiguidade sozinho.
