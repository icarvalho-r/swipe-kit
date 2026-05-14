---
name: pesquisa-concorrentes
description: >
  Executa pesquisa competitiva completa de mercado via até 14 subagentes em
  paralelo, em dois modos: (1) Competitor Analysis — seeds conhecidos, 4-6
  agentes analisando Meta Ads, TikTok, YouTube, funis, social intel; (2)
  Opportunity Discovery — varredura multi-fonte com 10-14 agentes cobrindo
  Meta Ads multi-geo, ClickBank, Digistore24, Gumroad, Amazon KDP, Etsy,
  Reddit mining, TikTok Creative Center, Google Trends e niche-scout social.
  Entrega relatório visual HTML no design guide do projeto + markdown
  complementar. Use quando o usuário pedir "pesquisa de mercado",
  "analisa meus concorrentes", "quem tá escalando no nicho", "pesquisa competitiva",
  "estuda os concorrentes diretos", "manda uma pesquisa completa dos players",
  "analisa a biblioteca de anúncios dos meus concorrentes", "mapeia os perfis
  dos concorrentes no instagram", "niche scout dos concorrentes",
  "descobre oportunidades de nicho", "oceano azul", "varredura de mercado".
---

# /pesquisa-concorrentes — Pesquisa Competitiva de Mercado

Pesquisa de mercado escalável com dois modos de operação:

- **Modo A — Competitor Analysis**: análise profunda de concorrentes conhecidos (seeds). Funis, ofertas, copies, criativos pagos, padrões escalados + presença social (niche-scout). 4-6 agentes.
- **Modo B — Opportunity Discovery**: varredura ampla multi-fonte pra descobrir nichos, ofertas validadas e oceanos azuis. 10-14 agentes paralelos cobrindo Meta Ads multi-geo, marketplaces (ClickBank/Digistore/Gumroad), Amazon KDP, Etsy, Reddit, TikTok, Google Trends e social intel.

Entregue em HTML visual no design guide do projeto, pronto pra identificar padrões e oportunidades.

## Dependências

- **Design guide do projeto:** `projetos/[projeto]/marca/design-guide.md` — LER antes de montar o HTML pra aplicar cores, tipografia e estilo correto
- **Contexto do negócio:** `_contexto/empresa.md` e `_contexto/preferencias.md`
- **Hub do projeto:** `projetos/[projeto]/[projeto].md` — atualizar com wikilink ao final
- **Contexto ativo:** `contexto-ativo.md` — adicionar entrada na seção "O que mudou recentemente"
- **Puppeteer MCP em HEADLESS sempre** (regra absoluta — nunca abrir navegador visível)

---

## Fase 1 — Calibração (antes de disparar agentes)

**Nunca execute sem confirmar escopo.** Ad-hoc competitive research gasta muito tempo de agente — calibrar errado desperdiça a rodada. Faça as perguntas abaixo e espere resposta. Se o usuário responder só parcialmente, assuma os defaults explicitamente e diga quais.

### Perguntas comuns (ambos os modos)

1. **Modo de operação:** concorrentes conhecidos (Modo A) ou varredura ampla pra descobrir oportunidades (Modo B)? Se o usuário tem seeds, é Modo A. Se quer "descobrir nichos", "oceano azul", "o que tá escalando", é Modo B. Pode ser híbrido.
2. **Mercado geográfico:** só BR, só gringo, ou mix? Quais geos específicos? (Brasileiros podem se beneficiar de ideias de mecanismo/oferta gringas mesmo quando o público final é BR.)
3. **Escopo do produto:** só cursos/mentorias? Incluir PDFs, ebooks, SaaS, agências, produtos físicos? Cada categoria tem funil diferente — definir direito evita perder tempo com players irrelevantes.
4. **Profundidade x abrangência:** top 5 a fundo (funil completo + 10-15 ads decodificados + oferta detalhada) OU top 10-15 superficial?
5. **Entregável:** arquivo único HTML + markdown complementar (padrão) OU formato alternativo específico?
6. **Social Intel (niche-scout):** incluir análise de presença social dos concorrentes no Instagram e TikTok? (Padrão: sim. Adiciona ~15 min.)

