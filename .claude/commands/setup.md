---
name: setup
description: >
  Configura o Swipe Kit pra função da pessoa no time. Reconhece a pessoa pelo nome,
  confirma função, pergunta sobre o contexto atual e copia as skills certas.
  Usar quando rodar /setup pela primeira vez.
---

# /setup — Configuração do Swipe Kit

## Antes de começar — ler o contexto

Antes de qualquer mensagem, ler:

1. `_contexto/empresa.md` — o que é a Swipe, produtos, time, projetos ativos
2. `templates/time/pessoas.md` — quem é quem no time, apelidos, função e contexto atual de cada pessoa
3. `templates/funcoes/mapa.md` — quais skills correspondem a cada função

Com isso carregado, o Claude já sabe: o que é o High Ticket, quem é o Luan, o que a Thais faz, o que tá ativo em cada frente. Usar esse contexto naturalmente nas perguntas — sem precisar explicar o que é a Swipe pra pessoa.

---

## Verificação inicial

Checar se `_contexto/estrategia.md` já tem conteúdo real (sem `<!-- NOT CONFIGURED -->`).

- Se **já tem conteúdo personalizado**: avisar que o setup já foi feito e perguntar se quer refazer.
- Se **não tem ou está vazio**: rodar o onboarding abaixo.

---

## Onboarding

### Passo 1 — Pedir o nome

> "Oi. Qual é o seu nome?"

Aguardar a resposta.

---

### Passo 2 — Reconhecer a pessoa

Ler `templates/time/pessoas.md` e tentar identificar a pessoa pelo nome ou apelido informado.

**Se reconheceu:**

Confirmar diretamente com tom casual — sem perguntar de novo:

> "Luan — você é o Operacional né. Sei que você tá tocando o High Ticket agora.
> Qual é o seu foco principal na próxima semana?"

Adaptar a fala ao contexto da pessoa conforme o `templates/time/pessoas.md`:
- Se a pessoa tem um campo **"Pergunta de contexto"** definido, usar exatamente aquela pergunta
- Caso contrário, mencionar o projeto ativo mais relevante pra função e perguntar sobre o foco atual
- Tom: conversa entre colegas, não onboarding corporativo

**Se não reconheceu (nome desconhecido):**

> "[Nome] — qual é a sua função na Swipe?"

Listar as opções de forma natural:

> "Pode ser: Sócio, CEO, CRM, Dados, Onboarding, Pesquisa/Social, Operacional, Vendas/CS ou Head de Ops."

---

### Passo 3 — Pergunta de contexto

Pedir o foco atual com uma pergunta específica, não genérica.

Se a função for conhecida, contextualizar:

- **Operacional (Luan):** "Luan — você ainda cuida da parte de espionagem / Spy, ou tá full no High Ticket agora?"
- **CRM (Thais):** "Tá focada no dunning ainda ou entrou coisa nova?"
- **Pesquisa/Social (Bruna):** "Conteúdo, pesquisa de ICP ou os dois?"
- **Onboarding (Henrique T):** "O onboarding tá em implementação ou ainda em refinamento?"
- **Vendas/CS (Luanna):** "Tá no CS proativo ou tem campanha nova rodando?"
- **Dados (Guibson):** "Instrumentação ainda ou já entrou análise de cohort?"
- **Sócio/CEO:** "Qual a prioridade que tá consumindo mais energia agora?"
- **Head de Ops (Isabella):** "Qual frente tá mais quente essa semana?"
- **Função desconhecida:** "Qual é o seu foco principal agora?"

Aguardar a resposta.

---

### Passo 4 (opcional) — Preferências

> "Tem alguma preferência de tom ou coisa que te incomoda em texto de IA? Se não tiver, sigo o padrão da Swipe."

Se disser "tudo bem" ou não tiver preferência específica: manter `_contexto/preferencias.md` como está, sem modificar.

---

## Processamento — gerar os arquivos

### 1. Preencher `_contexto/estrategia.md`

```markdown
# Foco Atual — [Nome]

## Função na Swipe
[Função]

## Foco principal agora
[Resposta da pergunta de contexto]

## O que pode esperar
[Inferir do contexto e função — ex: "Tarefas relacionadas a high ticket, espionagem e operação"]

---
*Atualize esse arquivo quando seu foco mudar.*
```

### 2. Copiar skills da função pra `.claude/commands/`

Ler `templates/funcoes/mapa.md` e copiar as skills da função:

- Skills de arquivo `.md` → copiar `templates/skills/<skill>.md` pra `.claude/commands/<skill>.md`
- Skills de pasta → copiar `templates/skills/<skill>/` pra `.claude/commands/<skill>/`
- Skills RMBC `(rmbc)` → copiar `templates/skills/rmbc/<skill>/` pra `.claude/commands/<skill>/`

Skills comuns (já estão em `.claude/commands/`, não precisa copiar):
- `/iniciar`, `/syncar`, `/atualizar`, `/setup`

### 3. Atualizar `_contexto/preferencias.md` (só se a pessoa pediu algo diferente)

Se respondeu algo na pergunta opcional que diverge do padrão: adicionar seção `## Preferências pessoais` no final.
Se não pediu nada: não tocar no arquivo.

---

## Mensagem final

```
[Nome], pronto.

Como [função], você tem:
- /iniciar — carrega contexto da Swipe e do teu foco no começo da sessão
- /syncar — salva no GitHub
[lista das skills específicas copiadas]

Como usar: chama qualquer skill com / (ex: /email-profissional, /hook-battery).
Roda /iniciar no começo de cada nova conversa.
```

Tom direto. Sem entusiasmo excessivo. Sem listas de instruções longas.

---

## Regras

- Tom casual — conversa entre colegas, não onboarding corporativo
- Se reconheceu a pessoa, NÃO pedir a função de novo — confirmar e seguir
- Se a função for desconhecida, pedir e mapear pro mapa de funções
- Não criar pastas extras (projetos/, clientes/, etc.)
- Gerar tudo de uma vez no final — não ir arquivo por arquivo durante as perguntas
- Máximo 3-4 perguntas no total
