Componente 9 do DAK — *Test scenarios*. Casos para validar a lógica de decisão (comp. 6) no L3.
O DAK fonte não traz cenários de teste explícitos; os casos abaixo são derivados diretamente das
tabelas DMN (§6.1–6.3) e dos Cenários de Uso (Componente 3).

### Casos de soma/risco (ESAS)

| Caso | Registro (resumo) | Soma esperada | Risco esperado |
|---|---|---|---|
| TC-01 | Todos os domínios 0–5 (ex.: 5+5+5+5+5+5) | 30 | Baixo (limite superior) |
| TC-02 | Soma intermediária (ex.: 6+6+6+6+6+1) | 31 | Moderado (limite inferior) |
| TC-03 | Cenário 1 do DAK: dor 8, dispneia 7 + demais domínios | 52 | **Alto** → orientação + alerta + notificação |
| TC-04 | Todos os domínios em 10 | 60 | Alto — **REVISAR ADR-0004** (tabela vai a 70) |

### Casos de classificação (Zarit)

| Caso | Pontuação | Classificação esperada |
|---|---|---|
| TC-05 | 20 / 21 | Leve / Moderada (borda) |
| TC-06 | 64 (Cenário 2 do DAK) | **Severa** → notificação ao profissional (RA-02) |
| TC-07 | 40 / 41 | Moderada / Severa (borda) |

### Casos de alerta e adesão

| Caso | Gatilho | Resultado esperado |
|---|---|---|
| TC-08 | soma_esas = 51 (> 50) | Alerta ESAS_ALTO + mensagem bidirecional (RA-01/RA-05) |
| TC-09 | dias_sem_registro > janela esperada | Sinalização ADESAO_BAIXA no painel do Gestor (RA-03) |
| TC-10 | Alerta aberto sem resolução | Visível como "requer atenção" no painel (RA-04) |
| TC-11 | Adesão da unidade 74% (< 80% em 7 dias — Cenário 4) | Alerta imediato ao Gestor; exportação PDF |

### Casos de agendamento

| Caso | Condição | Próxima coleta esperada |
|---|---|---|
| TC-12 | Risco Alto recente | ESAS 2×/dia (ajuste pelo profissional) |
| TC-13 | Zarit Severa na última avaliação | Zarit semanal (padrão mensal) |

*Casos derivados do DAK FamilIAr_Ativa, Componentes 3, 6 e 7.*