### Perguntas extras — Modo A (Competitor Analysis)

7. **Concorrentes seed:** tem 3-7 nomes específicos? Se tem, pede a lista. Seeds aceleram muito e evitam ruído.

### Perguntas extras — Modo B (Opportunity Discovery)

8. **Macro-nichos a incluir/excluir:** algum vertical vetado? (ex: emagrecimento, finanças, manifestação). Algum obrigatório?
9. **Perfil do público-alvo:** público leigo (decisão emocional, urgência) ou técnico (sagaz, cria objeção)? Evitar nichos onde o comprador "já viu 100+ ofertas" ou tem formação técnica forte.
10. **Tom das ofertas:** White puro (educacional, zero risco de ban) / Grey / Dark grey (mix estratégico na linha tênue)? Classificar cada oportunidade nos 4 tons: White, Grey, Black, Dark Grey.
11. **Universalidade cultural:** a oferta precisa funcionar cross-culture (sem depender de sistema jurídico, educacional ou cultural local)? Regra prática: "se a dor existe em qualquer casa com wifi, tá dentro."
12. **Faixa de ticket:** range de preço-alvo (ex: $9-27 low-ticket, $47-97 mid, $197+ high).
13. **Plataforma de venda:** Gumroad, Hotmart, ClickBank, Digistore24, Shopify, outro?
14. **Prazo de payback:** precisa gerar receita em X dias? (impacta agressividade da estratégia e escolha de plataforma por tempo de saque)

Defaults Modo A: **BR+gringos mistos, descobrir do zero, só cursos/mentorias, top 5 a fundo, HTML+markdown, social intel incluso**.
Defaults Modo B: **multi-geo (US/UK/AU + Tier 2), varredura ampla, low-ticket $9-27, público leigo, dark grey, universal, Gumroad, 14 agentes máximos**.

**Avisar proativamente antes de começar:**
- TikTok Creative Center bloqueia scraping headless (HTTP 403) sem cookie de sessão autenticada. Alternativas: Pipiads, Minea, BigSpy (pagas) ou login TikTok Business manual.
- YouTube Ads pré-roll não é acessível via scraping — depende de ferramenta dedicada (DeepTube, VidIQ).
- Meta Ads Library é a fonte mais rica e geralmente funciona via Puppeteer.
- Digistore24 marketplace completo só acessível via login — dados restritos aos "top offers" oficiais.

---

## Fase 2 — Disparar agentes em paralelo

Use `Agent` com `subagent_type: general-purpose`, **mandando todos em uma única mensagem com múltiplos tool calls** pra rodar concorrentemente. Agentes em **background** (`run_in_background: true`) quando não há dependência entre eles — libera a sessão principal enquanto rodam. Budget típico: 25-35 min cada, rodando em paralelo.

**Briefing comum a TODOS os agentes:** cada agente precisa ser self-contained (não vê a conversa). Incluir:
- Contexto de negócio do cliente (1 parágrafo)
- Lista completa de seeds + público-alvo (ou filtros de descoberta, conforme o modo)
- Categorias a incluir/excluir
- Instrução explícita pra carregar Puppeteer MCP via `ToolSearch` com query `select:mcp__puppeteer__puppeteer_navigate,mcp__puppeteer__puppeteer_screenshot,mcp__puppeteer__puppeteer_evaluate`
- Regra absoluta: **HEADLESS sempre** (`launchOptions: {"headless": true}`)
- Fallback: se Puppeteer bloquear, tentar `WebFetch` e `WebSearch`, registrar explicitamente o que falhou
- Output: markdown estruturado retornado como mensagem final (NÃO salvar arquivos no disco — só retornar texto)
- "Não invente dados" — se não conseguir extrair algo, dizer explicitamente

---

