Componente 3 do DAK — *User scenarios*. Narrativas do DAK fonte, cobrindo os processos BP-01..BP-07.

#### Diagrama de casos de uso (PlantUML)

{% include usecases-familiarativa.svg %}
<br clear="all"/>

#### Diagrama de sequência — cenário ponta a ponta (PlantUML)

{% include scenario-sequence-familiarativa.svg %}
<br clear="all"/>

### Cenário 1 — Registro diário de sintomas (ESAS)

**Como** cuidador (João, cuidador de sua mãe Maria, paciente oncológica em cuidados paliativos
domiciliares), **abro** o app às 09h, **seleciono** o perfil de Maria e **preencho** o ESAS —
hoje dor nível 8 e dispneia nível 7. O sistema soma os escores, classifica o risco como **Alto**
e **orienta** o contato com o profissional. Simultaneamente, a Dra. Ana recebe o **alerta** no
dashboard, consulta o histórico, responde pelo **chat seguro** com orientações de manejo e agenda
visita para o dia seguinte.

### Cenário 2 — Avaliação de sobrecarga (Zarit)

**Como** cuidador, **sou notificado** de que é hora de responder a **Escala Zarit**. Respondo os
22 itens em ~5 minutos; pontuação **64 → Sobrecarga Severa**. O sistema exibe o resultado e
**notifica** a Dra. Ana, que prioriza uma conversa na próxima semana para avaliar o suporte ao cuidador.

### Cenário 3 — Consulta de IA clínica

**Como** profissional de saúde, **noto** no dashboard três pacientes com piora progressiva de
dispneia em 14 dias. **Aciono** o módulo de IA clínica (contexto ESAS injetado automaticamente) e
**pergunto** a probabilidade de deterioração nas próximas 72h. O sistema retorna a análise do
modelo preditivo com **explicação XAI** dos fatores de risco mais relevantes.

### Cenário 4 — Gestor monitora adesão

**Como** coordenadora da unidade, **verifico** no painel de gestão que a adesão caiu para **74%**
(meta 80%). **Filtro** por profissional, identifico 3 pacientes sem registro há 7 dias e
**exporto** o relatório em PDF para a reunião de equipe.

*Fonte: DAK FamilIAr_Ativa, Componente 3 (Cenários 1–4).*
