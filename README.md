# mareIA — FamilIAr_Ativa · WHO SMART Guidelines IG

Implementation Guide (FHIR R4) da **linha de cuidado FamilIAr_Ativa** da Plataforma mareIA —
telemonitoramento de **pacientes em cuidados paliativos domiciliares** e seus **cuidadores
familiares**, com registro diário de sintomas pelo **ESAS** (6 domínios, 0–10), avaliação de
sobrecarga do cuidador pela **Escala Zarit** (22 itens, 0–88), detecção de risco por protocolo
auditável, predição por IA com explicabilidade (XAI) e comunicação segura cuidador↔profissional.

Este repositório é a **adaptação digital** do *DAK L2 FamilIAr_Ativa (UFPel / CUIDATIVA / RNP)* —
já estruturado segundo a camada **L2 (DAK)** do [WHO SMART Guidelines](https://www.who.int/teams/digital-health-and-innovation/smart-guidelines) —
para a camada **L3 (IG FHIR, máquina-legível)**, mantendo a narrativa L2 publicável.
> No SMART Guidelines, **cada linha de cuidado (pathway) é um IG separado**. Este repo cobre
> **somente o FamilIAr_Ativa**. Os demais cenários da mareIA (ATENTO 60+, CardioRemoto, AgroSUS)
> são repositórios próprios.

## Camadas SMART Guidelines

| Camada | O que é                          | Onde está                                                     |
| ------ | -------------------------------- | ------------------------------------------------------------- |
| **L1** | Narrativa (fonte clínica)        | `sources/` (PDF do DAK + Documento de Requisitos + texto extraído) |
| **L2** | DAK — 9 componentes estruturados | `l2/` (fonte) + `input/pagecontent/l2-*.md` (narrativa do IG) |
| **L3** | Artefatos FHIR (FSH)             | `input/fsh/**` → compilado para `fsh-generated/`              |

## Estrutura

```
sources/      → L1/L2 de origem: DAK FamilIAr_Ativa (fonte-verdade clínica)
l2/           → L2: DAK estruturado (CSV/DMN/BPMN/MD/YAML)
input/fsh/    → L3: FHIR Shorthand (profiles, instances, valuesets, libraries)
input/pagecontent/ → narrativa do IG publicado
docs/         → disciplina agentic-dev: PRD, ADRs, cookbooks, Hard-Earned Lessons
.claude/      → camada executável: subagentes (agents/) e skills/
```

## Desenvolvimento agêntico (agentic-based development)

O conteúdo é produzido por um **pipeline de agentes** versionado, com disciplina de docs
padrão de mercado. Pipeline L1 → L2 → L3:

1. `/l1-extract` — extrai fatos normalizados do DAK fonte (L1/L2 de origem).
2. `/dak-build` — gera/atualiza os 9 componentes do DAK (L2) neste repositório.
3. `/fhir-generate` — converte L2 em FSH (L3).
4. `/ig-build` — compila com SUSHI + IG Publisher e valida.

Decisões não-triviais viram **ADRs** (`docs/adr/`); armadilhas viram **Hard-Earned Lessons**
(`docs/hard-earned-lessons.md`). Veja `CLAUDE.md` para as convenções.

## Build

```
# 1. Compilar FSH → recursos FHIR JSON
sushi .

# 2. Gerar o site do IG (requer Java 11+; baixa o IG Publisher na 1ª vez)
./_genonce.sh      # Linux/macOS
_genonce.bat       # Windows
```

Saída em `output/index.html`.

## Status

`draft` v0.1.0 — fase WP1. Itens pendentes de confirmação clínica em `docs/adr/`
(faixas ESAS — ADR-0004; itens da Escala Zarit — ADR-0005).

## Licença

CC-BY-SA-4.0 (conteúdo). Instrumentos ESAS (Bruera et al.) e Zarit Burden Interview (Zarit et al.)
© seus autores — uso conforme fonte; os itens do ZBI-22 **não** são reproduzidos neste repositório
(ver ADR-0005).
