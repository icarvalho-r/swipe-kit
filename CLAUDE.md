# Swipe Kit — Claude Code OS pro time da Swipe Offers

Este repositório é o kit de boas-vindas pro time da Swipe.

Se você acabou de clonar:
1. Rode `/setup` pra configurar o sistema pra sua função (uns 3 minutos)
2. Use `/iniciar` no começo de cada sessão pra carregar o contexto

---

## Contexto do negócio

No início de toda conversa, ler:

1. `_contexto/empresa.md` — o que é a Swipe Offers, produtos, métricas, time
2. `_contexto/preferencias.md` — tom de voz, estilo de escrita, o que evitar
3. `_contexto/estrategia.md` — foco atual da empresa e da sua função

Usar essas informações como base pra qualquer resposta ou decisão. Não confirmar que leu — só usar naturalmente.

Para qualquer tarefa visual (carrossel, proposta, slide, deck, post), consultar `marca/design-guide.md`.

---

## Fluxo de trabalho

Antes de executar qualquer tarefa, verificar se existe uma skill relevante em `.claude/commands/`.
Se encontrar, seguir as instruções da skill.
Se não encontrar, executar a tarefa normalmente.

Ao concluir uma tarefa que parece repetível, perguntar:

> "Isso pode virar uma skill pra próxima vez. Quer que eu crie?"

Só perguntar quando o padrão de repetição for claro.

---

## Aprender com correções

Quando o usuário corrigir algo, melhorar uma resposta ou der uma instrução que parece permanente ("na verdade é assim", "não faça mais isso", "prefiro assim", "sempre que...", "evita...", "da próxima vez..."), perguntar:

> "Quer que eu salve isso pra não precisar repetir?"

Se sim, salvar onde faz mais sentido:

- **Sobre a Swipe ou o time** → `_contexto/empresa.md`
- **Sobre preferências de escrita** → `_contexto/preferencias.md`
- **Sobre prioridades atuais** → `_contexto/estrategia.md`
- **Regra de comportamento no workspace** → este `CLAUDE.md`

Salvar com uma linha nova clara, sem reformatar o arquivo inteiro. Mostrar a linha adicionada.

Não perguntar pra correções óbvias (ex: "na verdade o arquivo se chama X"). Só quando a informação tiver valor duradouro.

---

## Manter contexto atualizado

Ao terminar uma tarefa que mudou algo relevante (novo processo, mudança de foco, nova skill, ferramenta instalada), perguntar:

> "Isso mudou algo no contexto. Quer que eu atualize os arquivos de memória?"

Se sim:
- **Mudança no produto, time ou estratégia da Swipe** → `_contexto/empresa.md`
- **Mudança de foco ou prioridade** → `_contexto/estrategia.md`
- **Correção de tom ou estilo** → `_contexto/preferencias.md`
- **Nova skill ou pasta** → `CLAUDE.md`

Mostrar o que vai mudar antes de salvar. Não reformatar o arquivo inteiro.

Quando não souber se algo mudou, rodar `/atualizar`.

---

## Criação de skills

Quando o usuário pedir pra criar uma skill:

1. Verificar se já existe um template relevante em `templates/skills/`
2. Perguntar: "Essa skill é específica pra Swipe ou útil em qualquer projeto?"
   - Específica da Swipe → salvar em `.claude/commands/nome.md` (local)
   - Útil em qualquer projeto → salvar em `~/.claude/commands/nome.md` (global)
3. Ler `_contexto/empresa.md` e `_contexto/preferencias.md` pra calibrar
4. Se a skill precisar de arquivos de apoio, criar dentro da pasta da skill

---

## Sobre a Swipe Offers (resumo)

SaaS de inteligência competitiva pra marketing digital. Biblioteca de ofertas, criativos, VSLs e funis validados com tráfego real.

**Produtos:** Swipe Offers (R$97/mês), Swipe + SPY (R$147/mês), Plano Gratuito, Debrief Done-for-You (R$6k/mês).

**Foco atual:** retenção (churn ~30% acelerado, M1→M2 perde 31pp). Cada decisão precisa se pagar em 60 dias.

Detalhes completos em `_contexto/empresa.md`.
