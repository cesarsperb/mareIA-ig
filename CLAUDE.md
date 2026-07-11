# CLAUDE.md — Convenções do repositório mareIA / FamilIAr_Ativa

Este repositório é a **adaptação digital** do *DAK L2 FamilIAr_Ativa (UFPel / CUIDATIVA / RNP)*
para a metodologia **WHO SMART Guidelines**, cobrindo **um único pathway: FamilIAr_Ativa**
(cuidados paliativos domiciliares, ESAS + Zarit). Leia este arquivo antes de editar qualquer coisa.

## 1. Primer SMART Guidelines (mínimo necessário)

A OMS organiza diretrizes em 5 camadas de conhecimento (L1–L5). Aqui cobrimos L1→L3:

- **L1 — Narrativa:** a fonte clínica. Neste pathway a fonte-verdade em `sources/` já chega como
  **DAK L2** (documento estruturado nos 9 componentes) + Documento de Requisitos. **Nunca** inventar
  conteúdo clínico que não esteja na fonte; lacunas viram pergunta ao usuário/equipe clínica.
- **L2 — DAK (Digital Adaptation Kit):** 9 componentes estruturados, humano-legíveis, em `l2/`.
  São o "contrato" entre clínica e engenharia.
- **L3 — IG FHIR:** artefatos máquina-legíveis (FHIR R4) em `input/fsh/`, compilados por SUSHI.

### Os 9 componentes do DAK (ordem canônica)
1. Intervenções e recomendações de saúde
2. Personas genéricas
3. Cenários de uso
4. Processos de negócio e workflows (BPMN)
5. Elementos de dados centrais (dicionário de dados)
6. Lógica de suporte à decisão (DMN/CQL)
7. Indicadores de programa
8. Requisitos funcionais e não-funcionais
9. Cenários de teste

### Mapeamento L2 → L3 (FHIR)
| Componente L2 | Artefato L3 |
|---|---|
| Personas | `ActorDefinition` (R5; nesta fase R4 ficam no L2 — ADR-0006) |
| Processos/workflows | BPMN + `PlanDefinition` |
| Elementos de dados | `Questionnaire` (ESAS, Zarit), `StructureDefinition` (profiles), `CodeSystem`/`ValueSet` |
| Lógica de decisão | `Library` (CQL) + `PlanDefinition` |
| Alertas clínicos | `Flag` (tipo/status) |
| Indicadores | `Measure` |
| Requisitos | `CapabilityStatement` + `Requirements` |

## 2. Pipeline agêntico (L1 → L2 → L3)

Produção orientada por skills + subagentes versionados (`.claude/`):

| Etapa | Skill | Subagente(s) | Entrada → Saída |
|---|---|---|---|
| Extrair L1 | `/l1-extract` | `l1-extractor` | `sources/` → `l2/_l1-facts.yaml` |
| Construir DAK | `/dak-build` | `dak-personas`, `dak-user-scenarios`, `dak-bpmn`, `dak-data-dictionary`, `dak-decision-logic`, `dak-indicators`, `dak-requirements` | `_l1-facts.yaml` → `l2/*` + `input/pagecontent/l2-*.md` |
| Gerar FHIR | `/fhir-generate` | `fhir-author` | `l2/*` → `input/fsh/**` |
| Build & validar | `/ig-build` | `ig-validator` | `input/fsh/**` → `fsh-generated/`, `output/` |

**Princípio de rastreabilidade:** todo artefato L2/L3 deve citar a origem na fonte
(componente/seção do DAK, ex.: `DAK §6.1`) num campo `source:` ou comentário.

## 3. Disciplina de documentação (padrão de mercado)

- `docs/prd/` — **PRD**: o que o IG entrega e por quê; critérios de aceite.
- `docs/adr/` — **ADR** (Architecture Decision Records): uma decisão por arquivo, imutável após
  aceito; mudança = novo ADR que supersede. Formato: Contexto / Decisão / Consequências / Status.
- `docs/cookbooks/` — receitas passo-a-passo reproduzíveis.
- `docs/hard-earned-lessons.md` — armadilhas e como evitá-las; **atualize a cada build quebrado**.

**Regra de ouro:** decisão não-trivial → ADR. Bug não-óbvio resolvido → Hard-Earned Lesson.

## 4. Convenções FHIR/FSH

- `fhirVersion: 4.0.1` (ver ADR-0008 — R4 apesar de o cabeçalho do DAK citar o Starter Kit R5).
  Ids de recurso em `kebab-case` com prefixo do domínio (ex.:
  `Questionnaire/familiarativa-esas`, `CodeSystem/familiarativa-esas-risk`).
- **Idioma:** `title`/`description`/`display`/textos em **PT-BR**; nomes técnicos (ids, `name:`)
  em inglês/ASCII (convenção FHIR). Ver `docs/adr/0003-idioma.md`.
- Vocabulários: **LOINC** para os domínios do ESAS (códigos do DAK §5.1 — verificar, ADR-0004),
  **SNOMED CT** para desfechos de risco quando aplicável, **CID-10** (BR) para diagnósticos.
  CodeSystems locais só quando não houver código padrão (faixas de risco ESAS, classificação
  Zarit, tipos de alerta, escores).
- Um arquivo FSH por artefato lógico; agrupar por tipo em `input/fsh/<tipo>/`.
- A Escala Zarit (ZBI-22) é protegida por direitos autorais: o `Questionnaire` usa **placeholders**
  por item; o texto oficial só entra mediante licença (ADR-0005).

## 5. Build

```bash
sushi .                 # FSH → fsh-generated/resources/*.json (deve dar 0 erros)
./_updatePublisher.sh   # baixa o IG Publisher (1ª vez; requer Java 11+)
./_genonce.sh           # gera o site em output/
```

## 6. Não decidir sozinho

Ambiguidades clínicas (faixas de escore, codificação LOINC, itens de instrumento) **não** são
resolvidas por suposição: registre como item aberto em ADR (status `proposto`) e pergunte.
Itens abertos atuais em `docs/adr/0004-esas-escore-codificacao.md` e
`docs/adr/0005-zarit-itens-licenca.md`.
