# Swipe Offers

## O que é

SaaS de inteligência competitiva para profissionais de marketing digital brasileiro. Biblioteca de ofertas reais, criativos, VSLs e funis validados com tráfego real. Quebra cloakers, atualização diária.

**Missão:** ser a maior central de dados do marketing global.

## Produtos

- **Swipe Offers (plataforma):** R$97/mês
- **Swipe + SPY (plataforma + extensão Chrome):** R$147/mês — extensão é uma biblioteca de anúncios
- **Plano Gratuito:** entrada/trial
- **Debrief Done-for-You:** R$6.000/mês — desenhado, não lançado

## Métricas (referência, atualizar a cada mês)

- Assinantes ativos (Stripe): ~745
- MRR: ~R$82K
- ARPU: ~R$110
- ARR: ~R$980K
- Quick Ratio: 1,54
- Crescimento 2025: +172% sem ads

## Time

| Pessoa | Função |
|---|---|
| **Trevizan** | Sócio — dono do produto |
| **Caique** | CEO |
| **Thais** | CRM — contato para notificações de falha de pagamento |
| **Guibson** | Dados / Activation Points |
| **Henrique T** | Onboarding em grupo |
| **Bruna** | Pesquisa e social |
| **Helen** | Operacional |
| **Luan** | Operacional + Espionagem (boards Miro) |
| **Luanna** | Vendedora dedicada / CS Proativo (Frente 4) |
| **Isabella** | Head de Operações (período de teste) |

## Frentes de trabalho ativas

1. **Frente 1 — Churn involuntário** (falha de pagamento): Smart Retries, Grace Period, dunning emails, retry logic por tipo de recusa
2. **Frente 2 — Onboarding e ativação** primeira sessão
3. **Frente 3 — Cancel flow inteligente** + banner in-app
4. **Frente 4 — Health Score e CS Proativo** (executado pela Luanna)

## Stack da plataforma

- Next.js 14.2.35 com App Router
- Vercel (hosting)
- Firebase (banco)
- React + Tailwind + shadcn/ui + Radix
- Stripe (pagamento)
- Active Campaign (ESP — dunning, jornadas)
- Sem GTM, sem heatmap, sem gravação de sessão (Fase 2)

## Ferramentas internas

- ClickUp, Supabase, HubSpot, Hotmart
- Stripe (dashboard de assinaturas)
- Active Campaign
- Miro (espionagem, boards)
- Google Drive, Gmail, Calendar
- Obsidian (mapeamentos)

## Domínios

- swipeoffers.com.br — site principal
- app.swipeoffers.com.br — plataforma
- Emails: `@swipeoffers.com.br`

## Documentação interna

Plano de execução completo no ClickUp: **Espaço da equipe → Plano de Execução — Swipe Offers**
