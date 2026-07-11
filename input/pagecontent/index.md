### mareIA — FamilIAr_Ativa

Adaptação digital (WHO SMART Guidelines **L2/L3**) do *DAK L2 FamilIAr_Ativa (UFPel / CUIDATIVA / RNP)*
para a **linha de cuidado de telemonitoramento em cuidados paliativos domiciliares**, com registro
diário de sintomas pelo **ESAS** (6 domínios, 0–10), avaliação de sobrecarga do cuidador pela
**Escala Zarit** (22 itens, 0–88), detecção de risco por protocolo auditável e predição por IA com
explicabilidade (**XAI**).

> Este IG cobre **apenas o pathway FamilIAr_Ativa**. No SMART Guidelines, cada linha de cuidado é um
> IG independente (ver ADR-0001); este repositório foi derivado do template mareIA-ig (ATENTO 60+).

#### Fluxo de cuidado

`Vínculo clínico → Registro diário (ESAS) → Classificação de risco → Alertas e resposta clínica → Avaliação periódica do cuidador (Zarit) → Gestão (indicadores desidentificados)`

1. **Registro de sintomas (BP-01)** — cuidador/paciente preenche o ESAS; soma e risco calculados; timestamp imutável.
2. **Avaliação do cuidador (BP-02)** — Escala Zarit periódica; notificação se Sobrecarga Severa.
3. **Resposta clínica (BP-03/BP-04/BP-05)** — alertas, chat seguro e IA clínica com XAI.
4. **Educação e gestão (BP-06/BP-07)** — módulos educativos; painel do Gestor/SUS com dados desidentificados.

#### Componentes do DAK (L2)

| # | Componente | Página |
|---|---|---|
| 1 | Intervenções e recomendações | [l2-interventions](l2-interventions.html) |
| 2 | Personas genéricas | [l2-personas](l2-personas.html) |
| 3 | Cenários de uso | [l2-user-scenarios](l2-user-scenarios.html) |
| 4 | Processos de negócio e workflows | [l2-business-process](l2-business-process.html) |
| 5 | Elementos de dados (dicionário) | [l2-data-dictionary](l2-data-dictionary.html) |
| 6 | Lógica de suporte à decisão | [l2-decision-logic](l2-decision-logic.html) |
| 7 | Indicadores de programa | [l2-indicators](l2-indicators.html) |
| 8 | Requisitos | [l2-requirements](l2-requirements.html) |
| 9 | Cenários de teste | [l2-test-scenarios](l2-test-scenarios.html) |

#### Itens pendentes de confirmação clínica

- **Faixas/soma do ESAS e códigos LOINC** — a tabela de risco vai até 70, mas 6 domínios × 10 = 60 (ADR-0004).
- **Itens da Escala Zarit (ZBI-22)** — texto oficial sob licença; Questionnaire com placeholders (ADR-0005).

*Fonte (L1): DAK L2 FamilIAr_Ativa v0.1, Junho/2026 — UFPel / CUIDATIVA / RNP · Programa RNP Saúde Digital 2025.*
