---
name: iniciar
description: Carrega o contexto da Swipe Offers e do foco da pessoa no começo de cada sessão. Usar quando abrir o Claude Code.
---

# /iniciar — Carregar contexto

Use no começo de cada sessão de trabalho.

## O que fazer

1. Ler `_contexto/empresa.md`, `_contexto/preferencias.md` e `_contexto/estrategia.md`
2. Ler `CLAUDE.md` se houver alguma regra adicional
3. Apresentar um resumo curto e direto

## Fluxo

### Se os arquivos estão configurados

Apresente um resumo de no máximo 5 linhas:

```
Contexto carregado.

**Negócio:** Swipe Offers — SaaS de inteligência competitiva
**Sua função:** [função de estrategia.md]
**Foco agora:** [prioridade de estrategia.md]
**Lembretes:** [preferências importantes, ex: "sem travessões", "tom conversacional"]

O que você quer fazer hoje?
```

### Se `_contexto/estrategia.md` ainda não foi personalizado

Avise:

```
Parece que o setup ainda não foi feito.
Roda /setup pra configurar o sistema pra sua função na Swipe — leva 2-3 minutos.
```

## Comportamento

- Tom direto, sem enrolação. Não dizer "Olá! Fico feliz em ajudar!"
- Não listar os arquivos lidos
- Se houver `tarefas.md`, mencionar até 3 itens pendentes no topo
- Aguardar o usuário responder o que quer fazer
