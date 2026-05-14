---
name: setup
description: >
  Configura o Swipe Kit pra função da pessoa no time. Reconhece pelo nome,
  cria a estrutura de pastas e faz um onboarding leve e conversacional.
  Usar quando rodar /setup pela primeira vez.
---

# /setup: Configuração do Swipe Kit

## Antes de começar: ler o contexto

Antes de qualquer mensagem, ler:

1. `_contexto/empresa.md`: o que é a Swipe, produtos, time, projetos ativos
2. `templates/time/pessoas.md`: quem é quem, apelidos, função, concorrentes conhecidos, estrutura de pastas
3. `templates/funcoes/mapa.md`: skills por função

Com isso em mãos, o Claude já sabe quem é o Luan, o que é o High Ticket, quais concorrentes ele analisa, o que é o Spy de ofertas.

---

## Verificação inicial

Checar se `_contexto/estrategia.md` já tem conteúdo real (sem `<!-- NOT CONFIGURED -->`).

- Se **já tem**: avisar que o setup já foi feito e perguntar se quer refazer.
- Se **não tem**: rodar o onboarding abaixo.

---

## Passo 1: Pedir o nome

> "Oi. Qual é o seu nome?"

Aguardar resposta.

---

## Passo 2: Reconhecer ou não a pessoa

Buscar o nome em `templates/time/pessoas.md` (nome e apelidos).

### Se reconheceu → seguir o fluxo específico da pessoa (abaixo)
### Se não reconheceu → fluxo genérico (no final desse arquivo)

---

## Fluxos específicos por pessoa

### Luan

**1.** Sinalizar o que vai fazer antes de criar:

> "Boa, Luan. Sei que você tá tocando o High Ticket e também algumas partes do Spy de ofertas do produto principal. Vou criar algumas pastas pra você, tudo bem?"

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

> "Criei as pastas do High Ticket pros concorrentes que já tenho mapeados: Jeremy, Bluehackers, Full Sales System e Thiago Reis, mais referências e scripts. Tem alguma coisa que você quer mudar ou alguma pasta que quer adicionar?"

Aguardar. Ajustar se ele pedir.

**4.** Spy de ofertas:

> "Criei também uma pasta pro Spy de ofertas. Tem alguma subpasta que você quer adicionar que já faz parte do seu processo? Se quiser, pode me contextualizar como é o seu processo de spy que eu já crio um plano aqui pra você."

Aguardar. Se ele contextualizar o processo, registrar em `_contexto/estrategia.md` e criar as subpastas que fizer sentido.

**5.** Copiar as skills do Luan (Operacional) de `templates/funcoes/mapa.md` pra `.claude/commands/`.

Instruir a instalar o find-skills:

> "Roda esse comando no terminal pra instalar o find-skills:
>
> `npx skills add https://github.com/vercel-labs/skills --skill find-skills`"

**6.** Preencher `_contexto/estrategia.md` com tudo que foi dito.

**7.** Oferecer resumo de skills e pastas:

> "Quer um resumo das skills disponíveis e das pastas que eu criei?"

Se sim: mostrar em três blocos:

**Bloco 1 — Pastas do workspace:**
Listar todas as pastas do workspace: as criadas pelo setup pra função da pessoa (high-ticket/, spy/ e subpastas) mais as pastas base do kit (_contexto/ — contexto da Swipe e das suas prioridades, dados/ — arquivos de entrada como prints e PDFs, marca/ — identidade visual da Swipe).

**Bloco 2 — Skills ativas:**
Listar as skills em `.claude/commands/` (exceto setup, iniciar, syncar, atualizar) com uma linha descrevendo o que cada uma faz. Não listar os atalhos.

**Bloco 3 — Catálogo completo** (disponíveis em `templates/skills/` e `templates/skills/rmbc/`, instalar quando precisar):
Listar o que ainda não foi copiado pra commands, também com uma linha por skill descrevendo o que faz. Finalizar com:
> "Pra ativar qualquer uma, fala o nome que eu copio pra você."

**8.** Encerrar e oferecer próximos passos:

> "Pronto. Abre uma nova conversa e digita /iniciar, eu já carrego teu contexto lá.
>
> Caso queira, posso te mandar agora um prompt pra você jogar na nova conversa pra começar com alguma coisa específica. Por exemplo:
> - Analisar uma VSL ou página de concorrente
> - Montar um board no Miro com o que você já tem
> - Criar uma análise de oferta a partir de um link ou print
> - Comparar criativos de dois concorrentes
> - Conectar com o Obsidian e registrar um mapeamento
>
> Quer que eu monte um desses pra você?"

Aguardar. Se quiser um prompt específico, montar e mandar pronto pra copiar e colar na nova conversa.

**9.** Oferecer contexto da Swipe:

> "Quer que eu te passe um resumo sobre a Swipe ou sobre o High Ticket? O que é o produto, onde você entra, o que tá sendo construído."

Se sim, ler `_contexto/empresa.md` e montar um resumo enxuto focado no que é relevante pro papel do Luan.

**10.** Fechar:

> "Boa, Luan. Se tiver qualquer dúvida, pode me mandar, ou chamar a Isa."

---

### Outras pessoas reconhecidas (fluxo padrão com contexto)

**1.** Confirmar a função e criar as pastas da estrutura definida em `pessoas.md`:

> "[Nome]. [confirmar o que a pessoa faz]. Criando as pastas pra você."

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

> "[Nome], qual é a sua função na Swipe? Pode ser: Sócio, CEO, CRM, Dados, Onboarding, Pesquisa/Social, Operacional, Vendas/CS ou Head de Ops."

**2.** Criar as pastas do perfil mais próximo baseado na função informada.

**3.** Mostrar o que foi criado, perguntar se quer mudar.

**4.** Perguntar o foco da semana.

**5.** Perguntar sobre processo e arquivos.

**6.** Copiar skills da função. Encerrar.

---

## Regras gerais

- Tom de colega, não assistente. Nada de "posso?", "deseja que eu?", "gostaria de?"
- Criar as pastas antes de perguntar: mostrar o resultado, não pedir aprovação prévia
- Uma pergunta por vez: não listar tudo de uma vez
- Não criar pastas que a pessoa não pediu além da estrutura base
- Gerar `_contexto/estrategia.md` sempre ao final com o que foi dito
- Skills comuns já estão em `.claude/commands/` (iniciar, syncar, atualizar, setup): não recopiar
