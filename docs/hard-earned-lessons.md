# Hard-Earned Lessons

Registro vivo de armadilhas e como evitá-las. **Atualize a cada problema não-óbvio resolvido.**
As lições HEL-001..HEL-008 foram **herdadas do repositório-template `mareIA-ig`** (ATENTO 60+) e
permanecem válidas aqui; novas lições deste repo começam em HEL-101.

---

## HEL-001 — Extração do PDF: encoding e acentuação (herdada)
- **Sintoma:** `Read` do PDF falhou; extração via Python saía com acentos quebrados quando
  impressa direto no terminal Windows.
- **Solução:** extrair com PyMuPDF (`fitz`) e gravar com `open(dst,'w',encoding='utf-8')`.
  Texto-fonte deste repo em `sources/_dak_extract.txt`.

## HEL-002 — `sushi init` é interativo (herdada)
- **Solução:** recriar `sushi-config.yaml` e `ig.ini` manualmente. Validar cedo com `sushi .`.

## HEL-003 — Páginas declaradas x arquivos existentes (herdada)
- **Solução:** toda página listada em `sushi-config.yaml > pages/menu` precisa existir em
  `input/pagecontent/`. Crie stubs antes do primeiro build completo.

## HEL-004 — IG Publisher exige Java; cuidado com a checagem de versão (herdada)
- `java -version` escreve na **stderr**; use `Get-Command java`/`command -v java` para detectar.

## HEL-005 — Suppressed messages file e obs-7 (herdada)
- (1) `input/ignoreWarnings.txt` precisa existir (com cabeçalho `== Suppressed Messages ==`).
- (2) A invariante `obs-7` proíbe valor de nível superior quando há componente com o **mesmo
  código** da Observation. Neste repo, a soma ESAS usa `#esas-total-score` e o componente de risco
  usa `#esas-nivel-risco` (códigos distintos) — mesmo padrão do escore/faixa do IVCF-20.

## HEL-006 — `category = vital-signs` dispara o profile padrão automaticamente (herdada)
- Neste repo os registros ESAS/Zarit usam `category = survey` (não são vital signs), o que evita
  os profiles automáticos de sinais vitais. Se sinais vitais IoT forem adicionados em iteração
  futura, reveja a lição original (painel de PA; `valueQuantity.unit` obrigatório).

## HEL-007 — `hl7fhir/ig-publisher-base` não põe os scripts no PATH (herdada)
- No CI, **instalar o SUSHI** (`npm install -g fsh-sushi`) e adicionar `$(npm prefix -g)/bin` e
  `/opt/java/openjdk/bin` ao `$GITHUB_PATH`; depois `java -jar publisher.jar publisher -ig .`.
  O workflow deste repo já vem com essa correção aplicada.

## HEL-008 — Kramdown exige linha em branco antes de tabelas; PlantUML via images-source; páginas em /en/ (herdada)
- Linha em branco antes de **toda** tabela nos `input/pagecontent/*.md`.
- Fontes `.plantuml` em `input/images-source/`; incluir com `{% include nome.svg %}`.
- Com `fhir2.base.template`, as páginas finais ficam em `output/en/...`.

## HEL-101 — SUSHI exige acesso a packages.fhir.org
- **Sintoma:** em ambiente com rede restrita (allowlist), `sushi .` importa os 22 documentos FSH
  sem erro de sintaxe, mas falha ao baixar `hl7.fhir.r4.core#4.0.1`, `hl7.fhir.uv.sdc#3.0.0` e
  `hl7.fhir.uv.cpg#1.0.0` de `packages.fhir.org`/`packages2.fhir.org`.
- **Causa:** o registry de pacotes FHIR não faz parte do npm; precisa de saída de rede própria.
- **Solução:** liberar `packages.fhir.org` e `packages2.fhir.org` na rede, ou pré-popular o cache
  `~/.fhir/packages` a partir de uma máquina com acesso. O gate completo (`0 Errors`) deve ser
  reexecutado em ambiente com rede antes do primeiro build do IG Publisher.

## HEL-102 — `Observation.subject` não aceita `RelatedPerson` no R4
- **Sintoma:** `sushi .` (via GitHub Actions) acusou: `The type "Reference(...)" does not match
  any of the allowed types: Reference(Patient | Group | Device | Location)` no profile
  `ObservationZaritScore` e no exemplo correspondente; e um erro em cascata de cardinalidade
  (`Observation.subject has minimum cardinality 1 but occurs 0 time(s)`) porque o `subject`
  tinha ficado sem valor válido.
- **Causa:** `Observation.subject` no FHIR R4 base é restrito a `Patient | Group | Device |
  Location`. `RelatedPerson` (o cuidador, cuja sobrecarga a Observation mede) não está na lista.
  Isso só aparece quando o SUSHI consegue baixar os pacotes core do FHIR e rodar a validação de
  tipos — em um ambiente sem acesso a `packages.fhir.org` (ver HEL-101), o erro de download
  mascara esse erro de modelagem, que só apareceu no CI do GitHub Actions.
- **Solução:** inverter os elementos — `subject` (1..1) aponta ao **paciente**
  (`FamiliarAtivaPatientPalliative`, satisfaz a lista de tipos permitidos) e `focus` (1..1) aponta
  ao **cuidador** (`FamiliarAtivaRelatedPersonCaregiver`), usando `Observation.focus` exatamente
  para o caso em que "o foco da observação não é o subject". Ajustar profile, exemplo e a página
  de introdução coerentemente.
- **Lição geral:** ao perfilar `Observation` (ou qualquer recurso) para um ator que não seja
  `Patient`, checar a lista de tipos permitidos no elemento base antes de restringir — e lembrar
  que erros de rede/download no CI podem esconder erros de validação de tipo até a rede estar
  disponível.

<!-- Próximas lições: adicionar abaixo com id incremental. -->