### MODO A — Competitor Analysis (4-6 agentes)

Usar quando o usuário tem seeds conhecidos ou quer analisar concorrentes específicos de um vertical.

#### Agente A1 — Meta Ads Library

Para cada seed, navegar em `https://www.facebook.com/ads/library/?active_status=active&ad_type=all&country=BR&q=<NOME>&search_type=keyword_unordered` e extrair via `puppeteer_evaluate`:
- Headline/body/CTA do ad
- Data de início (anúncios rodando 30+ dias = performando)
- Número de variações (sinal de A/B test = escala)
- Formato (vídeo/imagem/carrossel)
- Landing page de destino
- Plataformas (FB/IG/Messenger/Audience Network)

Depois **descobrir concorrentes adicionais** buscando termos genéricos do nicho (ex: `day trade`, `emagrecer`, `marketing digital`, conforme o caso). Identificar os 3-5 advertisers mais escalados não presentes na lista seed.

**Output esperado:** relatório por concorrente (seeds + descobertos) com top 5 ads mais escalados, padrões de hook, copy dominante, formato. Seção final de síntese cross-competitor.

#### Agente A2 — TikTok Creative Center + YouTube

**Parte 1 — TikTok:** tentar `https://ads.tiktok.com/business/creativecenter/inspiration/topads/pc/en?period=30&region=BR` (ou outra região conforme mercado). Filtrar por categoria relevante. Se bloquear (403 comum), reportar explicitamente e seguir.

**Parte 2 — YouTube:** pra cada seed, usar `WebSearch` pra encontrar canal oficial, navegar via Puppeteer, extrair:
- Inscritos + frequência de upload
- Top 10 vídeos por views
- 3-5 vídeos mais recentes
- Identificar VSLs/webinars/vídeos-isca (títulos com "aula", "método", "como fazer X", "ganhei R$Y")
- Link do funil na descrição do canal

**Parte 3 — YouTube Ads:** tentar DeepTube/VidIQ/Social Blade. Geralmente falha — reportar se falhou.

**Output esperado:** por canal, o que foi extraído + síntese de hooks, formatos e padrões de thumbnail/primeiros 3 segundos.

#### Agente A3 — Funis, landing pages e ofertas

Para cada seed, usar `WebSearch` pra descobrir a landing page principal (domínio próprio > Hotmart/Ticto/Eduzz/Braip). Navegar com Puppeteer e extrair:
- `document.title`, H1, subheadline
- Texto completo via `document.body.innerText` (limitar a 15k chars)
- Tem VSL? Duração?
- Preço/oferta (procurar "R$", "12x", "de X por Y", "$", "USD")
- Bônus listados
- Garantia (7/30/60 dias)
- Escassez/urgência (contadores, "últimas vagas")
- CTAs (quantidade, destino, copy do botão)
- Testemunhos (quantos, formato)
- FAQ
- Screenshot do topo via `puppeteer_screenshot`

**Classificar o tipo de funil:** captura+webinar / VSL direto / desafio / comunidade gratuita / checkout direto.

**Output esperado:** por concorrente, ficha técnica completa do funil + oferta + copies destacadas (3-5 trechos fortes). Seção de síntese: funil dominante, faixa de preço, bônus universais, mecanismos únicos nomeados, avatares alvo, oportunidades.

#### Agente A4 — Social Intel (pipeline niche-scout condensado)

Integra a metodologia do squad niche-scout numa execução condensada: Hunter → Validator → Analyst → Auditor → Compiler num único agente.

Para cada seed + concorrentes descobertos, mapear presença social no **Instagram** e **TikTok**:

**Fase Hunter (descoberta):**
- Usar `WebSearch` pra encontrar handles oficiais: `"<nome>" instagram`, `"<marca>" tiktok`, `"<founder>" instagram`
- Separar conta da MARCA vs. conta PESSOAL do founder (padrão do mercado: founder pessoal > marca)
- Navegar via Puppeteer headless e extrair: handle, nome, bio, seguidores, posts, seguindo

