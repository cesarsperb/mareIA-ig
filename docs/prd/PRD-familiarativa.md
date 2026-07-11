# PRD — IG FamilIAr_Ativa (mareIA / WHO SMART Guidelines)

- **Produto:** Implementation Guide FHIR R4 da linha de cuidado FamilIAr_Ativa.
- **Versão:** 0.1.0 (WP1) · **Status:** draft · **Data:** 2026-07
- **Fonte L1:** `sources/FamilIAr_Ativa_DAK_L2_SMART.pdf` (DAK L2 UFPel / CUIDATIVA / RNP)

## 1. Problema
O SUS precisa de suporte contínuo a **pacientes em cuidados paliativos domiciliares** e seus
**cuidadores familiares**, frequentemente sobrecarregados e sem acesso ágil à equipe de saúde.
O FamilIAr_Ativa (plataforma mare.IA) propõe telemonitoramento com ESAS/Zarit, alertas e IA com
XAI. Para ser interoperável (e-SUS APS/RNDS) e auditável, a diretriz precisa ser convertida da
fonte estruturada (DAK L2) em artefatos máquina-legíveis (L3) segundo o WHO SMART Guidelines.

## 2. Objetivo
Entregar um IG que represente fielmente o DAK FamilIAr_Ativa: registro diário de sintomas
(**ESAS**) → classificação de risco → alertas e resposta clínica → avaliação periódica do
cuidador (**Zarit**) → gestão por indicadores desidentificados, em FHIR R4.

## 3. Escopo
**Inclui:** pathway FamilIAr_Ativa completo — ESAS (6 domínios), Zarit (ZBI-22), lógica de
risco/alertas (RA-01..RA-05), agendamento, indicadores IND-01..IND-07, requisitos e
interoperabilidade (Flag, Communication, ServiceRequest, RiskAssessment).
**Exclui:** demais pathways (repos próprios), L4/L5, integração executável real com e-SUS/RNDS,
implementação do modelo preditivo de IA (o IG modela a **interface** RiskAssessment/XAI, não o
modelo), texto oficial dos itens do ZBI-22 (pendente de licença — ADR-0005).

## 4. Personas (resumo — ver L2 §2)
Cuidador Familiar (PC) · Paciente em Autocuidado (PC-A) · Profissional de Saúde (PS) ·
Gestor/Equipe SUS (GT).

## 5. Requisitos-chave (ver L2 §8)
- **RF:** ESAS diário com risco imediato e timestamp imutável; Zarit com notificação se Severa;
  chat seguro; alertas rastreáveis; tendências (14 dias); protocolo auditável + IA/XAI;
  indicadores desidentificados com exportação PDF.
- **RNF:** FHIR R4 (e-SUS APS/RNDS); LGPD (TLS 1.3, AES-256, RLS, MFA); modo offline para ESAS;
  SLA 99,5%; WCAG 2.1 AA; LOINC/SNOMED CT/CID-10.

## 6. Critérios de aceite
1. `sushi .` compila com **0 erros**.
2. IG Publisher gera site com 0 erros de QA.
3. `Questionnaire` ESAS com 6 itens (0–10) renderiza corretamente; Zarit com 22 itens
   (placeholders — ADR-0005).
4. Lógica de decisão classifica: soma 0–30 → Baixo; 31–50 → Moderado; 51–70 → Alto
   (faixas conforme L1; pendência de confirmação em ADR-0004) e Zarit 0–20/21–40/41–88.
5. **1 `Measure` por indicador** (IND-01 a IND-07).
6. Rastreabilidade L3→L1 (componente/seção do DAK) presente em cada artefato.

## 7. Riscos / itens abertos
- Faixa de risco ESAS até 70 com máximo aritmético 60; códigos LOINC dos domínios a verificar (ADR-0004).
- Itens do ZBI-22 sob copyright — texto oficial pendente de licença (ADR-0005).
- FHIR R4 (RNF-04) vs. menção ao Starter Kit R5 no cabeçalho do DAK (ADR-0008).
- Disponibilidade de Java para o IG Publisher no ambiente de build.
