# ADR-0001 — Um IG por pathway (repo derivado do template mareIA-ig)

- **Status:** Aceito (2026-07-10)
- **Decisores:** Equipe mareIA + Claude

## Contexto
A Plataforma mareIA cobre 4 cenários (ATENTO 60+, CardioRemoto, FamilIAr_Ativa, AgroSUS). No WHO
SMART Guidelines, a unidade de publicação é a **linha de cuidado (pathway)**, normalmente um IG
por diretriz/condição. O repositório `mareIA-ig` (ATENTO 60+) estabeleceu essa decisão (seu
ADR-0001) e se ofereceu como template para os demais cenários.

## Decisão
Este repositório (`familiarativa-ig`) cobre **exclusivamente o FamilIAr_Ativa** e foi **derivado
do template `mareIA-ig`**: mesma estrutura (L1→L2→L3), mesma disciplina de docs (PRD/ADR/
cookbooks/HEL), mesmo pipeline agêntico (`.claude/`), com conteúdo clínico substituído pelo DAK
FamilIAr_Ativa (ESAS + Zarit, cuidados paliativos domiciliares).

## Consequências
- (+) Aderência ao padrão WHO; publicação e versionamento independentes por pathway.
- (+) Reuso comprovado do template (ADRs herdados; Hard-Earned Lessons preservadas).
- (−) Conteúdo comum (macrofases, LGPD) duplicado entre repos; mitigação futura: IG-base mareIA.
