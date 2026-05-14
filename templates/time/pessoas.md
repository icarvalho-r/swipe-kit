# Time Swipe Offers — Mapa de Pessoas

Lido pelo `/setup` pra reconhecer a pessoa, pré-carregar função e criar estrutura de pastas personalizada.

---

## Pessoas

### Trevizan
- **Apelidos / variações:** Trevizan, Henrique Trevizan, Henrique S, Sócio
- **Função:** Sócio — dono do produto
- **Contexto:** Decisões de roadmap, visão de produto, negociações estratégicas
- **Pergunta de contexto:** "Qual é a prioridade que tá consumindo mais energia essa semana?"
- **Estrutura de pastas:**
  ```
  estrategia/
  relatorios/
  decks/
  ```

---

### Caique
- **Apelidos / variações:** Caique, CEO
- **Função:** CEO
- **Contexto:** Liderança geral, métricas da empresa, comunicação externa
- **Pergunta de contexto:** "Qual é a prioridade que tá consumindo mais energia essa semana?"
- **Estrutura de pastas:**
  ```
  estrategia/
  relatorios/
  decks/
  ```

---

### Thais
- **Apelidos / variações:** Thais, Thaís, CRM
- **Função:** CRM
- **Contexto:** Fluxos de email, dunning, automações de retenção, Active Campaign
- **Pergunta de contexto:** "Tá focada no dunning ainda ou entrou coisa nova essa semana?"
- **Estrutura de pastas:**
  ```
  crm/
    emails/
    fluxos/
    relatorios/
  ```

---

### Guibson
- **Apelidos / variações:** Guibson, Guib, Dados
- **Função:** Dados / Activation
- **Contexto:** Dashboards, instrumentação, activation points, análise quantitativa
- **Pergunta de contexto:** "Instrumentação ainda ou já entrou análise de cohort essa semana?"
- **Estrutura de pastas:**
  ```
  dashboards/
  analise/
  instrumentacao/
  relatorios/
  ```

---

### Henrique T
- **Apelidos / variações:** Henrique T, Henrique Trevisan, HT, Onboarding
- **Função:** Onboarding
- **Contexto:** Onboarding em grupo, jornada início do cliente, apresentações
- **Pergunta de contexto:** "O onboarding tá em refinamento ou já entrou em implementação?"
- **Estrutura de pastas:**
  ```
  onboarding/
    materiais/
    scripts/
    grupos/
  ```

---

### Bruna
- **Apelidos / variações:** Bruna, Bru, Social, Pesquisa
- **Função:** Pesquisa e Social
- **Contexto:** Conteúdo Instagram/TikTok, pesquisa com base, entrevistas com clientes, ICP
- **Pergunta de contexto:** "Tá mais em conteúdo, pesquisa de ICP ou os dois essa semana?"
- **Estrutura de pastas:**
  ```
  conteudo/
    instagram/
    tiktok/
  pesquisa/
    entrevistas/
    icp/
  ```

---

### Helen
- **Apelidos / variações:** Helen, Hellen
- **Função:** Operacional
- **Contexto:** Operação geral, processos internos, suporte ao time
- **Pergunta de contexto:** "Qual é o processo que você tá tocando essa semana?"
- **Estrutura de pastas:**
  ```
  operacional/
    processos/
    tarefas/
  ```

---

### Luan
- **Apelidos / variações:** Luan, Operacional
- **Função:** Operacional
- **Contexto atual:** High Ticket + Spy de ofertas (busca ofertas black pra mandar pra Helen — produto principal)
- **Pergunta de contexto:** "Luan — você ainda cuida da parte de espionagem / Spy, ou tá full no High Ticket agora?"
- **Pergunta extra (High Ticket):** "Quais concorrentes você tá analisando no High Ticket agora? Me passa os nomes que eu já crio as pastas."
- **Pergunta extra (Spy):** "E pro Spy de ofertas — tem produtos ou nichos específicos que você monitora agora?"
- **Estrutura de pastas:**
  ```
  high-ticket/
    [uma pasta por concorrente respondido na pergunta extra]
    referencias/
    scripts/
  spy/
    ofertas-black/
    [uma pasta por nicho/produto informado, se houver]
  ```
- **Nota:** As pastas de concorrentes e nichos são criadas dinamicamente com os nomes que o Luan informar. Se não informar nenhum, criar `high-ticket/concorrente-1/` como placeholder.

---

### Luanna
- **Apelidos / variações:** Luanna, Lu, Vendas, CS
- **Função:** Vendas / CS Proativo
- **Contexto:** Outreach, CS proativo, clientes em risco (Health Score — Frente 4), follow-up de retenção
- **Pergunta de contexto:** "Tá mais em outreach ou em CS proativo essa semana?"
- **Estrutura de pastas:**
  ```
  leads/
  cs/
    follow-up/
    relatorios-saude/
  ```

---

### Isabella
- **Apelidos / variações:** Isabella, Isa, Isabella Carvalho, Head
- **Função:** Head de Operações
- **Contexto:** Retenção, UX da jornada, churn, coordenação das 4 frentes
- **Pergunta de contexto:** "Qual frente tá mais quente essa semana?"
- **Estrutura de pastas:**
  ```
  churn/
  ux/
  frentes/
    frente-1-churn-involuntario/
    frente-2-onboarding/
    frente-3-cancel-flow/
    frente-4-health-score/
  relatorios/
  ```

---

## Projetos ativos (contexto geral)

- **High Ticket:** Lançamento do Debrief Done-for-You (R$6k/mês). Luan é o responsável atual. Envolve análise de concorrentes do segmento high ticket.
- **Dunning / Churn involuntário:** Grace Period, emails D+0-D+7, retry por tipo de recusa. Thais executa, Isabella coordena.
- **Onboarding:** Protótipo pronto, aguarda implementação dev. Henrique T lidera.
- **Cancel flow + banner in-app:** Mapeado, aguarda dev.
- **Health Score + CS Proativo (Frente 4):** Luanna executa o playbook de retenção ativa.
- **Espionagem / Miro:** Luan monta boards de concorrentes no Miro pra produto principal (Swipe Offers).
- **Conteúdo e ICP:** Bruna pesquisa base e produz social.
