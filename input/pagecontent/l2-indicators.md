Componente 7 do DAK (Componente 8 no documento fonte) — *Program indicators*.
Fonte: `l2/7-indicators.csv`. Cada indicador → `Measure` (L3).

### Indicadores de processo

| Id | Nome | Numerador | Denominador |
|---|---|---|---|
| IND-01 | Taxa de adesão ao monitoramento (%) — **meta 80%** | Pacientes com ≥1 registro ESAS no período | Total de pacientes ativos |
| IND-03 | Taxa de resolução de alertas | Alertas com status = Resolvido | Total de alertas criados no período |
| IND-06 | Taxa de engajamento educativo | Pacientes com ≥1 acesso a módulo educativo no mês | Total de pacientes ativos |

### Indicadores de resultado

| Id | Nome | Numerador | Denominador |
|---|---|---|---|
| IND-02 | Proporção de registros com risco Alto | Registros com nivel_risco = Alto | Total de registros ESAS no período |
| IND-04 | Prevalência de sobrecarga severa do cuidador | Avaliações Zarit Severa | Total de avaliações Zarit no período |
| IND-05 | Tempo médio de resolução de alerta (horas) | Soma (resolvido_em − criado_em) | Total de alertas resolvidos |
| IND-07 | Pontuação média ESAS por domínio | Soma dos escores por sintoma | Total de registros no período |

Desagregações previstas: por profissional (IND-02, 03, 05), por unidade (IND-04, 06) e por
diagnóstico (IND-07). Fontes: `REGISTRO_SINTOMAS`, `ESCALA_ZARIT`, `ALERTA`, `ACESSO_MODULO`.

*Fonte: DAK FamilIAr_Ativa, Componente 8 (IND-01 a IND-07).*
