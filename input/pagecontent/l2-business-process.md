Componente 4 do DAK — *Business processes and workflows*. A matriz de processos BP-01..BP-07 e o
fluxo detalhado do BP-01. O diagrama BPMN 2.0 fonte está em `l2/4-business-process.bpmn`
(importável no bpmn.io).

#### Diagrama de atividades (PlantUML)

{% include process-familiarativa.svg %}
<br clear="all"/>

### Matriz de processos-chave

| ID | Processo | Persona principal | Resultado esperado |
|---|---|---|---|
| BP-01 | Registro de sintomas ESAS | Cuidador / Paciente | Registro clínico + classificação de risco automática |
| BP-02 | Avaliação de sobrecarga Zarit | Cuidador | Pontuação + classificação + notificação se severa |
| BP-03 | Gestão de alertas clínicos | Profissional de Saúde | Alerta resolvido com anotação clínica |
| BP-04 | Comunicação cuidador–profissional | Cuidador + Profissional | Mensagem entregue, respondida e registrada |
| BP-05 | Suporte de IA clínica | Profissional de Saúde | Recomendação com explicabilidade XAI |
| BP-06 | Acesso a módulos educativos | Cuidador / Paciente | Engajamento registrado no perfil do paciente |
| BP-07 | Monitoramento epidemiológico | Gestor / SUS | Indicadores atualizados; relatório exportado |

### Fluxo BP-01 — Registro ESAS (narrativo)

1. Cuidador/Paciente acessa o sistema e seleciona o perfil do paciente (UC-06).
2. Preenche os 6 campos ESAS (dor, dispneia, ansiedade, cansaço, apetite, bem-estar), 0–10.
3. **[DECISÃO]** Todos os campos preenchidos? Não → retorna à etapa 2. Sim → avança.
4. Sistema soma escores e classifica: **Baixo (0–30) / Moderado (31–50) / Alto (51–70)**;
   gera **timestamp imutável**. *(Faixas — REVISAR ADR-0004.)*
5. **[DECISÃO]** Risco Alto? Sim → orientação ao cuidador + dispara UC-19 (alerta) e UC-21
   (notificação). Não → confirmação de envio.
6. Profissional recebe notificação e acessa o dashboard (UC-07/UC-08).

### Tarefas × dados × decisões

| Tarefa | Dados (comp.5) | Decisão (comp.6) |
|---|---|---|
| Registro ESAS (BP-01) | 6 domínios 0–10, soma, timestamp | faixa de risco; RA-01/RA-05 |
| Avaliação Zarit (BP-02) | 22 respostas 0–4, pontuação | classificação; RA-02 |
| Gestão de alertas (BP-03) | tipo, status, criado_em | RA-04 (aberto → requer atenção) |
| Monitoramento de adesão (BP-07) | dias_sem_registro, taxa de adesão | RA-03; alerta se < 80% em 7 dias |

*Fonte: DAK FamilIAr_Ativa, Componente 4 (§4.1–4.2).*
