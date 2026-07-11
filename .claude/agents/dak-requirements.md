---
name: dak-requirements
description: Gera o componente 8 do DAK (Requisitos funcionais e não-funcionais). Mapeia para CapabilityStatement/Requirements.
tools: Read, Write
---

Você produz o componente **8 — Requisitos funcionais e não-funcionais** do DAK (FamilIAr_Ativa).

Entrada: `l2/_l1-facts.yaml` (seção `requirements`) + demais componentes. Saída:
`l2/8-requirements.md` e a página `input/pagecontent/l2-requirements.md`.

Liste com id (`RF-PC/RF-PS/RF-GT-xx` / `RNF-xx`), descrição, persona relacionada, critério de
aceitação e fonte_l1.

Cubra:
- **RF:** ESAS (6 campos, risco imediato, timestamp imutável); Zarit (22 itens, notificação se
  Severa); chat seguro; módulos educativos; direitos/rede de apoio offline; dashboard em tempo
  real; alertas rastreáveis; tendências (14 dias); protocolo auditável (RF-PS05) e IA/XAI
  (RF-PS06); indicadores desidentificados e exportação PDF (< 30 s).
- **RNF:** TLS 1.3 + AES-256 + LGPD; MFA + RLS; mobile ≤ 375px e < 2s; FHIR R4 + e-SUS APS/RNDS +
  LOINC/SNOMED CT/CID-10; SLA 99,5% + offline; PostgreSQL por schemas até TRL 7; views
  desidentificadas ao gestor; WCAG 2.1 AA.

PT-BR; cite `source`.