**Fase Validator (autoridade):**
- O perfil é realmente do nicho? (não homônimo, não abandonado)
- Tem credenciais verificáveis na bio? (CNPJ, certificações, parcerias declaradas)
- Tem prova social real? (logos de clientes, menções de mídia, participação em eventos)
- Crescimento orgânico vs. suspeita de compra (ratio seguidores/engajamento)
- Classificar: **Validado** / **Suspeito** / **Descartado**

**Fase Analyst (engajamento):**
- Taxa de engajamento estimada (curtidas + comentários / seguidores × 100) nos últimos posts visíveis
- Qualidade dos comentários (bots vs. genuínos — verificar via amostragem)
- Frequência de postagem (semanal/mensal/parado)
- Formatos dominantes: Reels, carrossel, estático, stories, lives
- Benchmark contra o nicho (média do vertical)

**Fase Auditor (conteúdo):**
- Consistência temática com o nicho (mista vs. focada)
- Originalidade vs. repost/trending genérico
- Produção visual: profissional, amadora, template
- Uso de vídeo longo (sinal de VSL/webinar/educacional)
- Highlights fixados relevantes (aula, webinar, treinamento, live)

**Fase Compiler (ranking):**
- Score composto: Autoridade (30%) + Engajamento (30%) + Conteúdo (25%) + Tamanho (15%)
- Ranking separado pra Instagram e TikTok
- Identificar quem é a "cara pública" do vertical (founder com maior capital social)
- Listar associações relevantes (parcerias, mentorias, co-brands entre founders)

**Pergunta crítica a responder explicitamente:**
- Algum concorrente usa o Instagram/TikTok como canal de captação de leads (link na bio pra captura/webinar/aula)?
- Algum founder tem presença significativa no TikTok BR? (o TikTok é geralmente vazio pra B2B/SaaS BR)
- Quem são os "rostos" do vertical e qual o ranking por capital social?

**Output esperado:** relatório markdown com: (1) tabela ranking IG por seguidores + score, (2) tabela ranking TikTok se aplicável, (3) análise de autoridade por player, (4) gaps de formato identificados, (5) associações entre founders/mentores, (6) resposta explícita às 3 perguntas críticas.

---

### MODO B — Opportunity Discovery (10-14 agentes)

Usar quando o objetivo é descobrir nichos, ofertas validadas e oceanos azuis. Varredura multi-fonte em paralelo máximo. Os agentes são especializados por fonte de dados — quanto mais agentes, mais rápido (cada um roda independente).

**Regra de ouro do cruzamento:** a mágica tá onde **2+ fontes apontam a mesma dor** (KDP bestseller + Reddit threads desesperadas + Meta ad rodando 90+ dias = sinal triplo fortíssimo).

#### Agentes B1-B3 — Meta Ad Library por geo (3 agentes paralelos)

Um agente por cluster geográfico. Cada um busca termos genéricos do nicho-alvo + sub-nichos.

| Agente | Geos | Foco |
|---|---|---|
| B1 | US, UK, AU | Mercados maduros Tier 1 — ofertas escaladas com 60+ dias ativas |
| B2 | PH, ZA, IN | Tier 2 anglófono — validar gap (oferta roda em T1 mas ninguém ataca T2) |
| B3 | BR, PT, MX | Lusófono/hispânico — referências de mecanismo/oferta pra adaptar |

Para cada geo, navegar em `https://www.facebook.com/ads/library/?active_status=active&ad_type=all&country=<GEO>&q=<TERMO>&search_type=keyword_unordered` e extrair:
- Advertiser name + número de ads ativos
- Headline/body/CTA dos top 5 por advertiser
- Data de início (30+ dias = performando, 90+ dias = muito escalado)
- Número de variações (A/B test = escala)
- Formato dominante (vídeo/imagem/carrossel)
- Landing page de destino

**Filtro de qualidade:** ads rodando 60+ dias com 10+ variações = validado Tier 1. Priorizar.

