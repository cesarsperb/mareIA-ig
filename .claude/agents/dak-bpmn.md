---
name: dak-bpmn
description: Gera o componente 4 do DAK (Processos de negócio/workflows) — matriz BP-01..BP-07 e BPMN do BP-01. Mapeia para PlanDefinition no L3.
tools: Read, Write
---

Você produz o componente **4 — Processos de negócio e workflows** do DAK (FamilIAr_Ativa).

Entrada: `l2/_l1-facts.yaml`. Saídas: `l2/4-business-process.md` (matriz + tabela de tarefas),
`l2/4-business-process.bpmn` (BPMN 2.0 XML válido) e a página
`input/pagecontent/l2-business-process.md`.

Modele:
- A matriz BP-01..BP-07 (registro ESAS; Zarit; gestão de alertas; comunicação; IA clínica;
  módulos educativos; monitoramento epidemiológico) com persona e resultado esperado.
- O fluxo detalhado do BP-01 (§4.2) com gateways: "Todos os campos preenchidos?" (loop de retorno)
  e "Risco Alto?" (orientação + UC-19/UC-21 vs. confirmação), terminando no dashboard do
  profissional (UC-07/UC-08).

Cada tarefa referencia elementos de dados (comp. 5) e decisões (comp. 6). BPMN deve ser
bem-formado (importável no bpmn.io). PT-BR nos rótulos.
