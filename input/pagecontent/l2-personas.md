Componente 2 do DAK — *Generic personas*. Os ids reservados abaixo mapeiam para `ActorDefinition`
quando o IG migrar para FHIR R5 (ver ADR-0006; nesta fase R4 as personas ficam no L2).

O módulo opera em **dois cenários**: **A** — paciente em autocuidado opera o sistema; **B** —
cuidador opera o sistema e o paciente é a fonte de dados clínicos.

#### Diagrama de atores (PlantUML)

{% include actors-familiarativa.svg %}
<br clear="all"/>

| Id (ActorDefinition) | Persona | Acesso | Função no fluxo |
|---|---|---|---|
| `caregiver` | **Cuidador Familiar (PC)** | App mobile/web (conectividade variável; ESAS offline) | Usuário primário: registra ESAS, responde Zarit, troca mensagens com o profissional e acessa módulos educativos. |
| `patient-selfcare` | **Paciente em Autocuidado (PC-A)** | App mobile/web (interface acessível) | Opera o sistema com autonomia funcional (Cenário A); mesmas funções do cuidador. |
| `health-professional` | **Profissional de Saúde (PS)** | Web (dashboard clínico) / app profissional | Monitora pacientes vinculados; recebe/resolve alertas, responde mensagens, usa IA clínica (XAI), vê tendências (14 dias). |
| `sus-manager` | **Gestor / Equipe SUS (GT)** | Web (painel de indicadores) | Indicadores epidemiológicos agregados; adesão da equipe (meta 80%); exportação PDF — **dados desidentificados**. |

### Notas

- O cuidador familiar é adulto **sem formação técnica em saúde**, com baixa a moderada literacia
  digital e possível sobrecarga emocional — a interface deve ser simples, mobile-first, com
  feedback imediato de risco.
- Fadiga, dor ou limitação cognitiva do paciente em autocuidado exigem **acessibilidade**
  (WCAG 2.1 AA — RNF-08).
- O gestor **não** acessa dados clínicos individuais (RNF-07 — views desidentificadas).

*Fonte: DAK FamilIAr_Ativa, Componente 2 (Personas 1–4).*