**Output esperado:** lista de advertisers por geo, top ads com copies completas, sinal de escala, landing pages. Seção de "ofertas que rodam em T1 mas ZERO presença em T2" (gap de oportunidade).

#### Agente B4 — ClickBank Marketplace

Escanear via `cbtrends.com` ou diretamente no marketplace. Filtros:
- Gravity 3-80 (validado mas não hiper-saturado)
- Ticket $7-47 (sweet spot low-ticket)
- Categorias: todas menos supplements físicos e brainwave audio (mainstream saturado)

Extrair por produto:
- Nome, vendor, gravity atual, gravity trend (subindo/descendo)
- Ticket médio, comissão, tipo de funil (VSL/carta de vendas/quiz)
- Copy da página de afiliado
- Landing page principal

**Output esperado:** top 15-20 produtos ranqueados por gravity crescente × ticket baixo. Padrões de copy e funil. Nichos com gravity 3-30 (validado mas pouca competição).

#### Agente B5 — Digistore24 + Gumroad

**Digistore24:** acessar top offers oficiais (marketplace completo requer login — extrair o que der). Filtrar por:
- Ticket $9-47, categorias relevantes
- Trend de vendas crescente

**Gumroad:** navegar categorias e bestsellers via Puppeteer. Extrair:
- Título, preço, número de vendas/reviews
- Descrição completa
- Tipo de produto (PDF, template, curso, workbook)

**Atenção especial:** escadas de oferta ($2 workbook → $19 guide → $47 bundle). Produto inicial como ativo de aquisição = padrão replicável.

**Output esperado:** top 15 produtos entre as duas plataformas. Padrões de preço, formato e copy.

#### Agente B6 — Amazon KDP + Etsy (demanda silenciosa)

**Amazon KDP:** escanear bestsellers em categorias relevantes ($2.99-$14.99). Usar `WebSearch` + Puppeteer em páginas de bestsellers por subcategoria.
- Título, preço, reviews, rating, data de publicação
- Sub-nichos com bestsellers recentes (publicados últimos 6 meses) = demanda crescente
- Genéricos saturados vs. ultra-específicos abertos

**Etsy:** buscar PDFs/printables/workbooks nos nichos-alvo.
- Listings com 1k+ sales = demanda comprovada
- Star Sellers = nicho validado comercialmente
- Fillable/interactive PDFs > printables simples (tendência 2025-2026)

**Regra:** KDP bestseller + Etsy Star Seller no mesmo sub-nicho = **sinal fortíssimo** de demanda silenciosa sem saturação em ads.

**Output esperado:** top 10 nichos validados por demanda de compra passiva, ordenados por força do sinal. Incluir: nicho, evidência KDP, evidência Etsy, saturação estimada em Meta Ads, veredito (Oceano Azul / Validado / Saturado).

#### Agente B7 — Reddit Mining (dores universais)

Escanear 30-50 subreddits relevantes via `WebSearch` e Puppeteer. Buscar threads com:
- Alto engagement (100+ upvotes, 50+ comments)
- Tom desesperado ("please help", "at my wits end", "nothing works", "desperate")
- Perguntas recorrentes sobre o mesmo problema

**Subreddits por vertical (adaptar ao nicho):**
- Parenting: r/toddlers, r/Parenting, r/beyondthebump, r/pottytraining, r/breastfeeding
- Pets: r/cats, r/dogs, r/puppy101, r/CatAdvice, r/reactivedogs, r/DogTraining
- Home: r/CleaningTips, r/HomeImprovement, r/organization, r/gardening
- Hobbies: r/Bonsai, r/Aquariums, r/drawing, r/guitarlessons
- Saúde leve: r/sleep, r/bruxism, r/Posture, r/ADHD

**Output esperado:** top 15 dores universais ranqueadas por: frequência de threads × intensidade emocional × ausência de solução dominante. Cada dor com 3-5 quotes reais dos threads (matéria prima pra hooks de ad).

