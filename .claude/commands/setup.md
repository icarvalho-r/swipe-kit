---
name: setup
description: >
  Configura o Swipe Kit pra função da pessoa no time. Reconhece pelo nome,
  cria a estrutura de pastas e faz um onboarding leve e conversacional.
  Usar quando rodar /setup pela primeira vez.
---

# /setup — Configuração do Swipe Kit

## Antes de começar — ler o contexto

Antes de qualquer mensagem, ler:

1. `_contexto/empresa.md` — o que é a Swipe, produtos, time, projetos ativos
2. `templates/time/pessoas.md` — quem é quem, apelidos, função, concorrentes conhecidos, estrutura de pastas
3. `templates/funcoes/mapa.md` — skills por função

Com isso em mãos, o Claude já sabe quem é o Luan, o que é o High Ticket, quais concorrentes ele analisa, o que é o Spy de ofertas.

---

## Verificação inicial

Checar se `_contexto/estrategia.md` já tem conteúdo real (sem `<!-- NOT CONFIGURED -->`).

- Se **já tem**: avisar que o setup já foi feito e perguntar se quer refazer.
- Se **não tem**: rodar o onboarding abaixo.

---

## Passo 1 — Pedir o nome

> "Oi. Qual é o seu nome?"

Aguardar resposta.

---

## Passo 2 — Reconhecer ou não a pessoa

Buscar o nome em `templates/time/pessoas.md` (nome e apelidos).

### Se reconheceu → seguir o fluxo específico da pessoa (abaixo)
### Se não reconheceu → fluxo genérico (no final desse arquivo)

---

## Fluxos específicos por pessoa

### Luan

**1.** Responder de forma casual, já sinalizando que vai criar as pastas:

> "Ah, Luan — você tá tocando o High Ticket né. Deixa eu criar as pastas pra você."

**2.** Criar silenciosamente toda a estrutura:
```
high-ticket/
  jeremy/
  bluehackers/
  full-sales-system/
  thiago-reis/
  referencias/
  scripts/
spy/
  ofertas-black/
```

**3.** Mostrar o que foi criado e abrir pra ajuste:

> "Criei as pastas do High Ticket: Jeremy, Bluehackers, Full Sales System e Thiago Reis — mais referências e scripts. Tem alguma coisa que você quer mudar?"

Aguardar. Ajustar se ele pedir (adicionar/renomear/remover pasta).

**4.** Perguntar sobre o Spy:

> "Criei também a pasta do Spy de ofertas. Tem alguma subpasta que você quer adicionar aí pro seu processo?"

Aguardar. Criar o que ele pedir.

**5.** Contextualizar o processo:

> "Beleza. Quer me contextualizar como é o seu processo? Tem algum arquivo que você quer subir dentro das tuas pastas?"

Aguardar. Se ele quiser subir arquivos, orientar onde colocar. Se quiser explicar o processo, ouvir e salvar em `_contexto/estrategia.md`.

**6.** Copiar as skills do Luan (Operacional) de `templates/funcoes/mapa.md` pra `.claude/commands/`.

**7.** Preencher `_contexto/estrategia.md` com o que foi dito.

**8.** Encerrar:

> "Pronto. Roda /iniciar no começo de cada nova conversa que eu já carrego teu contexto. Se quiser salvar alguma coisa no GitHub, /syncar."

---

### Outras pessoas reconhecidas (fluxo padrão com contexto)

**1.** Confirmar a função e criar as pastas da estrutura definida em `pessoas.md`:

> "[Nome] — [confirmar o que a pessoa faz]. Criando as pastas pra você."

**2.** Mostrar o que foi criado:

> "Criei [lista das pastas]. Quer mudar alguma coisa?"

Aguardar e ajustar.

**3.** Usar a **"Pergunta de contexto"** definida em `pessoas.md`:

> [pergunta específica da função]

Aguardar.

**4.** Perguntar sobre processo e arquivos:

> "Quer me contextualizar como é o teu processo? Tem algum arquivo que você quer subir dentro das pastas?"

Aguardar. Registrar em `_contexto/estrategia.md`.

**5.** Copiar skills da função. Encerrar com:

> "Pronto. /iniciar no começo de cada conversa, /syncar pra salvar no GitHub."

---

## Fluxo genérico (pessoa não reconhecida)

**1.** Perguntar a função:

> "[Nome] — qual é a sua função na Swipe? Pode ser: Sócio, CEO, CRM, Dados, Onboarding, Pesquisa/Social, Operacional, Vendas/CS ou Head de Ops."

**2.** Criar as pastas do perfil mais próximo baseado na função informada.

**3.** Mostrar o que foi criado, perguntar se quer mudar.

**4.** Perguntar o foco da semana.

**5.** Perguntar sobre processo e arquivos.

**6.** Copiar skills da função. Encerrar.

---

## Regras gerais

- Tom de colega, não assistente. Nada de "posso?", "deseja que eu?", "gostaria de?"
- Criar as pastas antes de perguntar — mostrar o resultado, não pedir aprovação prévia
- Uma pergunta por vez — não listar tudo de uma vez
- Não criar pastas que a pessoa não pediu além da estrutura base
- Gerar `_contexto/estrategia.md` sempre ao final com o que foi dito
- Skills comuns já estão em `.claude/commands/` (iniciar, syncar, atualizar, setup) — não recopiar
