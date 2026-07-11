**Uso.** Registra o **resultado de uma avaliação da Escala Zarit (ZBI-22)**: pontuação total
0–88 (`valueInteger`) e classificação (`interpretation`): Leve (0–20), Moderada (21–40) ou
Severa (41–88). Produzido após a resposta ao `Questionnaire/familiarativa-zarit` (BP-02).

**Escopo.** Uma observação por avaliação periódica (padrão mensal; semanal se Severa na última
avaliação). O `subject` é o **cuidador** (`RelatedPerson`) — o dado mede a sobrecarga do cuidador,
não do paciente; `focus` referencia o paciente relacionado. Fora de escopo: as respostas item a
item, que vivem no `QuestionnaireResponse` (itens do ZBI-22 sob licença — ver **ADR-0005**).

**Identificadores.** `code` fixo `familiarativa-obs-code#zarit-total-score`; `subject` (1..1) →
`FamiliarAtivaRelatedPersonCaregiver`; `effective[x]` e `valueInteger` *must-support*.
`interpretation` ligado (*required*) ao ValueSet `familiarativa-zarit-class-vs`
(`leve` · `moderada` · `severa`) — classificação Severa dispara RA-02.

**Extensões.** **Sem extensões próprias.** A classificação usa o elemento padrão
`Observation.interpretation`, evitando componente/extensão adicionais.

*Fonte L1: DAK FamilIAr_Ativa, §5.2 e §6.2.*