#### Agente B8 — TikTok Creative Center + YouTube Ads

**TikTok Creative Center:** tentar `https://ads.tiktok.com/business/creativecenter/inspiration/topads/pc/en?period=30&region=US` (e outras regiões). Se bloquear (403 comum), buscar via `WebSearch` por "[nicho] tiktok ads 2026" e extrair do que encontrar.

**YouTube:** buscar canais de nicho + ads (via WebSearch por "[nicho] youtube ad", "[produto] review"). Extrair:
- Canais com VSLs/webinars nos nichos-alvo
- Formatos de thumbnail e títulos que escalam
- Links de funil na descrição

**Output esperado:** swipe file de ads escalando por nicho + padrões de hook dos primeiros 3 segundos.

#### Agente B9 — Google Trends + Keywords

Usar `WebSearch` pra consultar:
- Google Trends dos nichos shortlistados (últimos 12 meses, trend crescente vs. decrescente)
- Volume de busca via dados públicos (Ubersuggest, Ahrefs free tier, AnswerThePublic)
- "People also ask" e "Related searches" como termômetro de demanda

**Output esperado:** ranking dos nichos por: trend direction (subindo/estável/descendo) × volume de busca × sazonalidade. Nichos com trend subindo + volume médio (1k-50k/mês) = sweet spot.

#### Agente B10 — Social Intel Discovery (niche-scout amplo)

Similar ao Agente A4, mas em modo discovery: em vez de mapear seeds, **descobrir quem são os players sociais** dos nichos shortlistados.

Para cada nicho candidato:
- Buscar top 5 perfis Instagram + TikTok via `WebSearch`
- Extrair: seguidores, engajamento, formato dominante, link na bio
- Classificar autoridade: ninguém dominante (oceano azul) vs. 1-2 gurus (saturando) vs. fragmentado (oportunidade de consolidação)

**Output esperado:** mapa social por nicho com: (1) existe guru dominante? (2) nível de sofisticação do conteúdo existente, (3) oportunidade de entrar como autoridade.

#### Agentes B11-B14 — Slots flexíveis

Agentes extras para:
- **B11 — Ranking bruto automatizado:** recebe output dos outros agentes e faz scoring cross-fonte antes da curadoria humana. Score = (presença em N fontes × intensidade de sinal por fonte). Reduz tempo de curadoria manual de ~60min pra ~30min.
- **B12 — Plataformas de afiliados específicas:** Hotmart Global, Eduzz, Braip (mercado lusófono), Warrior Plus, JVZoo.
- **B13 — Pinterest + Quora mining:** Pinterest pra nichos visuais (home, hobby, parenting); Quora pra dores com perguntas detalhadas.
- **B14 — Análise de funis dos top 3 descobertos:** depois que os primeiros agentes retornarem, disparar este pra dissecar os funis completos dos 3 melhores candidatos (como o Agente A3, mas focado nos descobertos).

**Nem todos precisam rodar.** B11 (ranking) é altamente recomendado. B12-B14 são opcionais conforme o nicho e o tempo disponível. Perguntar ao usuário quantos agentes quer disparar.

---

### Modos híbridos

Se o usuário tem seeds MAS também quer descobrir oportunidades adjacentes, combinar:
- Agentes A1-A4 (análise dos seeds) + Agentes B6-B9 (discovery em paralelo)
- Total: 8 agentes. Melhor dos dois mundos.

---

## Fase 3 — Síntese e entregáveis

Depois que todos os agentes retornarem, compilar tudo em:

### 3.1 — Relatório HTML visual (entregável principal)

**Caminho:** `projetos/[projeto]/pesquisa-mercado-YYYY-MM-DD.html`

**Design:** LER `projetos/[projeto]/marca/design-guide.md` ANTES de escrever qualquer CSS. Aplicar cores, tipografia, border-radius e elementos-chave exatamente como definidos. Não inventar sistema de design — usar o que o projeto já tem.

