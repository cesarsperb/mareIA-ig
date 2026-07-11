# Cookbook — L1 (fonte) → L2 (DAK)

Receita para converter a fonte clínica em componentes estruturados do DAK. Particularidade deste
pathway: a fonte em `sources/` **já é um DAK L2** (documento estruturado nos 9 componentes) —
logo, o trabalho é de **normalização e estruturação** (YAML/CSV/BPMN), não de derivação clínica.

## Pré-requisitos
- `sources/_dak_extract.txt` (texto extraído do PDF).
- Skill `/l1-extract` e subagentes `dak-*` disponíveis em `.claude/`.

## Passos
1. **Extrair fatos** (`/l1-extract`): normalize o DAK em `l2/_l1-facts.yaml` com seções:
   `recommendations`, `dhi_who`, `actors`, `data_elements`, `decision_rules`,
   `business_processes`, `indicators`, `requirements`, cada item com `source` (componente/seção).
2. **Personas** (`dak-personas`): PC (cuidador), PC-A (paciente autocuidado), PS (profissional),
   GT (gestor) — papel, acesso, restrições, id ASCII para futuro `ActorDefinition`.
3. **Cenários de uso**: transcrever/normalizar os Cenários 1–4 do DAK (Componente 3).
4. **Processos/BPMN** (`dak-bpmn` → `l2/4-business-process.bpmn`): matriz BP-01..BP-07 + fluxo
   detalhado do BP-01 (§4.2) com os gateways "campos preenchidos?" e "risco Alto?".
5. **Dicionário de dados** (`dak-data-dictionary` → `l2/5-data-dictionary.csv`): ESAS (6 domínios
   + soma + risco + timestamp), Zarit (respostas[22] + pontuação + classificação) e Alerta
   (tipo/status/criado_em), com códigos LOINC/locais e mapeamento FHIR.
6. **Lógica de decisão** (`dak-decision-logic` → `l2/6-decision-logic.csv`): DT-1 risco ESAS,
   DT-2 classificação Zarit, DT-3 regras RA-01..RA-05, DT-4 agendamento. Pendências → ADR-0004/0005.
7. **Indicadores** (`dak-indicators` → `l2/7-indicators.csv`): IND-01..IND-07 com numerador,
   denominador, tipo e desagregação.
8. **Requisitos** (`dak-requirements`): RF-PC/RF-PS/RF-GT e RNF-01..08 com critérios de aceite.
9. **Cenários de teste**: derivar casos-limite das tabelas DMN (bordas 30/31, 50/51, 20/21,
   40/41) e dos Cenários de Uso (soma 52 → Alto; Zarit 64 → Severa).

## Saída
- `l2/*` (fonte estruturada) + `input/pagecontent/l2-*.md` (narrativa publicável do IG).

## Regras
- **Fidelidade > completude:** não acrescente conteúdo clínico ausente da fonte
  (ex.: itens do ZBI-22 — ADR-0005).
- **Rastreabilidade:** todo item carrega `source` (componente/seção do DAK).
- **Ambiguidade → ADR** (status proposto) + pergunta, nunca suposição silenciosa
  (ex.: faixa ESAS até 70 — ADR-0004).
