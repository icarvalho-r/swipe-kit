# Mapa Função → Skills

Esse arquivo é lido pelo `/setup` pra decidir quais skills copiar pra `.claude/commands/` de cada pessoa do time.

Skills comuns (todo mundo recebe, já estão em `.claude/commands/`):
- `/iniciar`
- `/syncar`
- `/atualizar`
- `/setup`

---

## Funções

### Sócio (Trevizan)

Decisões estratégicas, visão de produto, reports executivos, negociações com parceiros.

**Skills:**
- `analisar-dados`
- `email-profissional`
- `proposta-comercial`
- `slide`
- `hormozi` — frameworks de oferta e posicionamento
- `funnel-architecture` (rmbc)
- `pricing-strategy` (rmbc)

---

### CEO (Caique)

Liderança, métricas, comunicação com time e externos, decks de pitch.

**Skills:**
- `analisar-dados`
- `email-profissional`
- `slide`
- `roteiro-post`
- `hormozi`
- `lander-copy` (rmbc)
- `funnel-audit` (rmbc)

---

### CRM (Thais)

Email, jornadas, dunning, automações de retenção, comunicação por falha de pagamento.

**Skills:**
- `email-profissional`
- `roteiro-post`
- `analisar-dados`
- `email-promo` (rmbc)
- `reengagement-sequence` (rmbc)
- `cart-abandonment-flow` (rmbc)
- `welcome-sequence` (rmbc)
- `broadcast-email` (rmbc)

---

### Dados / Activation (Guibson)

Instrumentação, dashboards, activation points, análise quantitativa.

**Skills:**
- `analisar-dados`
- `publicar-site`
- `slide`
- `funnel-audit` (rmbc)
- `competitor-offer-analysis` (rmbc)

---

### Onboarding (Henrique T)

Onboarding em grupo, apresentações de boas-vindas, jornada início do cliente.

**Skills:**
- `email-profissional`
- `slide`
- `roteiro-post`
- `welcome-sequence` (rmbc)
- `soap-opera-sequence` (rmbc)
- `hormozi`

---

### Pesquisa e Social (Bruna)

Conteúdo pra Instagram, TikTok, pesquisa com base, entrevistas com clientes.

**Skills:**
- `carrossel`
- `roteiro-post`
- `analisar-dados`
- `copy-decoder`
- `meta-ads-criativos`
- `hook-battery` (rmbc)
- `fb-ad-copy` (rmbc)
- `ugc-brief` (rmbc)
- `ad-angle-generator` (rmbc)

---

### Operacional (Helen, Luan)

Operação geral, processos, espionagem de concorrentes, suporte interno.

**Skills:**
- `email-profissional`
- `proposta-comercial`
- `carrossel`
- `roteiro-post`
- `copy-decoder`
- `pesquisa-concorrentes` (rmbc)
- `competitor-offer-analysis` (rmbc)
- `niche-scout`

---

### Vendas / CS Proativo (Luanna)

Outreach, CS proativo, retenção ativa, follow-up de clientes em risco (Frente 4 — Health Score).

**Skills:**
- `email-profissional`
- `roteiro-post`
- `analisar-dados`
- `email-promo` (rmbc)
- `reengagement-sequence` (rmbc)
- `soap-opera-sequence` (rmbc)
- `upsell-script` (rmbc)
- `hormozi`

---

### Head de Operações (Isabella)

Tudo. Sem filtro de função.

**Skills principais:**
- `analisar-dados`
- `carrossel`
- `copy-decoder`
- `email-profissional`
- `hormozi`
- `meta-ads-criativos`
- `niche-scout`
- `proposta-comercial`
- `publicar-site`
- `roteiro-post`
- `slide`
- `frontend-design`
- `ui-ux-pro-max`
- `derick-vsl`
- `gold-finder`
- `perpetuo-white`
- `squad-creator-pro`

**RMBC (via `templates/skills/rmbc/`):**
- `email-promo`, `welcome-sequence`, `reengagement-sequence`, `cart-abandonment-flow`
- `fb-ad-copy`, `hook-battery`, `lander-copy`, `vsl-script`, `copy-rewrite`
- `ad-angle-generator`, `funnel-architecture`, `funnel-audit`, `competitor-offer-analysis`
- `pesquisa-concorrentes` e demais

---

## Nota sobre skills RMBC

Skills com sufixo `(rmbc)` ficam em `templates/skills/rmbc/`. O `/setup` copia de lá pra `.claude/commands/` no mesmo fluxo das demais.

Para acessar todas as skills RMBC disponíveis, usar `/write-copy` (lista completa) ou chamar diretamente (ex: `/hook-battery`).