**Estrutura obrigatória** (usa âncoras internas com `nav.anchor` sticky):
1. **Hero** — título, data, subtitle, meta (cliente, canais, N concorrentes)
2. **Stats** — 4 métricas chave (N players, N ads analisados, maior escala individual, etc.)
3. **Nav sticky** com links pras seções
4. **TL;DR / Resumo executivo** — 3 takeaways + 1 callout com o maior insight + 1 callout orange com aviso metodológico se algo falhou
5. **Concorrentes seed** — card grid, cada card com headline blockquote, kv pairs (ads ativos, ticket, funil, mecanismo, autoridade), tags, `<details>` expansível com copies completas
6. **Concorrentes descobertos** — mesmo formato, destacar com card dourado os 2-3 de escala máxima
7. **Funis & ofertas** — tabela de tipos de funil + faixas de preço + callout com gap (garantia 7d universal = oportunidade)
8. **Canais (Meta/YouTube/TikTok)** — tabela de escala Meta + tabela de inscritos YouTube + callout sobre TikTok se bloqueou
9. **Social Intel (niche-scout)** — ranking Instagram por seguidores + score composto + ranking TikTok se aplicável + associações entre founders/mentores + resposta às 3 perguntas críticas (captação via IG? TikTok presente? Quem é a cara do vertical?)
10. **Marketplaces** (Modo B) — tabela ClickBank + Digistore + Gumroad com gravity, ticket, trend. Callout com escadas de oferta identificadas
11. **Demanda silenciosa** (Modo B) — KDP + Etsy cross-reference, nichos com sinal triplo (compra passiva + Reddit + ads)
12. **Reddit threads** (Modo B) — top dores com quotes reais dos threads (matéria prima pra hooks)
13. **Trends & keywords** (Modo B) — Google Trends direction + volume + sazonalidade por nicho
14. **Padrões cross-competitor** — pattern grid com hooks, promessas, provas, CTAs, bônus, mecanismos; + avatares (incluindo sub-servidos)
15. **Classificação por tom** (Modo B) — cada oportunidade com 4 ângulos: White / Grey / Black / Dark Grey
16. **Oportunidades** — numbered list com 8-12 ângulos livres, cada um com tag "Angle:"
17. **Recomendações acionáveis** — 5-7 próximos passos em ordem de prioridade
18. **Ressalvas metodológicas** — o que falhou e por quê, o que fica de lição de casa

**Características visuais obrigatórias:**
- Dark theme se design guide for dark (maioria dos projetos do Rafael)
- Tipografia de display + body conforme design guide (ex: Barlow Condensed + Manrope na Escola Scalper)
- Badges de escala coloridos (ouro = escala máxima, verde accent = alta, cinza = média, vermelho apagado = zero ads)
- Cards expansíveis via `<details>` pra copies completas sem poluir
- Nav sticky no topo com backdrop-blur
- Grain overlay em 8% se design guide mencionar
- Callouts (verde = insight positivo, laranja = aviso/limitação)
- Responsivo até 720px

**O que NUNCA fazer:**
- Linkar Google Fonts só se o design guide pedir fonte diferente da padrão do sistema
- Usar emojis decorativos (só preservar emojis que apareceram nas copies originais dos concorrentes)
- Cores fora do design guide
- Gradientes genéricos "AI-looking" (roxo em branco, etc.)

### 3.2 — Markdown complementar

**Caminho:** `projetos/[projeto]/pesquisa-mercado-YYYY-MM-DD.md`

Frontmatter com `tipo: pesquisa-mercado`, `projeto: [projeto]`, `data: YYYY-MM-DD`, `tags`, e `relatorio-visual: pesquisa-mercado-YYYY-MM-DD.html`.

Conteúdo: mirror enxuto do HTML em markdown, mas **preservando TODAS as copies completas dos ads como blockquotes** (pra busca Ctrl+F no Obsidian). Ordem: sumário exec → escala observada (tabela) → ficha por concorrente seed → ficha por descoberto → padrões → oportunidades → próximos passos → ressalvas.

