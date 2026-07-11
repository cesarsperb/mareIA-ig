---
name: dak-data-dictionary
description: Gera o componente 5 do DAK (Elementos de dados / dicionário) — ESAS (6 domínios), Zarit (22 itens) e Alerta, com codificação LOINC/local e mapeamento FHIR.
tools: Read, Write
---

Você produz o componente **5 — Elementos de dados centrais** do DAK (FamilIAr_Ativa).

Entrada: `l2/_l1-facts.yaml` (seção `data_elements`). Saída: `l2/5-data-dictionary.csv` e a página
`input/pagecontent/l2-data-dictionary.md`.

Colunas do CSV: `id, rotulo_ptbr, componente_dak, tipo, valores_ou_unidade, sistema_codigo,
codigo, obrigatorio, fonte_l1`.

Inclua:
- Os **6 domínios do ESAS** (dor, dispneia, ansiedade, cansaço, apetite, bem-estar; 0–10) com os
  códigos LOINC do DAK §5.1 (marcar REVISAR ADR-0004), soma, nível de risco e timestamp imutável.
- A **Escala Zarit**: respostas[22] (0–4), pontuação (0–88), classificação e data — sem
  transcrever os itens do ZBI-22 (ADR-0005).
- O **Alerta clínico**: id, paciente, profissional, tipo (ESAS_ALTO|ZARIT_SEVERA|ADESAO_BAIXA),
  status (Aberto|Resolvido → Flag.status) e criado_em (Flag.period.start).

Para valores calculados use CodeSystem local (`familiarativa-obs-code`, `familiarativa-esas-risk`,
`familiarativa-zarit-class`, `familiarativa-alert-type`). PT-BR nos rótulos.
