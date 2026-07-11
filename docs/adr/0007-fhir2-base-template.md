# ADR-0007 — Uso do fhir2.base.template

- **Status:** Aceito (2026-07-10) — herdado do template mareIA-ig (ADR-0007)

## Contexto
No template mareIA-ig, o IG Publisher emitiu o aviso de que `fhir.base.template` "is no longer
considered secure to use" (notificação de segurança 2026-03), recomendando o template
multilíngue **`fhir2.base.template`** e avisando que IGs com o template antigo passarão a ser
recusados.

## Decisão
Este repositório já **nasce** com o template novo em `ig.ini`:
```
template = fhir2.base.template#current
```

## Consequências
- (+) Sem aviso de segurança; template suportado e multilíngue (útil ao PT-BR).
- (~) Com esse template, as páginas finais ficam em `output/en/...` (ver Hard-Earned Lessons,
  HEL-008 herdada).
- A migração futura para o template **SMART da WHO** continua possível sem reescrever os FSH.