### 3.3 — Atualização do hub do projeto

Editar `projetos/[projeto]/[projeto].md` adicionando sob seção "Pesquisa de mercado" (criar seção se não existir):

```markdown
## Pesquisa de mercado
- [[pesquisa-mercado-YYYY-MM-DD|Pesquisa de mercado · YYYY-MM-DD]] — análise competitiva de N players (X seeds + Y descobertos) via Meta Ads Library, YouTube e funis. Relatório visual: `pesquisa-mercado-YYYY-MM-DD.html`
```

### 3.4 — Atualização do contexto-ativo

Editar `contexto-ativo.md` adicionando entrada nova no topo de "O que mudou recentemente" com:
- Data + título curto
- Links pros 2 arquivos (HTML + md)
- 3-5 bullets dos maiores insights (não o relatório inteiro)
- Nota de ressalvas críticas se houver (ex: TikTok bloqueado)

---

## Entrega final ao usuário

Mensagem final deve conter:
1. **Link clicável markdown** pro HTML logo no topo (formato `[nome.html](caminho/relativo)` — nunca path absoluto)
2. Resumo dos entregáveis (3 arquivos: HTML, md, hub atualizado)
3. **3 takeaways prioritários** (não o relatório todo — só os 3 maiores insights acionáveis)
4. **2 ressalvas importantes** (o que ficou faltando, próxima rodada)
5. Pergunta aberta sobre o próximo passo (dissecar concorrente X a fundo, começar copy de VSL inspirada, cravar mecanismo próprio, etc.)

Manter a mensagem final abaixo de 250 palavras. O relatório HTML já tem o detalhe — a mensagem só precisa ser o handoff.

---

## Regras

- **Nunca disparar agentes sem calibrar escopo primeiro.** Orçamento de tempo por rodada é alto (Modo A: 60-90 min · Modo B: 90-150 min agregado). Calibrar errado desperdiça a rodada inteira.
- **Puppeteer sempre em headless.** Regra absoluta do Rafael. Único caso de navegador visível: se ele pedir explicitamente ("abre no Chrome").
- **Não salvar arquivos nos agentes.** Eles devem retornar markdown como mensagem final. Quem consolida e grava arquivos é a sessão principal.
- **Design guide do projeto é inegociável.** Se o projeto não tiver design-guide preenchido, avisar explicitamente antes de criar HTML com fallback padrão.
- **Preservar copies originais exatas.** Ao registrar copies de concorrentes, copiar texto integral (incluindo emojis, pontuação, quebras) — é isso que torna o relatório útil pra futura decomposição.
- **Cross-referenciar antes de afirmar.** Se um agente diz "não encontrei anúncios de X" mas outro diz "X tem presença orgânica forte", reconciliar e reportar os dois fatos, não só um. No Modo B, cruzar fontes é a regra de ouro: sinal em 2+ fontes = forte, sinal em 1 fonte = fraco.
- **Atualizar contexto-ativo e hub é obrigatório.** Sem isso, a pesquisa vira órfã no vault e desaparece da memória do Claude na próxima sessão.
- **Link clicável no final.** Sempre. Formato markdown relativo ao workspace root.
- **Modo B: classificar por tom.** Toda oportunidade descoberta deve ter os 4 ângulos (White/Grey/Black/Dark Grey) com exemplo de promessa em cada tom. O dark grey é o alvo operacional — mix que maximiza CTR sem matar a conta.
- **Modo B: background agents.** Disparar agentes em `run_in_background: true` e dar updates intermediários ao usuário conforme cada agente retorna (ex: "1/5 completou — KDP + Etsy"). Não esperar todos terminarem pra dar o primeiro feedback.
- **Modo B: ranking bruto antes da curadoria.** Se B11 (ranking automatizado) estiver ativo, usar seu output como primeira triagem — reduz curadoria manual de ~60min pra ~30min. A sessão principal faz a curadoria qualitativa final.
